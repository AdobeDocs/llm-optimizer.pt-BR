---
title: Otimizar na Edge
description: Saiba como fornecer otimizações no LLM Optimizer na borda da CDN sem precisar fazer alterações de criação.
feature: Opportunities
source-git-commit: 3c6f287b3c3787cee95f99b7031412f26692a88b
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---


# Otimizar na Edge

Esta seção ...

## O que é otimizar na Edge?

Otimizar na Edge é um recurso de implantação baseado em borda no LLM Optimizer que pode fornecer alterações compatíveis com IA para agentes de usuário do LLM. Como fornece otimizações na borda da CDN, nenhuma alteração de criação é necessária no Sistema de gerenciamento de conteúdo (CMS). Ele também direciona somente o tráfego agenciador e não afeta usuários humanos ou bots de SEO.

Quando o LLM Optimizer detecta oportunidades para otimizar uma página, os usuários podem implantar correções diretamente na borda sem a necessidade de alterações na plataforma.

Esse recurso está atualmente em Acesso antecipado.

## Por que um cliente deve estar interessado?

Otimizar na Edge é uma alternativa mais rápida e mais enxuta às correções tradicionais que exigem esforços complexos de engenharia. Quando os clientes concluírem uma configuração única, nenhuma alteração na plataforma ou ciclos de desenvolvimento longos serão necessários para aplicar as alterações às páginas da Web. O usuário pode publicar melhorias em minutos, não em semanas, sem exigir o envolvimento do desenvolvedor. Essa é uma maneira de baixo risco e sem código de otimizar seu site para agentes de IA.

### Principais benefícios e proposta de valor

* **Entrega somente IA:** oferece HTML otimizado para agentes de IA somente sem impacto em visitantes humanos ou bots de SEO.
* **Ciclos mais rápidos:** Publique as alterações em minutos, não em semanas. Não são necessárias alterações na plataforma nem longos ciclos de engenharia.
* **Baixo risco e reversível:** Compatível com um recurso de reversão de um clique que pode reverter a página em minutos.
* **Nenhum impacto no desempenho:** as otimizações baseadas em Edge e o armazenamento em cache mantêm a latência do site inalterada.
* **CDN e CMS-agnostic:** funciona com qualquer configuração de CDN e configuração de front-end, independentemente do CMS.

## Quem deveria usá-lo?

Otimizar no Edge foi projetado para usuários empresariais em equipes de marketing, SEO, conteúdo e estratégia digital. Ele permite que os usuários empresariais concluam a jornada completa no LLM Optimizer: identificando oportunidades, entendendo sugestões e implantando facilmente as correções. Com a opção Otimizar na Edge, os usuários podem visualizar as alterações, implantá-las rapidamente na borda e validar se as otimizações estão ativas. O desempenho pode ser rastreado no ecossistema do LLM Optimizer.

## Quais oportunidades têm o recurso Otimizar na Edge?

Oportunidades que podem melhorar a experiência online do agente são compatíveis com a opção Otimizar no Edge. Saiba mais sobre cada oportunidade na seção [Oportunidades](/help/dashboards/opportunities.md).

## Integração

Você pode ativar Otimizar no Edge depois de ter integrado ao LLM Optimizer e de estar encaminhando seus logs de CDN.

Um engenheiro de CDN é necessário para concluir a configuração inicial para habilitar a Otimização no Edge.

Requisitos para configuração:

* Gere uma chave de API.
* Adicionar Otimizar nas regras de roteamento do Edge na CDN.
* Incluir na lista de permissões caminhos definidos pelo usuário ou todo o domínio.
* Adicione uma lista definida pelo usuário de agentes do usuário do LLM ao target.
* Certifique-se de que o robots.txt não bloqueie nenhum agente do usuário destinado ao target.
* Confirme se o roteamento Otimize at Edge está na interface do usuário do LLM Optimizer.

O Adobe fornece amostras de trechos de configuração para a maioria dos principais CDNs para orientar o processo de configuração. Os exemplos de trechos incluídos em nossas diretrizes precisam ser adaptados à configuração real ativa. A Adobe recomenda implementar as alterações nos ambientes inferiores primeiro.

>[!BEGINTABS]

>[!TAB CDN gerenciada pelo AEM Cloud Service (Fastly)]

**BYOCDN de Tokowaka - CDN Gerenciada pela Adobe**

