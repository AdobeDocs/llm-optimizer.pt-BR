---
title: Otimizar na Edge
description: Saiba como fornecer otimizações no LLM Optimizer na borda da CDN sem precisar fazer alterações de criação.
feature: Opportunities
source-git-commit: eb8bdf9144aebb85171a529a3cc25034be5b076e
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---


# Otimizar na Edge

Esta página fornece uma visão geral detalhada sobre como fornecer otimizações na borda da CDN sem alterações de criação. Ele aborda o processo de integração, as oportunidades de otimização disponíveis e como otimizar automaticamente na borda.

>[!NOTE]
>Essa funcionalidade está atualmente em Acesso antecipado. Você pode saber mais sobre os programas de Acesso Antecipado [aqui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## O que é otimizar na Edge?

Otimizar na Edge é um recurso de implantação baseado em borda no LLM Optimizer que fornece alterações amigáveis para IA a agentes de usuário do LLM. No contexto atual, &quot;Edge&quot; significa que a otimização é aplicada na camada CDN. Como ela fornece otimizações na camada CDN, nenhuma alteração de criação no Sistema de gerenciamento de conteúdo (CMS) é necessária, portanto, o CMS de origem permanece inalterado. Essa separação permite melhorar a visibilidade do LLM sem alterar os workflows de publicação existentes. Ele é direcionado somente ao tráfego direto e não afeta usuários humanos nem bots de SEO. Quando o LLM Optimizer detecta oportunidades para otimizar uma página, os usuários podem implantar correções diretamente na borda do CDN.

Otimizar na Edge é uma alternativa mais rápida e mais enxuta às correções tradicionais que exigem esforços complexos de engenharia. Como mencionado, após concluir uma configuração única, nenhuma alteração na plataforma ou ciclos de desenvolvimento longos são necessários para aplicar as alterações. Você pode publicar melhorias em minutos sem exigir o envolvimento do desenvolvedor. É uma maneira não codificada de otimizar seu site para agentes de IA.

Otimizar no Edge foi projetado para usuários empresariais em equipes de marketing, SEO, conteúdo e estratégia digital. Ele permite que os usuários empresariais concluam a jornada completa no LLM Optimizer: identificando oportunidades, entendendo sugestões e implantando facilmente as correções. Com a opção Otimizar na Edge, os usuários podem visualizar as alterações, implantá-las rapidamente na borda da CDN e validar se as otimizações estão ativas. O desempenho pode ser rastreado no ecossistema do LLM Optimizer.

### Principais benefícios

* **Entrega somente IA:** oferece o HTML otimizado somente para agentes de IA, sem impacto para visitantes humanos ou bots de SEO.
* **Ciclos mais rápidos:** Publicar alterações em minutos, não em semanas. Não são necessárias alterações na plataforma nem longos ciclos de engenharia.
* **Reversível:** Compatível com um recurso de reversão de um clique que pode reverter a página em minutos.
* **Nenhum impacto no desempenho:** as otimizações baseadas em Edge e o armazenamento em cache mantêm a latência do site inalterada.
* **CDN e CMS-agnostic:** funciona com qualquer configuração de CDN e configuração de front-end, independentemente do Sistema de Gerenciamento de Conteúdo.

### Quais oportunidades são compatíveis com a opção Otimizar na Edge?

Oportunidades que podem melhorar a experiência online do agente são compatíveis com a opção Otimizar no Edge. Saiba mais sobre cada oportunidade na página [Painel de Oportunidades](/help/dashboards/opportunities.md) e na seção de oportunidades na página atual.

## Integração

Você deve entrar em contato com a equipe de conta da Adobe ou com a equipe do FDE para iniciar o processo de integração. Sua equipe de TI ou CDN também é necessária para concluir os pré-requisitos e o processo de configuração. Além disso, você também pode entrar em contato com `llmo-at-edge@adobe.com` para obter mais assistência de integração.

Pré-requisitos para integração ao Otimizar no Edge:

* Conclua o processo de integração com o LLM Optimizer.
* Conclua o processo de encaminhamento de logs para os logs CDN.

Requisitos para sua equipe de TI/CDN:

* Gere uma chave de API.
* Adicionar Otimizar nas regras de roteamento do Edge na CDN.
* Incluir na lista de permissões caminhos definidos pelo usuário ou todo o domínio.
* Adicione uma lista definida pelo usuário de agentes do usuário do LLM ao target.
* Certifique-se de que `robots.txt` não bloqueie nenhum agente do usuário destinado ao direcionamento.
* Confirme a Otimização no Edge Routing na interface do LLM Optimizer.

Para orientar o processo de configuração, apresentado abaixo, são exemplos de configurações para várias configurações de CDN. Lembre-se de que esses exemplos devem ser adaptados à sua configuração real em tempo real. Recomendamos aplicar as alterações nos ambientes inferiores primeiro.

>[!BEGINTABS]

>[!TAB CDN Gerenciada pela Adobe]

**CDN Gerenciada pela Adobe**

A finalidade dessa configuração é configurar solicitações com agentes de usuário de agente que serão roteados para o serviço Otimizer (`live.edgeoptimize.net` backend). Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

A configuração de roteamento é feita usando uma [regra CDN originSelector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). Os pré-requisitos são os seguintes:

* decidir o domínio a ser roteado
* decidir os caminhos a serem roteados
* decidir os agentes de usuário a serem roteados (regex recomendado)

Para implantar a regra, é necessário:

* criar um [pipeline de configuração](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* confirme o arquivo de configuração `cdn.yaml` no repositório
* executar o pipeline de configuração


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

Para testar a configuração, execute um curl e espere o seguinte:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

>[!TAB Fastly (BYOCDN)]

**Otimização de Edge BYOCDN - Fastly - VCL**

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Adicionar trechos de VCL](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**trecho vcl_recv**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**trecho de vcl_hash**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_deliver_snippet**

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

>[!TAB Akamai (BYOCDN)]

**Otimização BYOCDN para Edge - Akamai**

A finalidade dessa configuração é rotear solicitações de agentes de usuário agenciais para o serviço de Otimização do Edge (`live.edgeoptimize.net` back-end). Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.


**A seguinte regra JSON do Akamai Property Manager encaminha agentes de usuário LLM para Otimização da Edge:**

A configuração inclui as seguintes etapas:

**1. Definir critérios de roteamento (correspondência usuário-agente)**

![Definir critérios de roteamento](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Definir Origem e comportamento SSL**

![Definir Origem e comportamento do SSL](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Definir Variável de Chave de Cache**

![Definir Variável de Chave de Cache](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Armazenando Regras em Cache**

![Regras de armazenamento em cache](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modificar Cabeçalhos de Solicitação de Entrada**

![Modificar Cabeçalhos de Solicitação de Entrada](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Modificar Cabeçalhos de Resposta de Entrada**

![Modificar Cabeçalhos de Resposta de Entrada](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Modificação de ID de Cache**

![Modificação da ID do Cache](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Failover de Site**

![Failover de Site](/help/assets/optimize-at-edge/akamai-step8-failover.png)

![Comportamentos de Failover](/help/assets/optimize-at-edge/akamai-step8-failover-behaviors.png)

![Regras de Failover](/help/assets/optimize-at-edge/akamai-step8-failover-rules.png)

![Resposta de Comportamentos](/help/assets/optimize-at-edge/akamai-step8-behaviors-response.png)

Para testar a configuração, execute um curl e espere o seguinte:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

>[!ENDTABS]

>[!NOTE]
>Para outros provedores de CDN, entre em contato com `llmo-at-edge@adobe.com` para auxiliar suas equipes de TI/CDN com a integração. Quando as configurações de instalação estiverem concluídas, você poderá implantar sugestões para Otimizar nas oportunidades do Edge no LLM Optimizer.

## Oportunidades

Na tabela a seguir, são apresentadas oportunidades que podem melhorar a experiência online agêntica e são compatíveis com a opção Otimizar no Edge.

| Oportunidade | Tipo | Identificação automática | Sugestão automática | Otimizar automaticamente |
|---------|----------|----------|----------|----------|
| Recuperar visibilidade do conteúdo | GEO técnico | Detecta páginas em que o conteúdo crítico está oculto dos agentes de IA. Mostra as URLs afetadas e o conteúdo esperado que pode ser recuperado. | Realça o conteúdo que pode ser disponibilizado para agentes de IA e recomenda ativar a pré-renderização para essas páginas. | Disponibiliza um instantâneo do HTML totalmente renderizado e compatível com IA para tráfego de agente que recupera o conteúdo oculto anteriormente. |
| Otimizar Cabeçalhos para LLMs | Otimização de conteúdo | Verifica cabeçalhos para detectar cabeçalhos vazios, duplicados, ausentes ou ambíguos que podem reduzir a legibilidade da máquina. | Propõe uma hierarquia de cabeçalho mais limpa e rótulos aprimorados e mostra uma visualização da estrutura atualizada para cada página. | Injeta a estrutura de cabeçalho aprimorada para agentes de IA, preservando seu design visual e tornando a página mais legível para LLMs. |
| Adicionar resumos compatíveis com LLM | Otimização de conteúdo | O código identifica páginas longas ou complexas que não têm resumos concisos no nível da página ou da seção, dificultando a digitalização e a compreensão rápidas pela IA. | Recomenda resumos curtos, gerados por IA no nível da página e da seção, que capturam o conteúdo principal. | Insere os resumos nas seções relevantes do HTML, melhorando a forma como os modelos interpretam e descrevem o conteúdo da página. |
| Adicionar perguntas frequentes relevantes | Otimização de conteúdo | Detecta lacunas de intenção no conteúdo da página existente que podem se beneficiar das perguntas frequentes. | Sugere conteúdo de perguntas frequentes gerado por IA alinhado à intenção do usuário e aos tópicos existentes. | Injeta conteúdo de perguntas frequentes no HTML, tornando as páginas mais visíveis e relevantes em respostas orientadas por IA. |
| Simplificar conteúdo complexo | Otimização de conteúdo | Sinaliza páginas com texto complexo que pode atrapalhar a compreensão da IA. | Fornece versões simplificadas geradas por IA de texto complexo, preservando o significado original. | Substitui seções complexas na página, melhorando a legibilidade da IA. |

### Ferramentas adicionais

A [Adobe LLM Optimizer: sua página da Web é citável?A extensão do Chrome ](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) mostra quanto do conteúdo da sua página da Web os LLMs podem acessar e o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, ele não requer licença ou configuração do produto.

Com um clique único, você pode avaliar a legibilidade de máquina de qualquer site. Você pode fazer uma comparação lado a lado do que os agentes de IA veem com relação ao que os usuários humanos veem e estimar quanto conteúdo pode ser recuperado usando o LLM Optimizer. Consulte o [A IA pode ler o seu site?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) página para obter mais informações.

## Oportunidades detalhadas

Nas seções a seguir, é possível exibir detalhes adicionais para cada oportunidade compatível com a opção Otimizar na Edge.

### Recuperar visibilidade do conteúdo

Essa oportunidade sinaliza páginas em que o conteúdo principal está oculto para agentes de IA devido à renderização do lado do cliente. Para cada página identificada, ele mostra exatamente qual conteúdo está faltando na visualização do agente de IA, destaca as lacunas de visibilidade e permite aplicar as alterações diretamente para recuperar o conteúdo oculto. Ao implantar essa oportunidade com a opção Otimizar no Edge, uma versão pré-renderizada e otimizada para IA da página é disponibilizada aos agentes do usuário do LLM para que eles possam acessar o contexto completo sem executar o Javascript.
Isso garante que a página fique totalmente visível para os agentes de IA. Aprimoramentos adicionais são aplicados sobre o HTML pré-renderizado.

>[!IMPORTANT]
>Esse recurso de pré-renderização se aplica automaticamente a todas as oportunidades apresentadas abaixo quando implantado com Otimizar no Edge para garantir que a página esteja totalmente visível para os agentes de IA.

### Otimizar Cabeçalhos para LLMs

Essa oportunidade detecta páginas em que a estrutura de cabeçalho dificulta que os agentes de IA entendam a página devido a cabeçalhos vazios, duplicados, ausentes ou ambíguos. Para cada página afetada, a oportunidade exibe os cabeçalhos abaixo do ideal e recomenda uma hierarquia mais clara. Quando implantados com Otimizar no Edge, os cabeçalhos aprimorados são aplicados no HTML veiculado para o tráfego agêntico. Isso ajuda a legibilidade da máquina, deixando o layout voltado para o humano o mesmo.

### Adicionar resumos compatíveis com LLM

Esta oportunidade identifica páginas que podem se beneficiar de resumos concisos para ajudar os LLMs a entender rapidamente sobre o conteúdo da página. Para cada página, a oportunidade detecta onde um resumo é mais necessário e cria resumos gerados pela IA no nível da página ou da seção. Quando você implanta com a opção Otimizar no Edge, esses resumos são inseridos na HTML que os agentes de IA recuperam, melhorando as chances de ter seu conteúdo descrito com mais precisão.

### Adicionar perguntas frequentes relevantes

Essa oportunidade sinaliza páginas em que o conteúdo adicional de perguntas e respostas pode corresponder melhor à intenção do usuário e às solicitações de detecção orientadas por IA. Para cada página, ela propõe blocos de perguntas frequentes gerados por IA vinculados à intenção e ao conteúdo do usuário na página. Com a opção Otimizar no Edge, essas Perguntas frequentes são inseridas no HTML, tornando sua página mais amigável para IA e aumentando a probabilidade de as respostas de IA refletirem diretamente suas orientações.

### Simplificar conteúdo complexo

Essa oportunidade encontra páginas com parágrafos longos e complexos que podem reduzir a compreensão da IA. Para cada página que excede os limites de legibilidade, ele cria conteúdo gerado por IA que é mais simples e fácil de digitalizar, preservando o significado original. Quando implantado na borda, o conteúdo simplificado entregue ao tráfego agêntrico ajuda os LLMs a interpretar e resumir seu conteúdo com mais fidelidade.

## Otimização automática na Edge

Para cada oportunidade, você pode visualizar, editar, implantar, exibir em tempo real e reverter as otimizações na borda.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Visualização

**Visualizar** permite que você veja o impacto de uma sugestão antes que ela entre em vigor. Ela exibe uma diferença lado a lado entre a página atual e a versão otimizada para IA esperada após aplicar a sugestão. Essa exibição usa a mesma lógica de Otimizar no Edge que alimentará o tráfego ativo, mas em um modo de visualização isolado. Isso não afeta o tráfego direto, pois é uma simulação somente leitura para revisão.

![Visualização](/help/assets/optimize-at-edge/preview.png)

### Editar

**Editar** permite que você refine ou regrave completamente a sugestão gerada automaticamente antes de implantá-la. Em vez de aceitar a sugestão, mantenha o controle total por meio do fluxo de trabalho de edição. A exibição mostra as alterações propostas em um editor estruturado, em que você pode modificar o texto para corresponder melhor à intenção original. A versão editada será entregue aos agentes de IA depois de implantada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implantar

**Implantar** publica as sugestões selecionadas para que as experiências otimizadas possam ser veiculadas da borda aos agentes de IA. Se o CDN for totalmente roteado, todas as páginas no domínio normalmente entrarão em funcionamento com as novas alterações em minutos. Incluir na lista de permissões Se o roteamento tiver sido configurado apenas para caminhos selecionados, somente as páginas destacadas entrarão em funcionamento com as otimizações.

![Implantar](/help/assets/optimize-at-edge/deploy.png)

### Visualizar ao vivo

**Exibir em tempo real** permite verificar se a otimização está em tempo real e se comportando conforme o esperado para tráfego de agente, uma exibição que, de outra forma, seria difícil de acessar. Você pode visualizar a página ao vivo em Sugestões fixas, que renderiza a página conforme mostrado aos agentes de IA.

![Exibir em tempo real](/help/assets/optimize-at-edge/view-live.png)

### Reverter

A reversão reverte com segurança uma otimização implantada anteriormente. A versão somente IA da página normalmente retorna ao estado anterior em minutos, tornando seguro experimentar otimizações quando necessário.

![Reversão](/help/assets/optimize-at-edge/rollback.png)

## Perguntas frequentes

P. Que tipo de LLMs você segmenta com Otimizar na Edge?

A lista de agentes de usuário a serem direcionados é definida por você durante o processo de integração.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

P. O que acontece se eu ainda não estiver integrado ao Otimize at Edge?

Se você clicar em **Implantar otimizações** antes de concluir a instalação necessária, nada será aplicado ao site. Em vez disso, uma caixa de diálogo pop-up solicita que você entre em contato com nossa equipe em `llmo-at-edge@adobe.com` para obter assistência de integração. Até que a integração seja concluída, você ainda poderá explorar as oportunidades e sugestões detectadas, mas o fluxo de trabalho de implantação de um clique permanecerá inativo.

P: O que acontece quando o conteúdo é atualizado na origem?

Oferecemos a versão otimizada da página do cache, desde que a página de origem subjacente não tenha sido alterada. No entanto, quando a origem é alterada, nosso sistema é atualizado automaticamente para que os agentes de IA sempre recebam o conteúdo mais atualizado. Isso ocorre porque usamos configurações de TTL (low cache time to live) (por ordem de minutos) para que qualquer atualização de conteúdo em seu site acione uma nova otimização dentro dessa janela. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. O recurso Otimizar na Edge é somente para sites que usam o Adobe Edge Delivery Service (EDS)?

Não. Otimizar na Edge é independente de CDN e funciona com qualquer arquitetura front-end, não apenas aquela implantada na pilha de EDS da Adobe.

P. Como a pré-renderização do Otimize at Edge é diferente da renderização tradicional do lado do servidor (SSR)?

Ambos resolvem problemas diferentes e podem trabalhar juntos. O SSR tradicional renderiza o conteúdo do lado do servidor, mas não inclui conteúdo carregado posteriormente no navegador. Otimizar na pré-renderização do Edge captura a página depois que os dados do JavaScript e do lado do cliente são carregados, produzindo a versão totalmente montada na borda do CDN. O SSR se concentra em melhorar a experiência humana e Otimizar no Edge melhora a experiência da Web para LLMs.
