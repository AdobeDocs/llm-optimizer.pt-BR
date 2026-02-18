---
title: Otimizar na Edge - CDN gerenciada pelo AEM Cloud Service (Fastly)
description: Saiba como configurar o AEM Cloud Service Managed CDN (Fastly) para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 16%

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

{{verify-setup-adobe-aem-cs-cdn}}

{{return-to-overview}}
