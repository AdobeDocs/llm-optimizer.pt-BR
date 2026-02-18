---
title: Otimizar na Edge - Akamai (BYOCDN)
description: Saiba como configurar o Akamai BYOCDN para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 26%

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

![Failover de site](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![Comportamentos de failover](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![Regras de failover](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

O Site Failover garante que, se o Edge Otimize retornar um erro `4XX` ou `5XX`, a solicitação será automaticamente encaminhada de volta à origem padrão para que o usuário final ainda receba uma resposta.

| Cenário | Comportamento |
| --- | --- |
| O Edge Otimize retorna `2XX` | A resposta otimizada é fornecida ao cliente. |
| O Edge Otimize retorna `4XX` ou `5XX` | A solicitação é roteada de volta para a origem padrão. |

{{verify-setup-byocdn}}

{{return-to-overview}}
