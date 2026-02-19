---
title: Otimizar na Edge - Akamai (BYOCDN)
description: Saiba como configurar o Akamai BYOCDN para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 14%

---


# Akamai (BYOCDN)

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras do Akamai Property Manager, verifique se você tem:

* Acesso ao Akamai Property Manager para o seu domínio.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Configuração**

A seguinte regra do Akamai Property Manager roteia agentes de usuário do LLM para o Edge Otimize. A configuração inclui as seguintes etapas:

**1. Definir critérios de roteamento (correspondência de usuário e agente)**

Definir roteamento para os seguintes user-agents:image.png

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![Definir critérios de roteamento](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Definir origem e comportamento do SSL**

Definir origem como `live.edgeoptimize.net` e Corresponder SAN a `*.edgeoptimize.net`

![Definir origem e comportamento do SSL](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Definir variável de chave de cache**

Definir a variável de chave de cache `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` como `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![Definir variável de chave de cache](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Regras de armazenamento em cache**

![Regras de armazenamento em cache](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modificar cabeçalhos de solicitação de entrada**

Defina os seguintes cabeçalhos de solicitação recebidos:
`x-edgeoptimize-api-key` para a chave de API recuperada de LLMO
`x-edgeoptimize-config` a `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` a `{{builtin.AK_URL}}`

![Modificar cabeçalhos de solicitação de entrada](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Modificar cabeçalhos de resposta de entrada**

![Modificar cabeçalhos de resposta de entrada](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Modificação da ID do cache**

![Modificação da ID do cache](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Modificar Cabeçalhos de Solicitação de Saída**

Definir cabeçalho `x-forwarded-host` como `{{builtin.AK_HOST}}`

![Modificar Cabeçalhos de Solicitação Enviados](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Failover de site**

A configuração de failover do site tem duas partes: o comportamento de failover (configurado na regra de roteamento principal de otimização na borda) e uma regra de cabeçalho de teste de failover separada.

**9a Comportamento de Failover de Site (dentro da regra de roteamento principal de otimização de borda)**

Dentro da regra de roteamento principal, configure o comportamento Failover do site e o trecho XML avançado da seguinte maneira:

![Failover de site](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Adicione o cabeçalho da solicitação `x-edgeoptimize-request` com o valor `fo` por meio do XML Avançado:

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

**9b Regra de Cabeçalho de Teste de Failover (regra irmã)**

>[!IMPORTANT]
>
>Crie a regra **EdgeOtimize Failover - Cabeçalho de Teste** como um **irmão** (no mesmo nível) das regras de roteamento — **não** aninhadas dentro delas. Na árvore de regras do Akamai Property Manager, a hierarquia deve ser semelhante a:
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>Isso garante que a regra de cabeçalho de teste de failover seja avaliada para **todas** regras de roteamento, não apenas uma.

Se o valor `x-edgeoptimize-request` do cabeçalho da solicitação for `fo`, defina o cabeçalho de resposta de saída `x-edgeoptimize-fo` como `true`.

![Regras de failover](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

O Site Failover garante que, se o Edge Otimize retornar um erro `4XX` ou `5XX`, a solicitação será automaticamente encaminhada de volta à origem padrão para que o usuário final ainda receba uma resposta.

| Cenário | Comportamento |
| --- | --- |
| O Edge Otimize retorna `2XX` | A resposta otimizada é fornecida ao cliente. |
| O Edge Otimize retorna `4XX` ou `5XX` | A solicitação é roteada de volta para a origem padrão. |

**Verificar a configuração**

Após concluir a configuração, verifique se o tráfego de bot está sendo roteado para o Edge Otimize e se o tráfego humano não foi afetado.

**1. Tráfego de bot de teste (deve ser otimizado)**

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

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
