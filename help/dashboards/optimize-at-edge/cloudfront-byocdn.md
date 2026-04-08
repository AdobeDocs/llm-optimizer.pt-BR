---
title: Otimizar no Edge - CloudFront (BYOCDN)
description: Saiba como configurar o CloudFront BYOCDN para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: da789100d814004687de2f46e18a295671dec4b8
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 1%

---


# CloudFront (BYOCDN)

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de definir a configuração do CloudFront, verifique se você tem:

* Uma distribuição CloudFront existente que atende ao seu site.
* Permissões do AWS IAM para criar funções Lambda, funções IAM, distribuições CloudFront e políticas de cache.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.
* (Opcional) Uma chave de API de otimização do Edge de preparo se você testar o roteamento em um nome de host de preparo primeiro.

{{retrieve-byocdn-api-key}}

{{retrieve-staging-edge-optimize-api-key}}

**Etapa 1: Criar Edge Otimizar Origem**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > guia Origens

1. Clique em **Criar origem**.

2. Configure a origem:
   * **Domínio de origem:** `live.edgeoptimize.net`
   * **Nome:** `EdgeOptimize_Origin`

3. Deixe todos os outros campos com seus valores padrão.

4. Adicionar cabeçalhos personalizados:

   | Cabeçalho | Valor |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Sua chave de API |
   | `x-forwarded-host` | `www.example.com` |

   Substitua `www.example.com` pelo domínio do seu site real e `Your API key` pela chave da API Otimizada para Edge fornecida pelo seu representante da Adobe.

5. Clique em **Criar origem**.

