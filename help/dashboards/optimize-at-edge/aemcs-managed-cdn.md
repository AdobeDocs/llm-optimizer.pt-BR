---
title: Otimizar na Edge - CDN gerenciada pelo AEM Cloud Service (Fastly)
description: Saiba como configurar o AEM Cloud Service Managed CDN (Fastly) para Otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 0c7ccadbb40c8c119cb2a57cf8118708c33c4236
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 12%

---


# CDN gerenciada do AEM Cloud Service (Fastly)

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Para começar a rotear o tráfego de agente para o Edge Otimize:

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Marque a caixa de seleção **Habilitar mecanismo de otimização**.

   ![Implantar otimizações em agentes de IA — pendente](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. No diálogo de confirmação, selecione **Habilitar**. A equipe do Adobe cuidará da configuração de roteamento em seu nome.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

   Quando o roteamento estiver configurado e ativo, o status será atualizado para **Concluído** com uma marca de seleção verde confirmando que o roteamento está habilitado. Nenhuma outra ação é necessária da sua parte.

   ![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

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

**4. Verificar status do roteamento no LLM Optimizer**

Você também pode confirmar o roteamento na interface do LLM Optimizer. Abra a **Configuração do cliente** e selecione a guia **Configuração de CDN**. Quando o roteamento está ativo, a seção **Implantar otimizações em agentes de IA** exibe **Concluído**.

![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
