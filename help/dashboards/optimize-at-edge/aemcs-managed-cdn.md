---
title: Otimizar na Edge - CDN gerenciada pelo AEM Cloud Service (Fastly)
description: Saiba como configurar o AEM Cloud Service Managed CDN (Fastly) para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 12%

---


# CDN gerenciada do AEM Cloud Service (Fastly)

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Para começar a rotear o tráfego de agente para o Edge Otimize:

1. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Em **Roteamento de tráfego de IA para Implantar Otimizações**, marque a caixa de seleção **Implantar Otimizações em Agentes de IA**. A equipe do Adobe cuidará da configuração de roteamento em seu nome.

   ![Otimizações de Implantação de Tarefa para Agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Após ativar a caixa de seleção, o status mostrará que a configuração está em andamento. A equipe do Adobe concluirá a configuração de roteamento para você.

   ![Configuração de Roteamento de Tráfego de IA em andamento](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   Quando o roteamento estiver configurado e ativo, o status será atualizado para mostrar uma marca de seleção verde indicando que o roteamento foi ativado com êxito. Nenhuma outra ação é necessária da sua parte.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

**Roteamento de autoatendimento por meio do Cloud Manager Pipeline**

Se preferir configurar o roteamento por conta própria no Cloud Manager Pipeline, siga as etapas abaixo. A configuração de roteamento é feita por meio de uma [regra de CDN originSelector](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). Os pré-requisitos são os seguintes:

* Decida o domínio a ser roteado.
* Decida os caminhos a serem roteados.
* Decidir os agentes do usuário que serão roteados (regex recomendado).

Para implantar a regra, é necessário:

* Criar um [pipeline de configuração](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/config-pipeline).
* Confirme o arquivo de configuração `cdn.yaml` no repositório.
* Execute o pipeline de configuração.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"
```

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

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

{{return-to-overview}}