![Criação de Origem Cloudfront](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**Etapa 2: Criar função de solicitação do visualizador**

**Navegação:** Console do AWS > CloudFront > Funções

1. Clique em **Criar função**.

2. Configurar o:
   * **Nome:** `edgeoptimize-routing`
   * **Tempo de execução:** `cloudfront-js-2.0`

3. Substitua o código padrão pelo código de [viewer-request.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/cloudfront-function/viewer-request.js).

   Antes de publicar, personalize os seguintes valores no código:

   * `YOUR_DEFAULT_ORIGIN` — Substitua com o nome de sua origem padrão existente (encontrada na guia CloudFront > Distribuições > [Sua Distribuição] > Origens).
   * `TARGETED_PATHS` — Defina como `null` para direcionar todas as páginas do HTML ou defina como uma matriz de caminhos específicos, por exemplo, `['/', '/products', '/about']`.

4. Clique em **Salvar alterações** > **Função de publicação**.

![Criação da Função Cloudfront](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**Etapa 3: configurar política de cache**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

Verifique a política de cache atualmente anexada ao seu comportamento. Clique em **Editar** sobre seu comportamento e observe a seção **Solicitações de chave de cache e origem** para identificar seu cenário:

* **Cenário A (Herdado):** Você vê um botão de opção rotulado **Configurações de cache herdadas** selecionado. Não há lista suspensa de nomes de política; em vez disso, você verá as configurações de cabeçalho e TTL em linha.
* **Cenário B (política personalizada):** Você vê a **política de cache** selecionada com um nome de política que você ou sua equipe criou (não uma política fornecida pela AWS).
* **Cenário C (Política gerenciada):** Você vê a **Política de cache** selecionada com um nome fornecido pela AWS como `CachingOptimized`, `CachingDisabled` ou `CachingOptimizedForUncompressedObjects` — eles não podem ser editados.

**Cenário A: configurações de cache herdadas**

Se seu comportamento usar configurações de cache herdadas:

1. Em **Solicitações de chave de cache e origem**, você verá **Configurações de cache herdadas** selecionadas.

2. Adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url` à lista de permissões **Headers**:

   * Selecione **Incluir os seguintes cabeçalhos** na lista suspensa.
   * Adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url`.
     ![Cache do Cloudfront Herdado](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   Se você já tiver **Todos** selecionados na lista suspensa Cabeçalhos, ignore esta etapa. Todos os cabeçalhos são automaticamente encaminhados para a origem.

3. Verifique a configuração **Cache de objetos**:

   * Se definido como **Personalizar** — é recomendável definir **TTL Mínimo** como `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.
   * Se definido como **Usar cabeçalhos de cache de origem** — nenhuma alteração será necessária.

4. Clique em **Salvar alterações**.

**Cenário B: não herdado com uma política de cache personalizada**

Se seu comportamento já usa uma política de cache personalizada (uma que você criou, não uma política gerenciada pela AWS):

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Clique em sua política atual.

2. Clique em **Editar**.

3. É recomendável definir **TTL Mínimo** como `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.
   ![Configurações TTL de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. Em **Configurações da chave de cache** > **Cabeçalhos**, junto com suas inclusões existentes, adicione `x-edgeoptimize-config` e `x-edgeoptimize-url`.
   ![Cabeçalhos de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Clique em **Salvar alterações**.

**Cenário C: não herdado com uma política de cache gerenciada (AWS)**

Se o seu comportamento usa uma política de cache gerenciada pela AWS (por exemplo, `CachingOptimized`), você não poderá editá-la. É necessário criar uma nova política de cache personalizada que replique as configurações de política gerenciada existentes e adicione os cabeçalhos de otimização do Edge.

**Parte 1: Anote as configurações atuais da política de cache gerenciado**

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Localize e clique na política de cache gerenciado atualmente anexada ao seu comportamento (por exemplo, `CachingOptimized`).

2. Anote todas as configurações existentes:
   * TTL mínimo, TTL máximo, TTL padrão
   * Cabeçalhos incluídos na chave de cache
   * Cookies incluídos na chave de cache
   * Sequências de consulta incluídas na chave do cache
   * Suporte para compactação (Gzip, Brotli)

**Parte 2: criar uma nova política de cache personalizada com as mesmas configurações + configuração de Otimização do Edge**

**Navegação:** Console do AWS > CloudFront > Políticas > Cache

1. Clique em **Criar política de cache**.

2. **Nome:** `edgeoptimize-cache`

   ![Nome da política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Replique todas as configurações indicadas na parte 1, com as seguintes modificações:

   * É recomendável definir **TTL Mínimo** como `0`. No entanto, se o TTL mínimo atual já for muito curto, talvez não seja necessário alterá-lo.

   ![Configurações TTL de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * Em **Configurações de chave de cache** > **Cabeçalhos**, inclua tudo o que a política gerenciada tinha, além de adicionar `x-edgeoptimize-config` e `x-edgeoptimize-url`.

   ![Cabeçalhos de política de cache](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Clique em **Criar**.

5. Volte para o seu comportamento e associe a política recém-criada:

   **Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

   1. Edite seu comportamento.
   2. Em **Solicitações de chave de cache e origem**, selecione **Política de cache**.
   3. Escolha `edgeoptimize-cache` na lista suspensa.
   4. Clique em **Salvar alterações**.

**Etapa 4: Criar função Lambda@Edge (solicitação e resposta de origem)**

>[!IMPORTANT]
>As funções Lambda@Edge **devem ser criadas na região `us-east-1` (N. Virgínia)**. Esse é um requisito do AWS. Mesmo que a função seja criada em `us-east-1`, o AWS a replica automaticamente em todos os locais de borda do CloudFront no mundo inteiro, para que seja executada no local de borda mais próximo do visualizador. Verifique se você está na região `us-east-1` do Console do AWS antes de continuar.

**Criar a função Lambda**

**Navegação:** Console do AWS > Lambda

1. Clique em **Criar função**.

2. Selecione **Autor do zero**.

3. Configurar o:
   * **Nome da função:** `edgeoptimize-origin`
   * Deixe todos os outros campos com seus valores padrão.

4. Clique em **Criar função**.

5. No editor de código, substitua o código padrão pelo código de [origin-request-response.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/origin-request-response.js).

6. Clique em **Implantar** para salvar o código.

7. Observe o **nome da função de execução** mostrado em **Configuração** > **Permissões** (por exemplo, `edgeoptimize-origin-role-xxxxx`). Isso é necessário nas etapas a seguir.

**Atualizar a diretiva de confiança da função de execução**

A função criada automaticamente só confia em `lambda.amazonaws.com`. Para Lambda@Edge, você também deve adicionar `edgelambda.amazonaws.com`.

**Navegação:** Console do AWS > IAM > Funções > [sua função da etapa anterior] > guia Relações de confiança

1. Clique em **Editar diretiva de confiança**.

2. Substitua a política pelo conteúdo de [trust-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/trust-policy.json).

3. Clique em **Atualizar política**.

>[!WARNING]
>A entidade de serviço `edgelambda.amazonaws.com` é **necessária** para Lambda@Edge. Sem ele, o CloudFront não pode invocar sua função em locais de borda.

**Corrigir a política de permissão de Logs do CloudWatch**

A função criada automaticamente vem com uma política `AWSLambdaBasicExecutionRole` configurada para Lambda comum, que tem a região e o nome do grupo de log incorretos para Lambda@Edge. Você precisa atualizá-la.

**Navegação:** Console do AWS > IAM > Funções > [sua função] > guia Permissões > clique no nome da política anexada (por exemplo, `AWSLambdaBasicExecutionRole-xxxx`)

1. Clique em **Editar**.

2. Substitua a política pelo conteúdo de [cloudwatch-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/cloudwatch-policy.json).

   No JSON, substitua `ACCOUNT_ID` pela ID de conta real do AWS (localizada no canto superior direito do Console do AWS) e `FUNCTION_NAME` pelo nome da função Lambda (por exemplo, `edgeoptimize-origin`).

3. Clique em **Salvar alterações**.

>[!WARNING]
>A região no ARN deve ser `*` — Lambda@Edge é executado no local de borda mais próximo do visualizador, portanto, os logs são gravados no CloudWatch na região do local de borda (por exemplo, `ap-south-1`, `eu-west-1`), não necessariamente `us-east-1`. O grupo de logs usa um nome prefixado por região: `/aws/lambda/us-east-1.FUNCTION_NAME`, onde `us-east-1` é sempre a região inicial da função.

**Publicar uma versão**

1. Na página de função, clique em **Ações** (canto superior direito) > **Publicar nova versão**.

2. Adicione uma descrição.

3. Clique em **Publicar**.
   ![Publicação Lambda](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Copie ou anote a **Função ARN** — você precisará disso na próxima etapa.
   ![Lambda ARN](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**Etapa 5: associar as funções e a política de cache ao comportamento**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

1. Edite seu comportamento.

2. Se você criou uma nova política de cache na Etapa 3 (Cenário C), defina a **Política de cache** como `edgeoptimize-cache`.
   ![Política de Cache](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. Em **Associações de função**, configure:

   * **Solicitação do visualizador:** `edgeoptimize-routing`
   * **Solicitação de origem:** Função com Versão ARN da Etapa 4 (em **Publicar uma versão**)
   * **Resposta de origem:** Função com Versão ARN da Etapa 4 (em **Publicar uma versão**)

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Clique em **Salvar alterações**.

**Etapa 6: testar a configuração**

**1. Tráfego de bot de teste (deve ser otimizado)**

Envie uma solicitação com um agente de usuário de bot agêntico. Na **primeira solicitação**, o Edge Otimize pode retornar uma resposta com proxy (não otimizada) enquanto processa e armazena em cache a página. Você pode identificar isso pelo cabeçalho `x-edgeoptimize-proxy: 1` na resposta.

Simular uma solicitação de bot de IA usando um user-agent agêntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Testar tráfego humano (NÃO deve ser afetado)**

Simular uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta deve **não** conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos a antes de habilitar a opção Otimizar no Edge.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bot (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém um ID de solicitação exclusivo | Ausente |
| `x-edgeoptimize-fo` | Presente somente se houver failover (valor: `1`) | Ausente |

**4. Domínio de preparo (opcional)**

Se você usar um nome de host de preparo e uma chave de API de preparo do LLM Optimizer, implante a mesma configuração do CloudFront na distribuição **de preparo** usando a chave de API **de preparo**. Em seguida, verifique o tráfego de bot no host de preparo:

```
curl -svo /dev/null https://staging.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Substitua `https://staging.example.com/page.html` com seu caminho e URL de preparo real. Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`.

{{verify-routing-status-in-ui}}

**5. Verificar se os logs estão fluindo corretamente**

Depois de executar as solicitações de teste acima, verifique se os logs estão sendo gravados para as funções CloudFront e Lambda@Edge.

*Logs de função do CloudFront (`edgeoptimize-routing`)*

**Navegação:** Console do AWS > CloudWatch > Grupos de logs (em `us-east-1` ou na região em que sua distribuição do CloudFront está configurada)

1. Procure um grupo de log chamado `/aws/cloudfront/function/edgeoptimize-routing`.
2. Abra o fluxo de log mais recente.
3. Para solicitações de agente, você deve ver entradas como:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. Para solicitações não agênticas, você deve ver:
   * `Routing to Default origin for userAgent: ...`

Você também pode verificar a guia **Métricas** em **Console do AWS > CloudFront > Funções > edgeotimize-routing** para exibir as contagens de invocação e as taxas de erro.

*Logs do Lambda@Edge (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Os logs Lambda@Edge são gravados no CloudWatch na **região do local da borda** que atendeu à solicitação, não `us-east-1`. Verifique o CloudWatch na região do AWS mais próxima de onde você executou o comando curl.

**Navegação:** Console do AWS > CloudWatch > Grupos de logs (verifique se você está na região correta)

1. Procure um grupo de log chamado `/aws/lambda/us-east-1.edgeoptimize-origin`.
2. Abra o fluxo de log mais recente.
3. Para solicitações de agente, você deve ver entradas como:
   * `Calling Edge Optimize Origin for agentic requests` — caminho principal
   * `Calling Default Origin in case of failover for agentic requests` — caminho de failover
   * `Failover Triggered for agentic requests` — detecção de failover de origem-resposta

Se o grupo de logs não estiver presente, verifique se as permissões do IAM foram atualizadas corretamente na Etapa 4. Verifique também outras regiões próximas do AWS — o local da borda que atendeu à sua solicitação pode ser diferente do esperado.

**Resolução de Problemas**

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| Nenhuma `x-edgeoptimize-request-id` em resposta a solicitações de agente | O grupo de origem não é roteado para o Edge Otimize | Verifique se `YOUR_DEFAULT_ORIGIN` foi substituído corretamente no código de função CloudFront (Etapa 2). |
| erros 403 em solicitações de agente | Chave de API inválida ou ausente | Verifique o valor do cabeçalho `x-edgeoptimize-api-key` nos cabeçalhos personalizados de origem de Otimização do Edge (Etapa 1). |
| Não é possível encontrar logs do CloudWatch para Lambda@Edge | Permissões de IAM incorretas | Verifique se a política de permissão de logs do CloudWatch foi atualizada (Etapa 4). Observação: os logs do Lambda@Edge aparecem na região de borda que atendeu à solicitação, não necessariamente `us-east-1`. |
| Cache não respeitando `cache-control: no-store` | O TTL mínimo pode ser muito alto | Defina o TTL mínimo como `0` na sua política de cache (Etapa 3). Se o TTL mínimo já for muito curto, talvez esse não seja o problema. |
| Tráfego regular (não agente) interrompido após a configuração | Erro de configuração da política de cache | Se você criou uma nova política de cache (Cenário C), certifique-se de ter replicado todas as configurações da política gerenciada original. |

**Desabilitando e reabilitando a opção Otimizar no Edge**

A função Lambda@Edge (`edgeoptimize-origin`) está associada aos eventos de resposta de origem e solicitação de origem do seu comportamento do CloudFront. Como é executado em linha em cada solicitação que passa por esse comportamento, seja humano ou prático, uma interrupção do Lambda@Edge afetará todo o tráfego ativo, não apenas solicitações críticas. Se você detectar uma interrupção do Lambda@Edge, remova as associações de função imediatamente para restaurar o fluxo de tráfego normal para sua origem padrão.

**Como detectar uma interrupção do Lambda@Edge**

* **Painel de Integridade do Serviço AWS** — Verifique no [Painel de Integridade do Serviço AWS](https://health.aws.amazon.com/health/status) se há incidentes ativos que afetem o **Amazon CloudFront** ou o **AWS Lambda**. Uma interrupção global ou regional relatada aqui é a maneira mais rápida de confirmar o problema na infraestrutura da AWS, e não na sua configuração.
* **Erros de Lambda@Edge** — Navegue até **Console do AWS > CloudFront > Monitoramento > [Sua Distribuição]**. Abra a guia **Lambda@Edge errors** e verifique se há erros de execução no gráfico **Execution errors**. Se estiverem altos, Lambda@Edge pode estar inativo.

**Desanexando a função Lambda@Edge**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

1. Clique em **Editar** sobre o seu comportamento.

2. Role para baixo até a seção **Associações de função**.

3. Definir as seguintes associações como **Nenhuma associação**:

   | Evento | Alterar para |
   |---|---|
   | Solicitação do visualizador | Nenhuma associação |
   | Solicitação de origem | Nenhuma associação |
   | Resposta de origem | Nenhuma associação |

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Clique em **Salvar alterações**.

5. Aguarde até que a distribuição CloudFront conclua a implantação. O status muda de **Implantação** para a data da última modificação, normalmente dentro de alguns minutos.

Depois de implantado, todo o tráfego é roteado diretamente para sua origem padrão. Nenhuma configuração é excluída; a função Lambda e suas associações podem ser restauradas a qualquer momento.

**Reanexando a função Lambda@Edge**

**Navegação:** Console do AWS > CloudFront > Distribuições > [Sua Distribuição] > Comportamentos

1. Clique em **Editar** sobre o seu comportamento.

2. Role para baixo até a seção **Associações de função**.

3. Restaurar as associações:

   | Evento | Defina como |
   |---|---|
   | Solicitação do visualizador | `edgeoptimize-routing` (função CloudFront) |
   | Solicitação de origem | Versão do ARN Lambda do passo 4 |
   | Resposta de origem | Versão do ARN Lambda do passo 4 |

   Use a **Função ARN** com versão anotada na Etapa 4 (em **Publicar uma versão**).

   ![Configuração de associações de função](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Clique em **Salvar alterações**.

5. Aguarde a implantação da distribuição ser concluída e, em seguida, verifique se as solicitações de agente retornam o cabeçalho `x-edgeoptimize-request-id` conforme descrito na Etapa 6.

{{return-to-overview}}
