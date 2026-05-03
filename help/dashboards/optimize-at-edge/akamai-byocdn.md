---
title: Otimizar na borda – Akamai (BYOCDN)
description: Saiba como configurar o Akamai BYOCDN para a otimização na borda no LLM Optimizer.
feature: Opportunities
source-git-commit: 13d2f4bbd1f9d3886f89f80df0e76093f2afdf13
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 61%

---


# Akamai (BYOCDN)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após sua conclusão, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras do Akamai Property Manager, verifique se você tem:

* Acesso ao Akamai Property Manager para o seu domínio.
* Uma chave da API do Edge Optimize obtida na interface do usuário do LLM Optimizer. Para obter as etapas, consulte [Recuperar suas chaves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para testar o roteamento de preparo, consulte [Chave de API de preparo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Configuração**

A seguinte regra do Akamai Property Manager roteia o tráfego de página de HTML para o Edge Otimize. A configuração inclui as seguintes etapas:

**1. Definir critérios de roteamento (correspondência de tráfego de usuário-agente e HTML)**

Defina o roteamento para os seguintes agentes do usuário:

```
 *AdobeEdgeOptimize-AI*
 *ChatGPT-User*
 *GPTBot*
 *OAI-SearchBot*
 *PerplexityBot*
 *Perplexity-User*
```

>[!NOTE]
>
>Aplique a regra de roteamento Otimizar no Edge somente ao tráfego de página agêntico do HTML. Uma configuração comum é usar os critérios do lado da solicitação, como **Extensão de arquivo**, para corresponder a `html` e `EMPTY_STRING` para URLs de página sem extensão. Se o site serve o HTML a partir de outros padrões de URL, ou inclui rotas não relacionadas à página sem extensão, como endpoints de API, refine a regra com critérios adicionais baseados em caminho.

![Definir critérios de roteamento](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Definir origem e comportamento do SSL**

Definir origem como `live.edgeoptimize.net` e Corresponder SAN a `*.edgeoptimize.net`

>[!NOTE]
>
>Se a ativação de propriedades falhar depois de adicionar a regra Otimizar no Edge, verifique se a regra usa um modo de verificação SSL do Servidor de Origem diferente da regra padrão. Se isso acontecer, atualize a regra Otimizar no Edge para corresponder à regra padrão. Por exemplo, se a regra padrão usa **Configurações de plataforma**, use **Configurações de plataforma** aqui também. Se não conseguir usar a configuração necessária, entre em contato com o suporte da Akamai.

![Definir origem e comportamento do SSL](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Definir variável de chave de cache**

Defina a variável de chave de cache `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` como `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![Definir variável de chave de cache](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Regras de armazenamento em cache**

![Regras de armazenamento em cache](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modificar cabeçalhos de solicitação de entrada**

Defina os seguintes cabeçalhos de solicitação recebidos:
`x-edgeoptimize-api-key` para a chave de API recuperada de LLMO
`x-edgeoptimize-config` para `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` a `{{builtin.AK_URL}}`

![Modificar cabeçalhos de solicitação de entrada](/help/assets/optimize-at-edge/akamai-step5-request.png)

**Permitir otimização na Edge por meio de regras de firewall (opcional)**

{{waf-allowlist-setup}}

![Definir cabeçalho x-edgeotimize-fetcher-key no Gerenciador de Propriedades](/help/assets/optimize-at-edge/akamai-step10-fetcher-key.png)

>[!NOTE]
>
>Inclua na lista de permissões também o agente de usuário `*AdobeEdgeOptimize/1.0*` e o cabeçalho `x-edgeoptimize-fetcher-key` no Akamai Bot Manager.

**6. Modificar cabeçalhos de resposta de entrada**

![Modificar cabeçalhos de resposta de entrada](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Modificação da ID do cache**

![Modificação da ID do cache](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modificar cabeçalhos de solicitações enviadas**

Definir cabeçalho `x-forwarded-host` como `{{builtin.AK_HOST}}`

![Modificar cabeçalhos de solicitações de saída](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Failover de site**

A configuração de failover do site tem duas partes: o comportamento de failover (configurado dentro da regra principal de roteamento da otimização-na-borda) e uma regra separada de cabeçalho de teste de failover.

**9a. Comportamento de failover do site (dentro da regra principal de roteamento da otimização-na-borda)**

Dentro da regra de roteamento principal, configure o comportamento de failover do site e o trecho XML avançado da seguinte maneira:

>[!IMPORTANT]
>
>O trecho XML nesta etapa requer o comportamento **Avançado**. Em alguns ambientes do Akamai, esse comportamento não está disponível para edição de autoatendimento. Se você não vir a opção **Avançado**, entre em contato com a equipe de conta do Akamai ou com o suporte do Akamai para habilitar a configuração necessária.

![Failover de site](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Adicione o cabeçalho da solicitação `x-edgeoptimize-request` com o valor `fo` por meio de XML avançado:

```
<forward:availability.fail-action2>
<add-header>
<status>on</status>
<name>x-edgeoptimize-request</name>
<value>fo</value>
</add-header>
</forward:availability.fail-action2>
```

![Comportamentos de failover](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

**9b. Regra de cabeçalho de teste de failover (regra irmã)**

>[!IMPORTANT]
>
>Crie a regra **EdgeOtimize Failover – Cabeçalho de Teste** como uma **irmã** (no mesmo nível) das regras de roteamento — **não** aninhadas dentro delas. Na árvore de regras do Akamai Property Manager, a hierarquia deve ser semelhante a:
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>Isso garante que a regra de cabeçalho de teste de failover seja avaliada para **todas** as regras de roteamento, e não apenas para uma.
>
>Além disso, certifique-se de que a regra **Otimizar no Edge Routing** não seja substituída por nenhuma regra correspondente posterior que altere a origem, o comportamento de cache ou a ID do cache para as mesmas solicitações. Se outra regra de correspondência redefinir esses comportamentos, Otimizar no roteamento ou cache do Edge pode não funcionar conforme esperado.

Se o valor `x-edgeoptimize-request` do cabeçalho da solicitação for `fo`, defina o cabeçalho de resposta de saída `x-edgeoptimize-fo` como `true`.

![Regras de failover](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

O failover do site garante que, se o Edge Optimize retornar um erro `4XX` ou `5XX`, a solicitação será automaticamente direcionada de volta para sua origem padrão para que o usuário final ainda receba uma resposta.

| Cenário | Comportamento |
| --- | --- |
| O Edge Otimize retorna `2XX` | A resposta otimizada é fornecida ao cliente. |
| O Edge Otimize retorna `4XX` ou `5XX` | A solicitação é roteada de volta para a origem padrão. |

**Verificar a configuração**

Após concluir a configuração, verifique se o tráfego de bots está sendo roteado para o Edge Optimize e se o tráfego humano permanece inalterado.

**1. Tráfego de bots de teste (deve ser otimizado)**

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

{{return-to-overview}}
