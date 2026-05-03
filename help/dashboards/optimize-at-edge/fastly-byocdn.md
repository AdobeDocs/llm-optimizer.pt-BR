---
title: Otimizar na borda – Fastly (BYOCDN)
description: Saiba como configurar o Fastly BYOCDN para a otimização na borda no LLM Optimizer.
feature: Opportunities
source-git-commit: 13d2f4bbd1f9d3886f89f80df0e76093f2afdf13
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 93%

---


# Fastly (BYOCDN)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após sua conclusão, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras do Fastly VCL, verifique se você tem:

* Acesso ao Fastly para o seu domínio.
* Uma chave da API do Edge Optimize obtida na interface do usuário do LLM Optimizer. Para obter as etapas, consulte [Recuperar suas chaves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para testar o roteamento de preparo, consulte [Chave de API de preparo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Configuração**

Adicione os três trechos de VCL a seguir ao serviço Fastly. Esses trechos lidam com solicitações agênticas de roteamento para o Edge Otimize, separação de chaves de cache e failover para a sua origem padrão.

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Adicionar snippets de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**Snippet vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;
unset req.http.x-edgeoptimize-fetcher-key; # Optional (required only in case of WAF)

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.http.x-edgeoptimize-fetcher-key = "<YOUR FETCHER KEY>"; # Optional (required only in case of WAF)
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**Snippet vcl_hash**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**Snippet vcl_deliver**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**Failover**

O trecho `vcl_deliver` trata o failover automaticamente. Se o Edge Otimize retornar um erro `4XX` ou `5XX`, a solicitação será reiniciada e roteada de volta para sua origem padrão para que o usuário final ainda receba uma resposta. As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo: 1`.

| Cenário | Comportamento |
| --- | --- |
| O Edge Otimize retorna `2XX` | A resposta otimizada é fornecida ao cliente. |
| O Edge Otimize retorna `4XX` ou `5XX` | A solicitação é reiniciada e veiculada a partir da origem padrão. |
| Resposta de failover | Inclui o cabeçalho `x-edgeoptimize-fo: 1`. |

**Permitir otimização na Edge por meio de regras de firewall (opcional)**

{{waf-allowlist-setup}}

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
