---
title: Otimizar na borda – CloudFront (BYOCDN)
description: Saiba como configurar o CloudFront BYOCDN para otimizar na borda no LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:41:48.977Z'
TQID: 'https://experienceleague.adobe.com/fGlW2FIQooU-8nv8H1lH3WOxinOFUVK7RVNol7ACPq8'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: 5a903ec2b6976e7997c45848265d022ca67bed9d
workflow-type: tm+mt
source-wordcount: 2204
ht-degree: 96%

---


# CloudFront (BYOCDN)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após sua conclusão, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de definir a configuração do CloudFront, verifique se você tem:

* Uma distribuição existente do CloudFront que atende ao seu site.
* Permissões do AWS IAM para criar funções Lambda, funções do IAM, distribuições do CloudFront e políticas de cache.
* Uma chave da API do Edge Optimize obtida na interface do usuário do LLM Optimizer. Para obter as etapas, consulte [Recuperar suas chaves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para testar o roteamento de preparo, consulte [Chave de API de preparo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Etapa 1: criar origem de otimização na borda**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > guia Origens

1. Clique em **Criar origem**.

2. Configure a origem:
   * **Domínio de origem:** `live.edgeoptimize.net`
   * **Nome** `EdgeOptimize_Origin`

3. Deixe todos os outros campos com seus valores padrão.

4. Adicionar cabeçalhos personalizados:

   | Cabeçalho | Valor |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Sua chave de API |
   | `x-forwarded-host` | `www.example.com` |
   | `x-edgeoptimize-fetcher-key` | Sua chave de busca (necessária somente no caso de WAF do incluir na lista de permissões) |

   Substitua `www.example.com` pelo domínio real do seu site e `Your API key` pela chave de API da Otimização na borda fornecida pelo seu representante da Adobe.

5. Clique em **Criar origem**.

![Criação de origem do Cloudfront](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**Etapa 2: criar função de solicitação do visualizador**

**Navegação:** Console do AWS > CloudFront > Funções

1. Clique em **Criar função**.

2. Configurar o:
   * **Nome:** `edgeoptimize-routing`
   * **Tempo de execução:** `cloudfront-js-2.0`

3. Substitua o código padrão pelo código de [viewer-request.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/cloudfront-function/viewer-request.js).

   Antes de publicar, personalize os seguintes valores no código:

   * `YOUR_DEFAULT_ORIGIN` — Substitua com o nome de sua origem padrão existente (encontrada na guia CloudFront > Distribuições > [Sua Distribuição] > Origens).
   * `TARGETED_PATHS` — Defina como `null` para direcionar todas as páginas do HTML ou defina como uma matriz de caminhos específicos, por exemplo, `['/', '/products', '/about']`.

4. Clique em **Salvar alterações** > **Função de publicação**.

![Criação da função do Cloudfront](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**Etapa 3: configurar política de cache**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

Verifique a política de cache atualmente anexada ao seu comportamento. Clique em **Editar** sobre seu comportamento e observe a seção **Solicitações de chave de cache e origem** para identificar seu cenário:

* **Cenário A (legado):** você vê um botão de opção com o rótulo **Configurações de cache legadas** selecionado. Não há lista suspensa com nomes de política — em vez disso, você vê as configurações de cabeçalho e TTL em linha.
* **Cenário B (política personalizada):** você vê a **Política de cache** selecionada com um nome de política que você ou sua equipe criou (não uma política fornecida pelo AWS).
* **Cenário C (Política gerenciada):** você vê a **Política de cache** selecionada com um nome fornecido pelo AWS como `CachingOptimized`, `CachingDisabled` ou `CachingOptimizedForUncompressedObjects` — estas não podem ser editadas.

**Cenário A: configurações de cache legadas**

Se seu comportamento usar configurações de cache legadas:

1. Em **Solicitações de chave de cache e origem**, você verá **Configurações de cache legadas** selecionada.

2. Adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url` à lista de permissões **Cabeçalhos**:

   * Selecione **Incluir os seguintes cabeçalhos** na lista suspensa.
   * Adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url`.
     ![Cache legado do Cloudfront](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   Se você já tiver **Todos** selecionados no menu suspenso de Cabeçalhos, ignore esta etapa — todos os cabeçalhos são automaticamente encaminhados à origem.

3. Verifique a configuração de **Armazenamento em cache de objetos**:

   * Se definido como **Personalizar** — é recomendável definir **TTL mínimo** como `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.
   * Se definido como **Usar cabeçalhos de cache de origem** — nenhuma alteração será necessária.

4. Clique em **Salvar alterações**.

**Cenário B: não legado com uma política de cache personalizada**

Se o seu comportamento já utiliza uma política de cache personalizada (uma que você criou, não uma política gerenciada pelo AWS):

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Clique na sua política atual.

2. Clique em **Editar**.

3. É recomendável definir **TTL Mínimo** como `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.
   ![Configurações de TTL da política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. Em **Configurações de chave de cache** >**Cabeçalhos**, juntamente com suas inclusões existentes, adicione `x-edgeoptimize-config` e `x-edgeoptimize-url`.
   ![Cabeçalhos de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Clique em **Salvar alterações**.

**Cenário C: não legado com uma política de cache gerenciada (AWS)**

Se o seu comportamento utiliza uma política de cache gerenciada pelo AWS (por exemplo, `CachingOptimized`), você não poderá editá-la. Você precisa criar uma nova política de cache personalizada que replique as configurações de política gerenciada existentes e adicione os cabeçalhos de Otimização na borda por cima.

**Parte 1: anote suas configurações atuais de política de cache gerenciada**

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Localize e clique na política de cache gerenciada atualmente associada ao seu comportamento (por exemplo, `CachingOptimized`).

2. Anote todas as configurações existentes:
   * TTL mínimo, TTL máximo, TTL padrão
   * Cabeçalhos incluídos na chave do cache
   * Cookies incluídos na chave do cache
   * Strings de consulta incluídas na chave do cache
   * Suporte para compactação (Gzip, Brotli)

**Parte 2: criar uma nova política de cache personalizada com as mesmas configurações + configuração de Otimização na borda**

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Clique em **Criar política de cache**.

2. **Nome:** `edgeoptimize-cache`

   ![Nome da política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Repita todas as configurações indicadas na Parte 1, com as seguintes modificações:

   * Recomenda-se definir **TTL mínimo** para `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.

   ![Configurações de TTL da política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * Em **Configurações de chave de cache** > **Cabeçalhos**, inclua tudo o que a política gerenciada tinha, além de adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url`.

   ![Cabeçalhos de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Clique em **Criar**.

5. Volte para o seu comportamento e associe a política recém-criada:

   **Navegação:** Console da AWS > CloudFront > Distribuições >[Sua distribuição] > Comportamentos

   1. Edite seu comportamento.
   2. Em **Solicitações de chave de cache e origem**, selecione **Política de cache**.
   3. Escolha `edgeoptimize-cache` na lista suspensa.
   4. Clique em **Salvar alterações**.

**Etapa 4: criar função Lambda@Edge (solicitação e resposta de origem)**

>[!IMPORTANT]
>As funções Lambda@Edge **devem ser criadas na região `us-east-1` (N. Virgínia)**. Esse é um requisito do AWS. Mesmo que a função seja criada em `us-east-1`, o AWS a replica automaticamente em todos os locais de borda do CloudFront no mundo inteiro, para que seja executada no local de borda mais próximo do visualizador. Verifique se você está na região `us-east-1` do Console do AWS antes de continuar.

**Criar a função Lambda**

**Navegação:** Console do AWS > Lambda

1. Clique em **Criar função**.

2. Selecione **Criar do zero**.

3. Configurar o:
   * **Nome da função:** `edgeoptimize-origin`
   * Deixe todos os outros campos com seus valores padrão.

4. Clique em **Criar função**.

5. No editor de código, substitua o código padrão pelo código de [origin-request-response.js](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/origin-request-response.js).

6. Clique em **Implantar** para salvar o código.

7. Observe o **nome da função de execução** mostrado em **Configuração** > **Permissões** (por exemplo, `edgeoptimize-origin-role-xxxxx`). Isso é necessário nas etapas a seguir.

**Atualizar a política de confiança da função de execução**

A função criada automaticamente só confia em `lambda.amazonaws.com`. Para Lambda@Edge, você também deve adicionar `edgelambda.amazonaws.com`.

**Navegação:** Console do AWS > IAM > Funções >[sua função da etapa anterior] > guia Relações de confiança

1. Clique em **Editar política de confiança**.

2. Substitua a política pelo conteúdo de [trust-policy.json](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/trust-policy.json).

3. Clique em **Atualizar política**.

>[!WARNING]
>O principal de serviço `edgelambda.amazonaws.com` é **obrigatório** para Lambda@Edge. Sem isso, o CloudFront não poderá invocar sua função em locais de borda.

**Corrigir a política de permissões do CloudWatch Logs**

A função criada automaticamente vem com uma política `AWSLambdaBasicExecutionRole` configurada para Lambda regular, que possui a região e o nome do grupo de logs incorretos para Lambda@Edge. Você precisa atualizá-la.

**Navegação:** Console da AWS > IAM > Funções > [sua função] > guia Permissões > clique no nome da política associada (por exemplo, `AWSLambdaBasicExecutionRole-xxxx`)

1. Clique em **Editar**.

2. Substitua a política pelo conteúdo de [cloudwatch-policy.json](https://github.com/adobe/llmo-code-samples/blob/main/optimize-at-edge/cloudfront/lambda/cloudwatch-policy.json).

   No JSON, substitua `ACCOUNT_ID` pela sua ID da conta AWS real (encontrada no canto superior direito do Console do AWS) e `FUNCTION_NAME` pelo nome da sua função Lambda (por exemplo, `edgeoptimize-origin`).

3. Clique em **Salvar alterações**.

>[!WARNING]
>A região no ARN deve ser `*` — a Lambda@Edge é executada no local de borda mais próximo do visualizador, portanto, os logs são gravados no CloudWatch na região do local de borda (por exemplo, `ap-south-1`, `eu-west-1`), não necessariamente `us-east-1`. O grupo de logs usa um nome com prefixo de região: `/aws/lambda/us-east-1.FUNCTION_NAME`, onde `us-east-1` é sempre a região de origem da função.

**Publicar uma versão**

1. Na página de funções, clique em **Ações** (canto superior direito) >**Publicar nova versão**.

2. Adicione uma descrição.

3. Clique em **Publicar**.
   ![Publicação Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Copie ou anote o **ARN da função**: você precisará dele na próxima etapa.
   ![ARN Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**Etapa 5: associar as funções e a política de cache ao comportamento**

**Navegação:** Console da AWS > CloudFront > Distribuições >[Sua distribuição] > Comportamentos

1. Edite seu comportamento.

2. Se você criou uma nova política de cache na Etapa 3 (Cenário C), defina a **Política de cache** para`edgeoptimize-cache`.
   ![Política de cache](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. Em **Associações de funções**, configure:

   * **Solicitação do visualizador:** `edgeoptimize-routing`
   * **Solicitação de origem:** função com Versão ARN da Etapa 4 (em **Publicar uma versão**)
   * **Resposta de origem:** função com Versão ARN da Etapa 4 (em **Publicar uma versão**)

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Clique em **Salvar alterações**.

**Permitir a otimização na borda por meio de regras de firewall (opcional)**

{{waf-allowlist-setup}}

**Etapa 6: testar a configuração**

**1. Tráfego de bots de teste (deve ser otimizado)**

Envie uma solicitação com um agente de usuário de bot agêntico. Na **primeira solicitação**, o Edge Otimize pode retornar uma resposta com proxy (não otimizada) enquanto processa e armazena em cache a página. Você pode identificar isso pelo cabeçalho `x-edgeoptimize-proxy: 1` na resposta.

Simular uma solicitação de bot de IA usando um agente de usuário agêntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Teste o tráfego humano (NÃO deve ser afetado)**

Simule uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta **não** deve conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos aos de antes da habilitação da otimização na borda.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bots (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém uma ID de solicitação exclusiva | Ausente |
| `x-edgeoptimize-fo` | Presente somente se houver um failover (valor: `1`) | Ausente |

{{verify-routing-status-in-ui}}

**4. Verificar se os logs estão fluindo corretamente**

Depois de executar as solicitações de teste acima, verifique se os logs estão sendo gravados para as funções CloudFront e Lambda@Edge.

*Logs de função do CloudFront (`edgeoptimize-routing`)*

**Navegação:** Console da AWS > CloudWatch > Grupos de logs (em `us-east-1` ou na região em que sua distribuição do CloudFront está configurada)

1. Procure um grupo de log chamado `/aws/cloudfront/function/edgeoptimize-routing`.
2. Abra o fluxo de log mais recente.
3. Para solicitações agênticas, você deve ver entradas como:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. Para solicitações não agênticas, você deve ver:
   * `Routing to Default origin for userAgent: ...`

Você também pode verificar a guia **Métricas** em **Console da AWS > CloudFront > Funções > edgeotimize-routing** para exibir as contagens de invocação e as taxas de erro.

*Logs do Lambda@Edge (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Os logs do Lambda@Edge são gravados no CloudWatch na **região do local da borda** que atendeu à solicitação, não `us-east-1`. Verifique o CloudWatch na região da AWS mais próxima de onde você executou o comando curl.

**Navegação:** Console da AWS > CloudWatch > Grupos de logs (verifique se você está na região correta)

1. Procure um grupo de log chamado `/aws/lambda/us-east-1.edgeoptimize-origin`.
2. Abra o fluxo de log mais recente.
3. Para solicitações agênticas, você deve ver entradas como:
   * `Calling Edge Optimize Origin for agentic requests`: caminho principal
   * `Calling Default Origin in case of failover for agentic requests`: caminho de failover
   * `Failover Triggered for agentic requests`: detecção de failover de resposta de origem

Caso o grupo de logs não esteja presente, verifique se as permissões do IAM foram atualizadas corretamente na Etapa 4. Verifique também outras regiões da AWS próximas — a localização de borda que atendeu à sua solicitação pode ser diferente da que você espera.

**Resolução de Problemas**

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| Não há `x-edgeoptimize-request-id` em resposta a solicitações agênticas | O grupo de origem não está encaminhando para o Edge Optimize | Verifique se `YOUR_DEFAULT_ORIGIN` foi substituído corretamente no código da função CloudFront (Etapa 2). |
| Erros 403 em solicitações agênticas | Chave de API inválida ou ausente | Verifique o valor do cabeçalho`x-edgeoptimize-api-key` nos cabeçalhos personalizados de origem do Edge Optimize (Etapa 1). |
| Não foi possível encontrar os logs do CloudWatch para Lambda@Edge | Permissões do IAM incorretas | Verifique se a política de permissões de logs do CloudWatch foi atualizada (Etapa 4). Observação: os logs do Lambda@Edge aparecem na região de borda que atendeu à solicitação, não necessariamente em `us-east-1`. |
| O cache não está respeitando `cache-control: no-store` | O TTL mínimo pode estar muito alto | Defina o TTL mínimo para `0` na política de cache (Etapa 3). Se o TTL mínimo já for muito curto, esse pode não ser o problema. |
| O tráfego regular (não agêntico) foi interrompido após a configuração | Configuração incorreta da política de cache | Se você criou uma nova política de cache (Cenário C), replique todas as configurações da política gerenciada original. |

**Desativar e reativar a Otimização na borda**

A função Lambda@Edge (`edgeoptimize-origin`) está associada aos eventos de solicitação de origem e resposta de origem do comportamento do CloudFront. Como ele é executado em linha em todas as solicitações que passam por esse comportamento — tanto humanas quanto automatizadas — uma interrupção do Lambda@Edge afeta todo o tráfego ativo, não apenas as solicitações agênticas. Se detectar uma interrupção no Lambda@Edge, remova imediatamente as associações de função para restaurar o fluxo de tráfego normal para sua origem padrão.

**Como detectar uma interrupção do Lambda@Edge**

* **Painel de integridade do serviço AWS**: consulte o[Painel de integridade do serviço AWS](https://health.aws.amazon.com/health/status) para verificar se há incidentes ativos que afetem o **Amazon CloudFront** ou o **AWS Lambda**. Uma interrupção global ou regional relatada aqui é a maneira mais rápida de confirmar o problema na infraestrutura da AWS, e não na sua configuração.
* **Erros do Lambda@Edge**: navegue até **Console da AWS > CloudFront > Monitoramento > [Sua distribuição]**. Abra a guia **Erros do Lambda@Edge** e verifique se há erros de execução no gráfico **Erros de execução**. Se estiverem altos, o Lambda@Edge pode estar inativo.

**Desanexar a função Lambda@Edge**

**Navegação:** Console da AWS > CloudFront > Distribuições > [Sua distribuição] > Comportamentos

1. Clique em **Editar** no comportamento.

2. Role para baixo até a seção **Associações de função**.

3. Definir as seguintes associações como **Nenhuma associação**:

   | Evento | Alterar para |
   |---|---|
   | Solicitação do visualizador | Nenhuma associação |
   | Solicitação de origem | Nenhuma associação |
   | Resposta de origem | Nenhuma associação |

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Clique em **Salvar alterações**.

5. Aguarde até que a distribuição do CloudFront conclua a implantação. O status muda de **Implantação** para a data da última modificação, normalmente dentro de alguns minutos.

Depois de implantado, todo o tráfego é roteado diretamente para sua origem padrão. Nenhuma configuração é excluída; a função Lambda e suas associações podem ser restauradas a qualquer momento.

**Reanexando a função Lambda@Edge**

**Navegação:** Console da AWS > CloudFront > Distribuições > [Sua distribuição] > Comportamentos

1. Clique em **Editar** no comportamento.

2. Role para baixo até a seção **Associações de função**.

3. Restaurar as associações:

   | Evento | Definir como |
   |---|---|
   | Solicitação do visualizador | `edgeoptimize-routing` (função do CloudFront) |
   | Solicitação de origem | Lambda com versão ARN da etapa 4 |
   | Resposta de origem | Lambda com versão ARN da etapa 4 |

   Use o **ARN da função** com versão que você anotou na etapa 4 (em **Publicar uma versão**).

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Clique em **Salvar alterações**.

5. Aguarde até que a distribuição conclua a implantação e, em seguida, verifique se as solicitações agênticas retornam o cabeçalho `x-edgeoptimize-request-id`, conforme descrito na etapa 6.

{{return-to-overview}}
