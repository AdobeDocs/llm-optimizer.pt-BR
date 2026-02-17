---
title: Otimizar na borda
description: Saiba como fornecer otimizações na borda da CDN, no LLM Optimizer, sem precisar fazer alterações de criação.
feature: Opportunities
source-git-commit: ae37ef578f279eae6ea51fd8aed5c6b91c8e1088
workflow-type: tm+mt
source-wordcount: '4843'
ht-degree: 45%

---


# Otimizar na borda

Esta página oferece uma visão geral detalhada sobre como fornecer otimizações na borda da CDN sem realizar alterações de criação. Ela aborda o processo de integração, as oportunidades de otimização disponíveis e como otimizar automaticamente na borda.

>[!NOTE]
>Essa funcionalidade está atualmente em disponibilidade antecipada. Saiba mais sobre os programas de acesso antecipado [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## O que é a otimização na borda?

A otimização na borda é um recurso de implantação baseada na borda no LLM Optimizer que envia alterações com linguagem de IA a agentes de usuário do LLM. No contexto atual, “borda” significa que a otimização é aplicada na camada da CDN. Como ela fornece otimizações na camada da CDN, não são necessárias alterações de criação no Sistema de gerenciamento de conteúdo (CMS), portanto, o CMS de origem permanece inalterado. Essa separação permite melhorar a visibilidade do LLM sem alterar os fluxos de trabalho de publicação existentes. Ele direciona apenas o tráfego agêntico e não afeta usuários humanos nem bots de SEO. Quando o LLM Optimizer detecta oportunidades para otimizar uma página, os usuários podem implantar correções diretamente na borda da CDN.

Otimizar na borda é uma alternativa mais rápida e simples para as correções tradicionais que exigem esforços complexos de engenharia. Como mencionado, após concluir uma configuração única, não são necessárias alterações na plataforma ou ciclos de desenvolvimento longos para aplicar as alterações. É possível publicar melhorias em minutos sem exigir o envolvimento do desenvolvedor. É uma maneira de otimizar o site para agentes de IA sem adição de código.

A otimização na borda foi projetada para usuários empresariais em equipes de marketing, SEO, conteúdo e estratégia digital. Ela permite que os usuários empresariais concluam a jornada completa no LLM Optimizer por: identificar oportunidades, compreender sugestões e implantar facilmente as correções. Com a Otimização na borda, usuários podem visualizar as alterações, implantá-las rapidamente na borda da CDN e confirmar se as otimizações estão ativas. O desempenho pode ser monitorado no ecossistema do LLM Optimizer.

### Principais benefícios

* **Entrega somente para IA:** oferece HTML otimizado somente para agentes de IA, sem impacto para visitantes humanos ou bots de SEO.
* **Ciclos mais rápidos:** publique alterações em minutos, não em semanas. Não são necessárias alterações na plataforma nem longos ciclos de engenharia.
* **Reversível:** compatível com um recurso de reversão de um clique que pode reverter a página em minutos.
* **Nenhum impacto no desempenho:** as otimizações baseadas na borda e o armazenamento em cache não afetam a latência do site.
* **Independente da CDN e do CMS:** funciona com qualquer configuração de CDN e de front-end, independentemente do sistema de gerenciamento de conteúdo.

### Quais oportunidades são compatíveis com a Otimização na borda?

Algumas oportunidades que podem melhorar a experiência agêntica na web são compatíveis com a Otimização na borda. Saiba mais sobre cada oportunidade na página [Painel de oportunidades](/help/dashboards/opportunities.md) e na seção de oportunidades da página atual.

## Integração

Entre em contato com a equipe de contas da Adobe ou com a equipe do FDE para iniciar o processo de integração. Sua equipe de TI ou CDN também é necessária para concluir os pré-requisitos e o processo de configuração. Além disso, também é possível entrar em contato com `llmo-at-edge@adobe.com` para obter maior assistência na integração.

Pré-requisitos para a integração à Otimização na borda:

* Conclua o processo de integração com o LLM Optimizer.
* Conclua o processo de encaminhamento de logs da CDN.

Requisitos para a equipe de TI/CDN:
* Adicione o agente-usuário `*AdobeEdgeOptimize/1.0*` ao Incluo na lista de permissões no arquivo robots.txt do site ou nas regras de gerenciamento de tráfego de bot.
* Verifique se as páginas não estão bloqueadas no nível de domínio ou da CDN.
* Adicionar regras de roteamento para o recurso Otimização na borda da CDN.
* Confirme o roteamento do recurso Otimização na borda na interface do LLM Optimizer.

Para orientar o processo de configuração, veja abaixo exemplos de configurações para várias definições de CDN. Lembre-se de que esses exemplos devem ser adaptados à sua configuração atualmente ativa. Recomendamos aplicar as alterações nos ambientes inferiores primeiro.

>[!BEGINTABS]

>[!TAB CDN gerenciada pelo AEM Cloud Service (Fastly)]

**Otimização do Edge - CDN gerenciada do AEM Cloud Service (Fastly)**

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

Para testar a configuração, execute um curl e espere o seguinte:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

>[!TAB Fastly (BYOCDN)]

**Otimização do Edge - Fastly (BYOCDN)**

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras do Fastly VCL, verifique se você tem:

* Acesso ao Fastly no seu domínio.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.

**Etapas para recuperar sua chave de API:**

1. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Em **Roteamento de tráfego de IA para Implantar Otimizações**, marque a caixa de seleção **Implantar Otimizações em Agentes de IA**.

   ![Otimizações de Implantação de Tarefa para Agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie a chave da API e prossiga com as etapas de configuração de roteamento abaixo.

   ![Copiar a chave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >Nesse estágio, o status pode mostrar uma cruz vermelha indicando que a configuração ainda não foi concluída. Isso é esperado — quando você concluir a configuração de roteamento abaixo e o tráfego de bot de IA começar a fluir, o status será atualizado para uma marca de seleção verde confirmando que o roteamento foi ativado com êxito.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

**Configuração**

Adicione os três trechos de VCL a seguir ao serviço Fastly. Esses snippets lidam com solicitações de agente de roteamento para o Edge Otimize, separação de chaves de cache e failover para sua origem padrão.

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Adicionar snippets de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**Snippet vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
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

**Verificar a configuração**

Para testar a configuração, execute um curl e espere o seguinte:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Akamai (BYOCDN)]

**Otimização do Edge - Akamai (BYOCDN)**

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras do Akamai Property Manager, verifique se você tem:

* Acesso ao Akamai Property Manager para o seu domínio.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.

**Etapas para recuperar sua chave de API:**

1. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Em **Roteamento de tráfego de IA para Implantar Otimizações**, marque a caixa de seleção **Implantar Otimizações em Agentes de IA**.

   ![Otimizações de Implantação de Tarefa para Agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie a chave da API e prossiga com as etapas de configuração de roteamento abaixo.

   ![Copiar a chave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >Nesse estágio, o status pode mostrar uma cruz vermelha indicando que a configuração ainda não foi concluída. Isso é esperado — quando você concluir a configuração de roteamento abaixo e o tráfego de bot de IA começar a fluir, o status será atualizado para uma marca de seleção verde confirmando que o roteamento foi ativado com êxito.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

**Configuração**

A seguinte regra do Akamai Property Manager roteia agentes de usuário do LLM para o Edge Otimize. A configuração inclui as seguintes etapas:

**1. Definir critérios de roteamento (correspondência de usuário e agente)**

Defina o roteamento para os seguintes user-agents:

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

**Verificar a configuração**

Para testar a configuração, execute um curl e espere o seguinte:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Cloudflare (BYOCDN)]

**Otimização do Edge - Cloudflare (BYOCDN)**

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras de roteamento do Cloud Worker, verifique se você:

* Uma conta CloudFlare com Workers ativados em seu domínio.
* Acesso às configurações de DNS do seu domínio no Cloud Flare.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.

**Etapas para recuperar sua chave de API:**

1. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Em **Roteamento de tráfego de IA para Implantar Otimizações**, marque a caixa de seleção **Implantar Otimizações em Agentes de IA**.

   ![Otimizações de Implantação de Tarefa para Agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie a chave da API e prossiga com as etapas de configuração de roteamento abaixo.

   ![Copiar a chave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >Nesse estágio, o status pode mostrar uma cruz vermelha indicando que a configuração ainda não foi concluída. Isso é esperado — quando você concluir a configuração de roteamento abaixo e o tráfego de bot de IA começar a fluir, o status será atualizado para uma marca de seleção verde confirmando que o roteamento foi ativado com êxito.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

**Como funciona o roteamento**

Quando configurada corretamente, uma solicitação para o seu domínio (por exemplo, `www.example.com/page.html`) de um agente de usuário agente é interceptada pelo Cloud Worker e roteada para o back-end do Edge Otimize. A solicitação de backend inclui os cabeçalhos necessários.

**Testando a solicitação de back-end**

Você pode verificar o roteamento fazendo uma solicitação direta para o back-end do Edge Otimize.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Cabeçalhos obrigatórios**

Os seguintes cabeçalhos devem ser definidos nas solicitações para o back-end do Edge Otimize:

| Cabeçalho | Descrição | Exemplo |
|--------|-------------|---------|
| `x-forwarded-host` | O host original da solicitação. Obrigatório para identificar o domínio do site. | `www.example.com` |
| `x-edgeoptimize-url` | O caminho do URL original e a sequência de consulta da solicitação. | `/page.html` ou `/products?id=123` |
| `x-edgeoptimize-api-key` | A chave de API fornecida pela Adobe para o seu domínio. | `your-api-key-here` |
| `x-edgeoptimize-config` | String de configuração para diferenciação da chave de cache. | `LLMCLIENT=TRUE;` |

**Etapa 1: Criar o Trabalho da Cloudflare**

1. Faça logon no painel do Cloud.
2. Navegue até **Trabalhadores e páginas** na barra lateral.
3. Clique em **Criar aplicativo** e depois em **Criar Trabalhador**.
4. Nomeie seu trabalhador (por exemplo, `edge-optimize-router`).
5. Clique em **Implantar** para criar o trabalhador com o código padrão.

![Painel de Trabalhadores em Nuvem](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Etapa 2: adicionar o código do Trabalhador**

Depois de criar o trabalhador, clique em **Editar código** e substitua o código padrão pelo seguinte:

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Clique em **Salvar e implantar** para publicar o trabalhador.

![Editor de código do Cloud Worker](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Etapa 3: configurar variáveis de ambiente**

As variáveis de ambiente armazenam configurações confidenciais como sua chave de API com segurança.

1. Nas configurações do seu trabalhador, navegue até **Configurações** > **Variáveis**.
2. Em **Variáveis de Ambiente**, clique em **Adicionar variável**.
3. Adicione as seguintes variáveis:

   | Nome da variável | Descrição | Obrigatório |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Sua chave de API de otimização Edge fornecida pela Adobe. | Sim |
   | `EDGE_OPTIMIZE_TARGET_HOST` | O host de destino para as solicitações de Otimização do Edge (enviadas como cabeçalho `x-forwarded-host`) e o domínio de origem para failover. Deve ser somente o domínio sem protocolo (por exemplo, `www.example.com`, não `https://www.example.com`). | Sim |

4. Para a chave de API, clique em **Criptografar** para armazená-la com segurança.
5. Clique em **Salvar e implantar**.

![Variáveis de ambiente de nuvem](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Etapa 4: adicionar uma rota ao seu domínio**

Para ativar o worker no seu domínio:

1. Vá para as **Configurações** > **Acionadores** do seu trabalhador.
2. Em **Rotas**, clique em **Adicionar rota**.
3. Insira seu padrão de domínio (por exemplo, `www.example.com/*` ou `example.com/*`).
4. Selecione sua zona na lista suspensa.
5. Clique em **Salvar**.

Como alternativa, você pode configurar rotas no nível da zona:

1. Navegue até o domínio no Cloud Flare.
2. Vá para **Rotas dos Trabalhadores**.
3. Clique em **Adicionar rota** e especifique o padrão e o trabalhador.

![Rotas de Trabalho da Cloudflare](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Etapa 5: verificar a configuração**

Após a implantação, teste a configuração fazendo uma solicitação com um agente de usuário agenciador.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

Você também pode verificar se o tráfego normal continua a funcionar:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0"
```

Esta solicitação deve ser servida de sua origem sem o cabeçalho `x-edgeoptimize-request-id`.

**Verificando o comportamento de failover**

Se o Edge Otimize estiver indisponível ou retornar um erro, o worker efetuará automaticamente o failover para sua origem. As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo`:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Você pode monitorar eventos de failover nos logs do Cloud Workers para solucionar problemas.

**Entendendo a lógica do Worker**

O Cloud Worker implementa a seguinte lógica:

1. **Detecção do Agente do Usuário:** verifica se o agente do usuário da solicitação recebida corresponde a qualquer um dos bots de agente definidos (não diferencia maiúsculas de minúsculas).

2. **Direcionamento de caminho:** filtra opcionalmente solicitações com base em caminhos direcionados. Por padrão, todas as páginas do HTML (URLs terminadas com `/`, sem extensão ou `.html`) são roteadas. Você pode especificar caminhos específicos usando a matriz `TARGETED_PATHS`.

3. **Proteção de loop:** O cabeçalho `x-edgeoptimize-request` impede loops infinitos. Quando o Edge Otimize faz solicitações de volta à sua origem, esse cabeçalho é definido como `"1"` e o trabalhador transmite a solicitação sem roteá-la de volta para o Edge Otimize.

4. **Segurança de cabeçalho:** Antes de configurar cabeçalhos Edge Otimize, o trabalhador remove todos os cabeçalhos `x-edgeoptimize-*` existentes da solicitação de entrada para evitar ataques de injeção de cabeçalho.

5. **Mapeamento de cabeçalho:** o trabalhador define os cabeçalhos necessários para a Otimização Edge:
   * `x-forwarded-host` - Identifica o domínio do site original.
   * `x-edgeoptimize-url` - Preserva o caminho da solicitação original e a sequência de consulta.
   * `x-edgeoptimize-api-key` - Autentica a solicitação com o Otimize do Edge.
   * `x-edgeoptimize-config` - Fornece a configuração da chave de cache.

6. **Lógica de failover:** se o Edge Otimize retornar qualquer código de status de erro (erros de cliente 4XX ou erros de servidor 5XX) ou a solicitação falhar devido a um erro de rede, o trabalhador efetuará automaticamente o failover para sua origem usando `EDGE_OPTIMIZE_TARGET_HOST`. A resposta de failover inclui o cabeçalho `x-edgeoptimize-fo: 1` para indicar que o failover ocorreu.

7. **Tratamento de redirecionamento:** a opção `redirect: "manual"` garante que as respostas de redirecionamento do Edge Otimize sejam passadas para o cliente sem que o trabalhador as siga.

**Personalizando a configuração**

Você pode personalizar o comportamento do trabalhador modificando as constantes de configuração na parte superior do código:

**Lista de bots de agente**

Modifique a matriz `AGENTIC_BOTS` para adicionar ou remover agentes do usuário:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**Caminhos direcionados**

Por padrão, todas as páginas do HTML são roteadas para o Edge Otimize. Para limitar o roteamento a caminhos específicos, modifique a matriz `TARGETED_PATHS`:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**Configuração de failover**

Por padrão, o trabalhador falha em qualquer erro 4XX ou 5XX do Edge Otimize. Personalizar este comportamento:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Considerações importantes**

* **Comportamento de failover:** o trabalhador executará automaticamente o failover de sua origem se o Edge Otimize retornar qualquer erro (códigos de status 4XX ou 5XX) ou se a solicitação falhar devido a um erro de rede. O failover usa `EDGE_OPTIMIZE_TARGET_HOST` como o domínio de origem (semelhante ao `F_Default_Origin` do Fastly ou ao `Default_Origin` do CloudFront). As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo: 1`, que pode ser usado para monitoramento e depuração.

* **Armazenamento em cache:** o Cloud Flare armazena em cache as respostas com base na URL por padrão. Como o tráfego de agente recebe conteúdo diferente do tráfego humano, certifique-se de que a configuração de cache tenha em conta isso. Considere usar a API de cache ou cabeçalhos de cache para diferenciar o conteúdo em cache. O cabeçalho `x-edgeoptimize-config` deve ser incluído na sua chave de cache.

* **Limitação de taxa:** monitore seu uso do Edge Otimize e considere implementar a limitação de taxa para tráfego de agente, se necessário.

* **Testando:** sempre teste a configuração em um ambiente de preparo antes de implantar em produção. Verifique se o tráfego de agentes e humanos se comportam conforme esperado. Teste o comportamento de failover simulando erros de Otimização do Edge.

* **Logs:** Habilite o log de Trabalhadores em Nuvem para monitorar solicitações e solucionar problemas. Navegue até **Workers** > **seu worker** > **Logs** para exibir os logs em tempo real. O trabalhador registra eventos de failover para fins de depuração.

**Resolução de Problemas**

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| Nenhum cabeçalho `x-edgeoptimize-request-id` na resposta | A rota do trabalhador não corresponde ou o agente de usuário não está na lista de bots de agente. | Verifique se o padrão de rota corresponde ao URL da solicitação. Verifique se o agente do usuário está na matriz `AGENTIC_BOTS`. |
| Erros 401 ou 403 do Edge Otimize | Chave de API inválida ou ausente. | Verifique se `EDGE_OPTIMIZE_API_KEY` está definido corretamente nas variáveis de ambiente. Entre em contato com a Adobe para confirmar se a chave de API está ativa. |
| Redirecionamentos ou loops infinitos | O cabeçalho de proteção contra loop não está sendo definido ou foi verificado corretamente. | Verifique se a verificação do cabeçalho `x-edgeoptimize-request` está em vigor. |
| Tráfego humano afetado | A lógica de roteamento do trabalhador é muito ampla. | Verifique se a lógica de correspondência do agente do usuário está correta e não diferencia maiúsculas de minúsculas. Verifique se `TARGETED_PATHS` está configurado corretamente. |
| Tempos de resposta lentos | Latência de rede para o back-end de Otimização do Edge. | Isso é esperado para a primeira solicitação; as solicitações subsequentes são armazenadas em cache no Edge Otimize. |
| Cabeçalho `x-edgeoptimize-fo: 1` na resposta | O Edge Otimize retornou um erro e ocorreu failover para a origem. | Verifique os logs do Cloud Workers para obter o código de erro específico. Verifique o status do serviço de Otimização do Edge com o Adobe. |
| O failover não está funcionando | Sinalizadores de failover desabilitados ou erro na lógica de failover. | Verificar se `FAILOVER_ON_4XX` e `FAILOVER_ON_5XX` estão definidos como `true`. Verifique se há mensagens de erro nos logs do trabalhador. |
| Determinados caminhos não estão sendo otimizados | Caminho não correspondente aos caminhos direcionados ou ao padrão de página do HTML. | Verifique se o caminho está em `TARGETED_PATHS` (se especificado) e corresponde ao padrão regex da página do HTML. |
| Solicitações que falham com host inválido | `EDGE_OPTIMIZE_TARGET_HOST` inclui o protocolo (por exemplo, `https://`). | Use apenas o nome de domínio sem protocolo (por exemplo, `example.com`, não `https://example.com`). |
| Erro 530 durante failover | A nuvem não pode se conectar à origem ou a solicitação de failover tem cabeçalhos inválidos. | Certifique-se de que a função de failover remova os cabeçalhos Edge Otimize. Verifique se a origem está acessível e se o DNS está configurado corretamente. |

>[!ENDTABS]

>[!NOTE]
>No caso de outros provedores de CDN, entre em contato com `llmo-at-edge@adobe.com` para auxiliar suas equipes de TI/CDN com a integração. Após a conclusão das configurações, você poderá enviar sugestões para o recurso Otimização na borda no LLM Optimizer.

## Oportunidades

A tabela a seguir apresenta oportunidades que podem melhorar a experiência agêntica na web e que são compatíveis com o recurso Otimização na borda.

| Oportunidade | Tipo | Identificação automática | Sugestão automática | Otimizar automaticamente |
|---------|----------|----------|----------|----------|
| Recuperar visibilidade do conteúdo | GEO técnico | Detecta páginas em que o conteúdo crítico não está visível para agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Realça o conteúdo que pode ser disponibilizado para agentes de IA e recomenda habilitar a pré-renderização para essas páginas. | Disponibiliza um instantâneo do HTML totalmente renderizado e compatível com IA para tráfego agêntico que recupera o conteúdo oculto anteriormente. |
| Otimizar cabeçalhos para LLMs | Otimização de conteúdo | Detecta cabeçalhos em branco, duplicados, ausentes ou ambíguos que podem reduzir a legibilidade da máquina. | Propõe uma hierarquia de cabeçalho mais limpa e rótulos aprimorados, além de mostrar uma visualização da estrutura atualizada para cada página. | Injeta a estrutura de cabeçalho aprimorada para agentes de IA, preservando seu design visual e tornando a página mais legível para LLMs. |
| Adicionar resumos compatíveis com LLM | Otimização de conteúdo | Identifica páginas longas ou complexas que não têm resumos concisos no nível da página ou da seção, dificultando a rápida análise e compreensão por parte da IA. | Recomenda resumos curtos e gerados por IA no nível da página e da seção que capturam o conteúdo principal. | Insere os resumos nas seções relevantes do HTML, melhorando a forma como os modelos interpretam e descrevem o conteúdo da página. |
| Adicionar perguntas frequentes relevantes | Otimização de conteúdo | Detecta lacunas de intenção no conteúdo da página existente que podem se beneficiar de perguntas frequentes. | Sugere conteúdo de perguntas frequentes gerado por IA e alinhado à intenção do usuário e aos tópicos existentes. | Injeta conteúdo de perguntas frequentes no HTML, tornando as páginas mais visíveis e relevantes em respostas orientadas por IA. |
| Simplificar conteúdo complexo | Otimização de conteúdo | Sinaliza páginas com texto complexo que pode atrapalhar a compreensão da IA. | Fornece versões simplificadas geradas por IA de texto complexo, preservando o significado original. | Reescreve seções complexas na página, melhorando a legibilidade da IA. |

### Ferramentas adicionais

O [Adobe LLM Optimizer: sua página da web pode ser citada?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) A extensão do Chrome mostra quanto do conteúdo da sua página da web os LLMs podem acessar e o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, não exige licença ou configuração do produto.

Com um clique único, você pode avaliar a legibilidade por máquina de qualquer site. Você pode visualizar uma comparação lado a lado do que os agentes de IA veem em comparação com o que os usuários humanos veem e estimar quanto conteúdo poderia ser recuperado usando o LLM Optimizer. Acesse a página [A IA pode ler o seu site?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obter mais informações.

## Oportunidades detalhadas

Nas seções a seguir, é possível ver detalhes adicionais sobre cada oportunidade compatível com o recurso Otimização na borda.

### Recuperar visibilidade do conteúdo

Essa oportunidade sinaliza páginas em que o conteúdo principal está oculto para agentes de IA devido à renderização do lado do cliente. Em cada página identificada, é possível ver exatamente qual conteúdo está faltando na visualização do agente de IA, as lacunas de visibilidade e aplicar alterações diretas para recuperar o conteúdo oculto. Ao implantar essa oportunidade com o recurso Otimização na borda, uma versão pré-renderizada e otimizada para IA da página é disponibilizada aos agentes de usuário de LLM para que possam acessar o contexto completo sem executar o Javascript.
Isso garante que a página fique totalmente visível primeiro para os agentes de IA. Aprimoramentos adicionais são aplicados sobre o HTML pré-renderizado.

>[!IMPORTANT]
>Essa funcionalidade de pré-renderização se aplica automaticamente a todas as oportunidades apresentadas abaixo quando implantada com o recurso Otimização na borda, para garantir que a página esteja totalmente visível para os agentes de IA.

### Otimizar cabeçalhos para LLMs

Essa oportunidade detecta páginas em que a estrutura de cabeçalho dificulta a compreensão por parte dos agentes de IA devido a cabeçalhos vazios, duplicados, ausentes ou ambíguos. Em cada página afetada, a oportunidade exibe os cabeçalhos abaixo do ideal e recomenda uma hierarquia mais clara. Quando implantados com o recurso Otimização na borda, os cabeçalhos aprimorados são aplicados no HTML veiculado para o tráfego agêntico. Isso facilita a legibilidade para máquinas, sem alterar o layout para humanos.

### Adicionar resumos compatíveis com LLM

Essa oportunidade identifica páginas que podem se beneficiar de resumos concisos, ajudando LLMs a entender rapidamente sobre o que se trata o conteúdo da página. Para cada página, a oportunidade detecta onde um resumo é mais necessário e cria resumos gerados por IA no nível da página ou da seção. Ao implantar com o recurso Otimização na borda, esses resumos são inseridos no HTML que os agentes de IA recuperam, melhorando as chances de ter seu conteúdo descrito com mais precisão.

### Adicionar perguntas frequentes relevantes

Essa oportunidade sinaliza páginas em que o conteúdo adicional de perguntas e respostas pode corresponder melhor à intenção do usuário e aos prompts de descoberta orientados por IA. Para cada página, ela sugere blocos de perguntas frequentes (FAQ) geradas por IA, relacionados à intenção do usuário e ao conteúdo da página. Com o recurso Otimização na borda, essas perguntas frequentes são inseridas no HTML, tornando sua página mais compatível com a IA e aumentando a probabilidade de que as respostas da IA reflitam diretamente suas orientações.

### Simplificar conteúdo complexo

Essa oportunidade encontra páginas com parágrafos longos e complexos que podem reduzir a compreensão da IA. Para cada página que excede os limites de legibilidade, ela cria conteúdo gerado por IA que é mais simples e fácil de digitalizar, preservando o significado original. Quando implantado na borda, o conteúdo simplificado entregue ao tráfego agêntico ajuda os LLMs a interpretar e resumir o conteúdo com mais fidelidade.

## Otimização automática na borda

Em cada oportunidade, é possível visualizar, editar, implantar, exibir em tempo real e reverter as otimizações na borda.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Visualização

A opção **Visualizar** permite que você veja o impacto de uma sugestão antes que ela seja aplicada. Ela exibe uma comparação lado a lado entre a página atual e o resultado esperado da otimização por IA após aplicar a sugestão. Essa exibição usa a mesma lógica do recurso Otimização na borda, alimentando o tráfego ativo, mas em um modo de visualização isolado. Isso não afeta o tráfego ativo, pois é uma simulação somente leitura para revisão.

![Visualização](/help/assets/optimize-at-edge/preview.png)

### Editar

A opção **Editar** permite refinar ou reescrever completamente a sugestão gerada automaticamente antes de implantá-la. Em vez de aceitar a sugestão, você pode manter o controle total por meio do fluxo de trabalho de edição. A exibição mostra as alterações propostas em um editor estruturado, onde você pode modificar o texto para corresponder melhor à intenção original. A versão editada será entregue aos agentes de IA depois de implantada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implantar

A opção **Implantar** publica as sugestões selecionadas para que as experiências otimizadas possam ser enviadas da borda para os agentes de IA. Se a CDN estiver totalmente roteada, todas as páginas no domínio normalmente serão disponibilizadas com as novas alterações em minutos. Se o roteamento tiver sido configurado apenas para caminhos seletos, somente as páginas na lista de permissões serão publicadas com as otimizações.

![Implantar](/help/assets/optimize-at-edge/deploy.png)

### Visualizar em tempo real

A opção **Visualizar em tempo real** permite verificar se a otimização está ativa e se comportando conforme o esperado para o tráfego agêntico, uma visualização que seria difícil de acessar de outra forma. Você pode visualizar a página ativa em Sugestões fixas, que renderiza a página conforme ela está sendo mostrada aos agentes de IA.

![Visualizar em tempo real](/help/assets/optimize-at-edge/view-live.png)

### Reversão

A reversão reverte com segurança uma otimização implantada anteriormente. A versão somente de IA da página normalmente retorna ao estado anterior em minutos, tornando seguro experimentar as otimizações quando necessário.

![Reversão](/help/assets/optimize-at-edge/rollback.png)

## Perguntas frequentes

P. Que tipo de LLMs são direcionados com o recurso Otimização na borda?

A lista de agentes de usuário a serem direcionados é definida por você durante o processo de integração.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

P. O que acontece se eu ainda não estiver integrado(a) ao recurso Otimização na borda?

Se você clicar em **Implantar otimizações** antes de concluir a instalação necessária, nenhuma informação será aplicada ao site. Em vez disso, uma caixa de diálogo pop-up solicita que você entre em contato com nossa equipe pelo email `llmo-at-edge@adobe.com` para obter assistência durante a integração. Até que a integração seja concluída, você ainda poderá explorar as oportunidades e sugestões detectadas, mas o fluxo de trabalho de implantação com um clique permanecerá inativo.

P: O que acontece quando o conteúdo é atualizado na origem?

Oferecemos a versão otimizada da sua página do cache, desde que a página de origem subjacente não tenha sido alterada. No entanto, quando a origem é alterada para **Recuperar Visibilidade do conteúdo**, nosso sistema é atualizado automaticamente para que os agentes de IA sempre recebam o conteúdo mais atualizado. Isso ocorre porque usamos configurações de TTL (low cache time to live) (por ordem de minutos) para que qualquer atualização de conteúdo em seu site acione uma nova otimização dentro dessa janela. Para oportunidades de conteúdo como **Adicionar Resumos Amigáveis a LLM**, o LLM Optimizer monitora as alterações na página de origem. Se uma alteração for detectada, pausaremos a otimização e a sinalizaremos para revisão humana para evitar o descompasso do conteúdo entre a página visível por agente e a página visível por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. O recurso Otimização na borda é somente para sites que usam o Adobe Edge Delivery Service (EDS)?

Não. O recurso Otimização na borda é independente da CDN e funciona com qualquer arquitetura de front-end, não apenas com as implantadas na pilha do Adobe EDS.

P: Como a pré-renderização do recurso Otimização na borda se diferencia da renderização tradicional do lado do servidor (SSR)?

Ambas resolvem problemas diferentes e podem trabalhar juntas. A SSR tradicional renderiza o conteúdo do lado do servidor, mas não inclui conteúdo carregado posteriormente no navegador. A pré-renderização do recurso Otimização na borda captura a página depois que o JavaScript e os dados do lado do cliente são carregados, produzindo a versão completa na borda da CDN. A SSR se concentra em melhorar a experiência humana, e o recurso Otimização na borda melhora a experiência da web para LLMs.

P. O que acontece se eu implantar otimizações para alguns URLs em meu domínio, mas não todos?

Somente os URLs que você otimiza explicitamente são modificados. Para URLs com oportunidades implantadas, os agentes de IA recebem a versão otimizada. Para URLs sem oportunidades implantadas, nosso serviço simplesmente faz o proxy da página original como está, sem aplicar alterações ou armazená-la em nossa camada de cache de otimização. Isso garante que você possa implantar otimizações seletivamente sem afetar o restante do site.