Usa somente originSelectors para selecionar a origem Tokowaka.

O exemplo a seguir roteia solicitações de agentes LLM em um domínio específico correspondente ao padrão &quot;/es/*&quot; ou caminhos exatos (somente páginas html são roteadas). O exemplo deve fornecer um ponto de partida e, caso você tenha vários originSelectors em sua configuração, é recomendável colocá-los primeiro.

Observações importantes:

* x-tokowaka-request precisa ser verificado antes do roteamento para o back-end de Tokowaka. Somente as solicitações que não têm esse cabeçalho devem ser roteadas para o back-end de Tokowaka.
* a regra originSelector que direciona para o back-end de Tokowaka deve ser a primeira na lista se houver várias regras.
* O segredo TOKOWAKA_API_KEY precisa ser implantado antes da implantação do cdn.yaml

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Tokowaka backend
  originSelectors:
    rules:
      - name: route-to-tokowaka-backend
        when:
          allOf:
            - reqHeader: x-tokowaka-request
              exists: false # avoid loops when requests comes from Tokowaka
            - reqHeader: user-agent
              matches: "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: tokowaka-backend
          headers:
            x-tokowaka-api-key: "${{TOKOWAKA_API_KEY}}"
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"
```

>[!TAB Akamai (BYOCDN)]

**BYOCDN de Tokowaka - Akamai**

```
{
    "name": "Project Tokowaka CDN Rule",
    "children": [
        {
            "name": "Connection settings",
            "children": [],
            "behaviors": [
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.health-detect.status>off</forward:availability.health-detect.status>\n<forward:availability>\n<max-reforwards>1</max-reforwards>\n<max-reconnects>1</max-reconnects>\n</forward:availability>\n<match:forward.server-type value=\"CUSTOMER_ORIGIN\">\n<network:http.read>%(PMUSER_HTTP_READ)</network:http.read>\n<network:http.first-byte-timeout>%(PMUSER_FIRST_BYTE_TIMEOUT)</network:http.first-byte-timeout>\n<network:http.connect-timeout>%(PMUSER_HTTP_CONNECT_TIMEOUT)</network:http.connect-timeout> \n</match:forward.server-type>"
                    },
                    "uuid": "4a8c027b-1b23-44a7-8e12-f8d07e453679",
                    "templateUuid": "41c77091-419f-43f2-9a84-0b406b050cc8"
                }
            ],
            "uuid": "4759571b-8036-4c16-9b60-d3aeb84958f1",
            "criteria": [],
            "criteriaMustSatisfy": "all"
        },
        {
            "name": "Site Failover Behavior",
            "children": [],
            "behaviors": [
                {
                    "name": "failAction",
                    "options": {
                        "actionType": "RECREATED_CO",
                        "contentCustomPath": false,
                        "contentHostname": "www.adobe.com",
                        "enabled": true
                    }
                },
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.fail-action2>\n<add-header>\n<status>on</status>\n<name>x-tokowaka-request</name>\n<value>fo</value>\n</add-header>\n</forward:availability.fail-action2>"
                    }
                }
            ],
            "uuid": "b3000c12-1ab8-49b1-a5d0-75e58bb18c9c",
            "criteria": [
                {
                    "name": "matchResponseCode",
                    "options": {
                        "lowerBound": 400,
                        "matchOperator": "IS_BETWEEN",
                        "upperBound": 599
                    }
                },
                {
                    "name": "originTimeout",
                    "options": {
                        "matchOperator": "ORIGIN_TIMED_OUT"
                    }
                }
            ],
            "criteriaMustSatisfy": "any",
            "comments": "If Tokowaka origin returns a 4xx or 5xx error (or times out), failover condition is to send the request back to Akamai and set the x-tokowaka-request header so we don't re-send the request to Tokowaka"
        }
    ],
    "behaviors": [
        {
            "name": "origin",
            "options": {
                "cacheKeyHostname": "ORIGIN_HOSTNAME",
                "compress": true,
                "customValidCnValues": [
                    "{{Origin Hostname}}",
                    "{{Forward Host Header}}",
                    "*.tokowaka.now"
                ],
                "enableTrueClientIp": true,
                "forwardHostHeader": "ORIGIN_HOSTNAME",
                "hostname": "edge.tokowaka.now",
                "httpPort": 80,
                "httpsPort": 443,
                "ipVersion": "IPV4",
                "minTlsVersion": "DYNAMIC",
                "originCertificate": "",
                "originCertsToHonor": "STANDARD_CERTIFICATE_AUTHORITIES",
                "originSni": true,
                "originType": "CUSTOMER",
                "ports": "",
                "standardCertificateAuthorities": [
                    "akamai-permissive",
                    "THIRD_PARTY_AMAZON"
                ],
                "tlsVersionTitle": "",
                "trueClientIpClientSetting": true,
                "trueClientIpHeader": "True-Client-IP",
                "verificationMode": "CUSTOM"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_LLMCLIENT",
                "variableValue": "TRUE"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "caseSensitive": false,
                "extractLocation": "CLIENT_REQUEST_HEADER",
                "globalSubstitution": false,
                "headerName": "Accept-Language ",
                "regex": "^([a-zA-Z]{2}).*",
                "replacement": "$1",
                "transform": "SUBSTITUTE",
                "valueSource": "EXTRACT",
                "variableName": "PMUSER_LANG"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_X_FORWARDED_HOST",
                "variableValue": "{{builtin.AK_HOST}}"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY",
                "variableValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}};X_FORWARDED_HOST={{user.PMUSER_X_FORWARDED_HOST}}"
            }
        },
        {
            "name": "caching",
            "options": {
                "behavior": "CACHE_CONTROL_AND_EXPIRES",
                "cacheControlDirectives": "",
                "defaultTtl": "1d",
                "enhancedRfcSupport": false,
                "honorMustRevalidate": false,
                "honorPrivate": false,
                "mustRevalidate": false
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-tokowaka-api-key",
                "newHeaderValue": "<your api-key here>",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-config",
                "newHeaderValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-url",
                "newHeaderValue": "{{builtin.AK_URL}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "cacheId",
            "options": {
                "rule": "INCLUDE_VARIABLE",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY"
            }
        },
        {
            "name": "modifyIncomingResponseHeader",
            "options": {
                "action": "DELETE",
                "customHeaderName": "Age",
                "standardDeleteHeaderName": "OTHER"
            }
        },
        {
            "name": "prefreshCache",
            "options": {
                "enabled": true,
                "prefreshval": 90
            }
        },
        {
            "name": "modifyOutgoingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-Forwarded-Host",
                "newHeaderValue": "{{builtin.AK_HOST}}",
                "standardModifyHeaderName": "OTHER"
            }
        }
    ],
    "criteria": [
        {
            "name": "userAgent",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "IS_ONE_OF",
                "matchWildcard": true,
                "values": [
                    "*Tokowaka-AI*",
                    "*ChatGPT-User*",
                    "*GPTBot*",
                    "*OAI-SearchBot*"
                ]
            }
        },
        {
            "name": "path",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "MATCHES_ONE_OF",
                "normalize": false,
                "values": [
                ]
            }
        },
        {
            "name": "requestHeader",
            "options": {
                "headerName": "x-tokowaka-request",
                "matchOperator": "DOES_NOT_EXIST",
                "matchWildcardName": false
            }
        },
        {
            "name": "matchVariable",
            "options": {
                "matchCaseSensitive": true,
                "matchOperator": "IS",
                "matchWildcard": false,
                "variableExpression": "FALSE",
                "variableName": "PMUSER_TOKOWAKA_DISABLE"
            }
        }
    ],
    "criteriaMustSatisfy": "all"
}
```

Considerações importantes:

* A regra de Tokowaka será ATIVADA com base na variável User-Agent + Path + x-tokowaka-request (se não estiver presente) + TOKOWAKA_DISABLE (para permitir o desligamento usando uma única variável)
* Configure as regras para **Modificar a regra Cabeçalhos de Solicitação Recebida** para definir cabeçalhos personalizados
* Defina a chave de cache no Akamai usando a variável definida pelo usuário por meio do mecanismo de modificação da ID de cache. Somente uma única variável definida pelo usuário é permitida, portanto, crie uma variável separada para cache_key e defina-a de acordo.
* Idioma: extraído do cabeçalho Accept-Language usando &quot;regex&quot;: &quot;^([a-zA-Z]{2}).*&quot;
* Com a Modificação da ID de cache em uma correspondência no Agente do usuário, o conteúdo não pode ser removido por URL (apenas para sua informação)
* Mecanismo de failover do site: com a correspondência na regra do usuário-agente, o Akamai não permite o failover com base na verificação de integridade, mas somente com base na resposta/conectividade de origem por solicitação. Defina o cabeçalho resp **x-tokowaka-fo:true** em caso de resposta de failover.
* Não há suporte para SWR no Akamai. Portanto, somente o armazenamento em cache com base em TTL está lá. Portanto, configure uma regra no Akamai para remover o cabeçalho Idade da resposta de origem, caso contrário o armazenamento em cache com base em TTL não funcionaria.
* Certifique-se de que a regra de Tokowaka seja a regra mais inferior na hierarquia de regras (para que ela substitua todas as outras regras).

>[!TAB Fastly (BYOCDN)]

**BYOCDN de Tokowaka - Fastly - VCL**

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Adicionar trechos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**trecho vcl_recv**

```
unset req.http.x-tokowaka-url;
unset req.http.x-tokowaka-config;
unset req.http.x-tokowaka-api-key;

if (!req.http.x-tokowaka-request
    && req.http.user-agent ~ "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-tokowaka-url = req.url; # required for identifying the original url
  set req.http.x-tokowaka-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-tokowaka-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_Tokowaka;
}
```

**trecho de vcl_hash**

```
if (req.http.x-tokowaka-config) {
  set req.hash += "tokowaka";
  set req.hash += req.http.x-tokowaka-config;
}
```

**vcl_deliver_snippet**

```
if (req.http.x-tokowaka-config && resp.status >= 400) {
  set req.http.x-tokowaka-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-tokowaka-config && req.http.x-tokowaka-request == "failover") {
  set resp.http.x-tokowaka-fo = "1";
}
```

>[!ENDTABS]


Para outros provedores de CDN, entre em contato com llmo-at-edge@adobe.com para ajudar suas equipes de TI/CDN com a integração.

<!--This should probably be included Opportunities dashboard content. Content also needs serious editing - lots of "customer needs"and business user" etc.-->

Depois que as configurações forem concluídas, os usuários empresariais poderão implantar sugestões para Otimizar nas oportunidades do Edge no LLM Optimizer.

## Oportunidades

| Oportunidade | Tipo | Identificação automática | Sugestão automática | Otimizar automaticamente |
|---------|----------|----------|----------|----------|
| Recuperar visibilidade do conteúdo | GEO técnico | Detecta páginas em que o conteúdo crítico está oculto dos agentes de IA. Mostra as URLs afetadas e o conteúdo esperado que pode ser recuperado. | Realça o conteúdo que pode ser disponibilizado para agentes de IA e recomenda ativar a pré-renderização para essas páginas. | Disponibiliza um instantâneo do HTML totalmente renderizado e compatível com IA para tráfego de agente que recupera o conteúdo oculto anteriormente. |
| Otimizar cabeçalhos para IA | Otimização de conteúdo | Verifica cabeçalhos para detectar cabeçalhos vazios, duplicados, ausentes ou ambíguos que podem reduzir a legibilidade da máquina. | Propõe uma hierarquia de cabeçalho mais limpa e rótulos aprimorados e mostra uma visualização da estrutura atualizada para cada página. | Injeta a estrutura de cabeçalho aprimorada para agentes de IA, preservando seu design visual e tornando a página mais compreensível para LLMs. |
| Adicionar resumos compatíveis com IA | Otimização de conteúdo | O código identifica páginas longas ou complexas que não têm resumos concisos no nível da página ou da seção, dificultando a digitalização e a compreensão rápidas pela IA. | Recomenda resumos curtos, gerados por IA no nível da página e da seção, que capturam o conteúdo principal. | Insere os resumos nas seções relevantes do HTML, melhorando a forma como os modelos interpretam e descrevem o conteúdo da página. |
| Adicionar perguntas frequentes relevantes | Otimização de conteúdo | Detecta lacunas de intenção no conteúdo da página existente que podem se beneficiar das perguntas frequentes. | Sugere conteúdo de perguntas frequentes gerado por IA alinhado às intenções do usuário e aos tópicos existentes. | Injeta conteúdo de perguntas frequentes no HTML, tornando as páginas mais visíveis e relevantes em respostas orientadas por IA. |
| Simplificar conteúdo complexo | Otimização de conteúdo | Sinaliza páginas com texto complexo que pode atrapalhar a compreensão da IA. | Fornece versões simplificadas geradas por IA de testes complexos, preservando o significado original. | Substitui seções complexas na página, melhorando a legibilidade da IA. |

### Recuperar visibilidade do conteúdo

Essa oportunidade sinaliza páginas em que o conteúdo principal está oculto para agentes de IA devido à renderização do lado do cliente. Para cada página identificada, ele mostra exatamente qual conteúdo está faltando na visualização do agente de IA, destaca as lacunas de visibilidade e permite aplicar as alterações diretamente para recuperar o conteúdo oculto. Ao implantar essa oportunidade com a opção Otimizar no Edge, uma versão pré-renderizada e otimizada para IA da página é disponibilizada aos agentes do usuário do LLM para que eles possam acessar o contexto completo sem executar o Javascript.

**Esse recurso de pré-renderização se aplica automaticamente a todas as oportunidades que se seguem quando implantado com Otimizar na Edge.** Isso garante que a página esteja totalmente visível para os agentes de IA primeiro. Aprimoramentos adicionais são aplicados sobre o HTML pré-renderizado.

#### Ferramentas adicionais

Sua página da Web é citável? A [Adobe LLM Optimizer: sua página da Web é citável?A extensão do Chrome ](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) permite ver exatamente quanto do conteúdo da sua página da Web os LLMs podem acessar e o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, ele não requer licença ou configuração do produto.

Com um único clique, você pode avaliar a legibilidade automática de qualquer site, visualizar uma comparação lado a lado do que os agentes de IA veem com o que os usuários humanos veem e estimar quanto conteúdo pode ser recuperado usando o LLM Optimizer. Consulte [A IA pode ler o seu site?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obter mais informações.

### Otimizar Cabeçalhos para LLMs

Essa oportunidade detecta páginas em que a estrutura de cabeçalho dificulta que os agentes de IA entendam a página devido a cabeçalhos vazios, duplicados, ausentes ou ambíguos. Para cada página afetada, a oportunidade exibe os cabeçalhos abaixo do ideal e recomenda uma hierarquia mais clara. Quando implantados com a opção Otimizar no Edge, os cabeçalhos aprimorados são aplicados no HTML veiculado para agenciar o tráfego, o que pode ajudar a melhorar a legibilidade da máquina e, ao mesmo tempo, deixar o layout voltado para o humano inalterado.

### Adicionar resumos compatíveis com LLM

Esta oportunidade identifica páginas que podem se beneficiar de resumos concisos para ajudar os LLMs a entender rapidamente sobre o que se trata a página. Para cada página, a oportunidade detecta onde um resumo é mais necessário e cria resumos gerados pela IA no nível da página e/ou da seção. Quando você implanta com a opção Otimizar no Edge, esses resumos são inseridos na HTML que os agentes de IA recuperam, melhorando as chances de ter seu conteúdo descrito com mais precisão.

### Adicionar perguntas frequentes relevantes

Essa oportunidade sinaliza páginas em que o conteúdo adicional de perguntas e respostas pode corresponder melhor à intenção do usuário e às solicitações de detecção orientadas por IA. Para cada página, ela propõe blocos de perguntas frequentes gerados por IA vinculados à intenção e ao conteúdo do usuário na página. Com a opção Otimizar no Edge, essas Perguntas frequentes são inseridas no HTML, tornando sua página mais amigável para IA e aumentando a probabilidade de as respostas de IA refletirem diretamente suas orientações.

### Simplificar conteúdo complexo

Essa oportunidade encontra páginas com parágrafos longos e complexos que podem reduzir a compreensão da IA. Para cada página que excede os limites de legibilidade, ele cria conteúdo gerado por IA que é mais simples e mais digitalizável, preservando o significado original. Quando implantado na borda, o conteúdo simplificado entregue ao tráfego agêntrico ajuda os LLMs a interpretar e resumir seu conteúdo com mais fidelidade.

## Sugestões

Para cada oportunidade, você pode visualizar, editar, implantar, visualizar em tempo real e reverter as otimizações na borda.

### Visualização

A visualização permite que os usuários vejam o impacto de uma sugestão na página antes que qualquer item seja publicado. Ela exibe uma diferença lado a lado entre a página atual e a versão otimizada para IA esperada após aplicar a sugestão. Essa exibição usa a mesma lógica de Otimizar no Edge que potencializará o tráfego ativo, mas em um modo de visualização seguro e isolado. Isso não afeta o tráfego direto, pois é uma simulação somente leitura para revisão.

![Visualização](/help/assets/optimize-at-edge/preview.png)

### Editar

Editar permite que os usuários refine ou regravem completamente a sugestão gerada automaticamente antes de implantá-la. Em vez de aceitar passivamente a sugestão, os usuários mantêm controle total por meio desse workflow humano em loop. A exibição mostra as alterações propostas em um editor estruturado, em que os usuários podem modificar o texto para melhor corresponder à intenção. A versão editada será entregue aos agentes de IA depois de implantada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implantar

Implantar publica as sugestões selecionadas para que as experiências otimizadas possam ser veiculadas desde a borda até os agentes de IA. Se o CDN for totalmente roteado, todas as páginas no domínio entrarão em funcionamento com as novas alterações, normalmente em minutos. Incluir na lista de permissões Se o roteamento tiver sido configurado apenas para caminhos selecionados, somente as páginas destacadas entrarão em funcionamento com as otimizações.

![Implantar](/help/assets/optimize-at-edge/deploy.png)

### Exibir em tempo real

View Live permite que os usuários verifiquem se a otimização está ativa e se comportando conforme esperado para o tráfego de agente, uma visualização que, de outra forma, seria difícil de acessar. Os usuários podem visualizar a página ao vivo em Sugestões fixas, que renderiza a página conforme mostrado aos agentes de IA.

![Exibir em tempo real](/help/assets/optimize-at-edge/view-live.png)

### Reverter

A reversão reverte com segurança uma otimização implantada anteriormente. A versão somente IA da página normalmente retorna ao estado anterior em minutos, tornando seguro para os usuários experimentar otimizações, se necessário.

![Reversão](/help/assets/optimize-at-edge/rollback.png)

## Perguntas frequentes

P. Que tipo de LLMs você segmenta com Otimizar na Edge?

A lista de agentes de usuário a serem direcionados é completamente definida pelo cliente na integração.

P. O que significa &quot;Edge&quot; em Otimizar na Edge?

Em nosso contexto, &quot;Edge&quot; significa que a otimização é aplicada na camada CDN e não dentro do CMS.

P. Por que essa otimização requer um CDN?

O CDN é o local onde a versão otimizada da página é montada e entregue aos agentes de IA. Usamos a CDN para garantir que o CMS de origem permaneça inalterado. Essa separação permite melhorar a visibilidade do LLM sem alterar os workflows de publicação existentes.

P. O que acontece se eu ainda não estiver integrado ao Otimize at Edge?

Se você clicar em **Implantar otimizações** antes de concluir a instalação necessária, nada será aplicado ao site. Em vez disso, uma caixa de diálogo pop-up solicita que você entre em contato com nossa equipe em llmo-at-edge@adobe.com para obter assistência de integração. Até que a integração seja concluída, você ainda poderá explorar as oportunidades e sugestões detectadas, mas o fluxo de trabalho de implantação de um clique permanecerá inativo.

P: O que acontece quando o conteúdo é atualizado na origem?

Oferecemos a versão otimizada da página do cache, desde que a página de origem subjacente não tenha sido alterada. No entanto, quando a origem é alterada, nosso sistema é atualizado automaticamente para que os agentes de IA sempre recebam o conteúdo mais atualizado. Isso ocorre porque usamos TTLs de cache baixos em ordem de minutos para que qualquer atualização de conteúdo no site acione uma nova otimização dentro dessa janela. Como não há um TTL universal que se ajuste a todos os sites, podemos configurar esse TTL com base nas regras de invalidação de cache para garantir que ambos os sistemas permaneçam sincronizados.

P. O recurso Otimizar na Edge é somente para sites que usam o Adobe Edge Delivery Service (EDS)?

Não. Otimizar na Edge é independente de CDN e funciona com qualquer arquitetura front-end, não apenas aquelas implantadas na pilha de EDS da Adobe.

P. Como a pré-renderização do Otimize at Edge é diferente da renderização tradicional do lado do servidor (SSR)?

Os dois resolvem problemas diferentes e podem trabalhar juntos. O SSR tradicional renderiza o conteúdo do lado do servidor, mas não inclui conteúdo carregado posteriormente no navegador. Otimizar na pré-renderização do Edge captura a página após o carregamento de dados do JavaScript e do lado do cliente, produzindo a versão totalmente montada na borda do CDN. O SSR se concentra em melhorar a experiência humana e Otimizar no Edge melhora a experiência da Web para LLMs.


















