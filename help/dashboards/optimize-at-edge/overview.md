---
title: Otimizar na borda
description: Saiba como fornecer otimizações na borda da CDN, no LLM Optimizer, sem precisar fazer alterações de criação.
feature: Opportunities
autotag-review: '2026-05-15T17:55:41.072Z'
TQID: 'https://experienceleague.adobe.com/kMxoKtrfyzxIpLJP9nt-rq6GP37ICCNe4XienUKqDZE'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 559e77adedb1a93215090441c93c2aa6dc664e5f
workflow-type: tm+mt
source-wordcount: 2931
ht-degree: 63%

---


# Otimizar na borda

Esta página oferece uma visão geral detalhada sobre como fornecer otimizações na borda da CDN sem realizar alterações de criação. Ela aborda o processo de integração, as oportunidades de otimização disponíveis e como otimizar automaticamente na borda.

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

Algumas oportunidades que podem melhorar a experiência agêntica na web são compatíveis com a Otimização na borda. Saiba mais sobre cada oportunidade na página [Painel de oportunidades](/help/dashboards/opportunities-overview.md) e na seção de oportunidades da página atual.

## Integração

<!--You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.-->

Inicie o processo de integração na sua conta do LLM Optimizer:

1. No painel **Configuração do cliente**, selecione a guia **Configuração da CDN**.
1. Clique em **Integrar CDN**.
   ![Guia de Configuração da CDN](/help/overview/assets/cc-cdn.png)
1. Para os clientes do Fastly gerenciados pelo AEM Cloud Service, a configuração do roteamento é autônoma e pode ser concluída diretamente na interface do usuário do LLM Optimizer. Para os clientes que utilizam outros provedores de CDN, sua equipe de TI/CDN precisa concluir a configuração necessária e os pré-requisitos. Você também pode consultar os guias de CDN de exemplo fornecidos abaixo para obter orientações adicionais.

>[!NOTE]
>Consulte os guias passo a passo abaixo, que abrangem todo o fluxo de integração. Para problemas não resolvidos pelos guias, você pode entrar em contato com `llmo-at-edge@adobe.com`.

Requisitos para a equipe de TI/CDN:

* Adicione o user-agent `*AdobeEdgeOptimize/1.0*` à lista de permissões no arquivo robots.txt do site ou nas regras de gerenciamento de bot-traffic.
* Verifique se as páginas não estão bloqueadas no nível de domínio ou da CDN.
* Adicionar regras de roteamento para o recurso Otimização na borda da CDN.
* Se a CDN tiver regras de WAF ou do Bot Manager, inclua o agente de usuário `*AdobeEdgeOptimize/1.0*` na lista de permissões. Caso seja necessária verificação adicional, configure o cabeçalho `x-edgeoptimize-fetcher-key`. Cada guia BYOCDN abaixo inclui as etapas.
* Confirme o roteamento do recurso Otimização na borda na interface do LLM Optimizer.

O diagrama a seguir ilustra como as solicitações fluem por meio de uma configuração BYOCDN com a Otimização na borda:

![Fluxo de solicitação BYOCDN](/help/assets/optimize-at-edge/byocdn-request-flow.png)

>[!IMPORTANT]
>O roteamento deve ser configurado na CDN externa (a CDN mais próxima do cliente). Se você tiver várias CDNs, o roteamento só poderá ser feito na CDN externa.

Para orientar o processo de configuração, selecione seu provedor de CDN abaixo e siga o guia de configuração correspondente. Lembre-se de que esses exemplos devem ser adaptados à sua configuração atualmente ativa. Recomendamos aplicar as alterações nos ambientes inferiores primeiro.

### Guias de configuração de CDN

| Provedor de CDN | Tipo | Guia |
|---|---|---|
| CDN gerenciada do AEM Cloud Service (Fastly) | Gerenciado pela Adobe | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/aemcs-managed-cdn.md) |
| Fastly (BYOCDN) | Traga sua própria CDN | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/fastly-byocdn.md) |
| Akamai (BYOCDN) | Traga sua própria CDN | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Traga sua própria CDN | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/cloudflare-byocdn.md) |
| CloudFront (BYOCDN) | Traga sua própria CDN | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/cloudfront-byocdn.md) |
| Porta frontal do Azure (BYOCDN) | Traga sua própria CDN | [Exibir guia de configuração](/help/dashboards/optimize-at-edge/azure-front-door-byocdn.md) |

>[!NOTE]
>
>Se o provedor de CDN não estiver listado acima ou se você não encontrar o domínio ou email na interface do usuário do LLM Optimizer, entre em contato com `llmo-at-edge@adobe.com` para obter assistência de integração. Após a conclusão das configurações, você poderá enviar sugestões para o recurso Otimização na borda no LLM Optimizer.

Cada guia de configuração de CDN acima inclui etapas de verificação detalhadas no final para confirmar que o tráfego agêntico está sendo roteado corretamente e que o tráfego humano não é afetado.

## Oportunidades

A tabela a seguir apresenta oportunidades que podem melhorar a experiência agêntica na web e que são compatíveis com o recurso Otimização na borda.

| Oportunidade | Tipo | Identificação automática | Sugestão automática | Otimizar automaticamente |
|---------|----------|----------|----------|----------|
| [Recuperar visibilidade do conteúdo](/help/dashboards/opportunities/recover-content-visibility.md) | GEO técnico | Detecta páginas em que o conteúdo crítico não está visível para agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Realça o conteúdo que pode ser disponibilizado para agentes de IA e recomenda habilitar a pré-renderização para essas páginas. | Disponibiliza um instantâneo do HTML totalmente renderizado e compatível com IA para tráfego agêntico que recupera o conteúdo oculto anteriormente. |
| [Enriquecer Páginas De Detalhes Do Produto](/help/dashboards/opportunities/enrich-product-detail-pages.md) | GEO técnico | Para as vitrines do Adobe Commerce, compara os dados completos do catálogo ao que os agentes de IA podem acessar em cada página de detalhes do produto; mostra PDPs em que as variantes, as especificações, os atributos e os campos de catálogo relacionados estão ausentes no HTML visível para agentes, priorizados pelo tráfego de agente. | Destaca as informações recuperáveis do catálogo que estão faltando na visualização do agente e por que isso é importante para a detecção de produtos orientada por LLM. | Disponibiliza um instantâneo do HTML totalmente pré-renderizado e compatível com IA para tráfego de agente na borda da CDN, para que os agentes recebam um contexto de produto avançado do seu catálogo sem alterações no CMS ou catálogo. |
| [Adicionar Resumos Amigáveis a LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | Otimização de conteúdo | O código identifica páginas de alto tráfego que não têm resumos concisos e pontos-chave estruturados no nível da página ou da seção, dificultando a digitalização e a interpretação pelos agentes de IA. | Recomenda resumos curtos gerados por IA e pontos-chave com base no conteúdo existente. | Insere resumos e pontos principais nas seções relevantes do HTML, melhorando a forma como os modelos interpretam e descrevem o conteúdo da página. |
| [Adicionar perguntas frequentes relevantes](/help/dashboards/opportunities/add-relevant-faqs.md) | Otimização de conteúdo | O código identifica páginas de alto tráfego que não têm conteúdo estruturado de perguntas e respostas alinhado ao seu conjunto de prompts, dificultando aos agentes de IA corresponder as perguntas do usuário à sua página. | Sugere conteúdo de perguntas frequentes gerado por IA alinhado à intenção do usuário e aos tópicos da página existentes. | Injeta conteúdo de perguntas frequentes no HTML, tornando as páginas mais visíveis e relevantes em respostas orientadas por IA. |
| [Simplificar conteúdo complexo](/help/dashboards/opportunities/simplify-complex-content.md) | Otimização de conteúdo | Sinaliza páginas com texto complexo que pode atrapalhar a compreensão da IA. | Fornece versões simplificadas geradas por IA de texto complexo, preservando o significado original. | Reescreve seções complexas na página, melhorando a legibilidade da IA. |
| [Adicionar Sumário](/help/dashboards/opportunities/add-table-of-contents.md) | GEO técnico | Detecta páginas que não têm organização estrutural clara ou cabeçalhos de navegação, dificultando a análise e o mapeamento do conteúdo para consultas do usuário pelos agentes de IA. | A sugere um Sumário estruturado com cabeçalhos vinculados por âncora que reflitam as seções principais da página. | Injeta um índice no HTML, melhorando a estrutura da página para que os modelos de IA possam extrair, mapear e citar seções relevantes com mais facilidade. |
| [Adicionar Resumos de Transcrição de Multimídia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | Otimização de conteúdo | Identifica páginas em que as informações principais são incorporadas em vídeo ou outras mídias sem transcrições ou resumos legíveis por máquina, tornando esse conteúdo difícil de ser usado pelos agentes de IA. Mostra URLs afetados e texto recomendado. | Recomenda resumos de transcrição gerados por IA com base na mídia e na página. | Insere resumos de transcrição no HTML para que o tráfego agêntrico receba texto legível por máquina (por exemplo, próximo ao vídeo relevante). |

### Ferramentas adicionais

A extensão de navegador [Verificador de visibilidade do conteúdo de IA](https://chromewebstore.google.com/detail/ai-content-visibility-che/jbjngahjjdgonbeinjlepfamjdmdcbcc) mostra quanto do conteúdo da sua página da web os LLMs conseguem acessar e o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, não exige licença ou configuração do produto.

Com um clique único, você pode avaliar a legibilidade por máquina de qualquer site. Você pode visualizar uma comparação lado a lado do que os agentes de IA veem em comparação com o que os usuários humanos veem e estimar quanto conteúdo poderia ser recuperado usando o LLM Optimizer. Acesse a página [A IA pode ler o seu site?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obter mais informações.

## Oportunidades detalhadas

Nas seções a seguir, é possível ver detalhes adicionais sobre cada oportunidade compatível com o recurso Otimização na borda.

### Recuperar visibilidade do conteúdo

Essa oportunidade sinaliza páginas em que o conteúdo principal está oculto para agentes de IA devido à renderização do lado do cliente. Para cada página identificada, ele mostra exatamente qual conteúdo está faltando na visualização do agente de IA, destaca as lacunas de visibilidade e permite aplicar as alterações diretamente para recuperar o conteúdo oculto. Ao implantar essa oportunidade com a opção Otimizar no Edge, uma versão pré-renderizada e otimizada para IA da página é disponibilizada aos agentes do usuário do LLM para que eles possam acessar o contexto completo sem executar o Javascript.
Isso garante que a página fique totalmente visível para os agentes de IA. Aprimoramentos adicionais são aplicados sobre o HTML pré-renderizado.

>[!IMPORTANT]
>Essa funcionalidade de pré-renderização se aplica automaticamente a todas as oportunidades apresentadas abaixo quando implantada com o recurso Otimização na borda, para garantir que a página esteja totalmente visível para os agentes de IA.

Consulte [Recuperar a visibilidade do conteúdo](/help/dashboards/opportunities/recover-content-visibility.md) para obter um passo a passo do painel, etapas de implantação e perguntas frequentes.

### Enriquecer páginas de detalhes do produto

Essa oportunidade se destina às páginas de detalhes do produto do Adobe Commerce, em que os compradores veem o contexto completo do produto por meio de experiências interativas da loja, mas os agentes de IA recebem apenas um instantâneo superficial do HTML. O Catalog Agent compara seu catálogo Commerce autorizado ao PDP visível ao agente, lista cada lacuna significativa (por exemplo, variantes ou especificações que nunca aparecem no HTML estático) e permite implantar uma resposta de borda somente de bot que restaura a paridade para rastreadores LLM sem alterar registros de catálogo ou interface humana.

Consulte [Enriquecer páginas de detalhes do produto](/help/dashboards/opportunities/enrich-product-detail-pages.md) para obter uma apresentação, etapas de implantação e perguntas frequentes do painel.

### Adicionar resumos compatíveis com LLM

Esta oportunidade identifica páginas de alto tráfego que podem se beneficiar de resumos concisos e pontos principais estruturados para que os LLMs possam entender rapidamente as solicitações na página. Para cada página, ele detecta onde um resumo é mais necessário e propõe resumos gerados por IA (e pontos-chave quando relevante) no nível da página ou da seção, com base no conteúdo existente. Ao implantar com a opção Otimizar no Edge, esse conteúdo é inserido na HTML que os agentes de IA recuperam, melhorando a precisão com que sua marca é representada nas respostas de IA.

Consulte [Adicionar Resumos amigáveis a LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) para obter mais detalhes sobre esta oportunidade.

### Adicionar perguntas frequentes relevantes

Essa oportunidade sinaliza páginas de alto tráfego nas quais o conteúdo adicional de perguntas e respostas pode corresponder melhor à intenção do usuário e às solicitações de detecção orientadas por IA. Para cada página, ela propõe blocos de perguntas frequentes gerados por IA vinculados ao seu conjunto de prompts e conteúdo na página. Com a opção Otimizar no Edge, essas Perguntas frequentes são inseridas no HTML, tornando sua página mais amigável para IA e aumentando a probabilidade de as respostas de IA refletirem diretamente suas orientações.

Consulte [Adicionar perguntas frequentes relevantes](/help/dashboards/opportunities/add-relevant-faqs.md) para obter uma apresentação do painel, etapas de implantação e perguntas frequentes.

### Simplificar conteúdo complexo

Essa oportunidade encontra páginas com parágrafos longos e complexos que podem reduzir a compreensão da IA. Para cada página que excede os limites de legibilidade, ela cria conteúdo gerado por IA que é mais simples e fácil de digitalizar, preservando o significado original. Quando implantado na borda, o conteúdo simplificado entregue ao tráfego agêntico ajuda os LLMs a interpretar e resumir o conteúdo com mais fidelidade.

Consulte [Simplificar conteúdo complexo](/help/dashboards/opportunities/simplify-complex-content.md) para obter uma apresentação do painel, etapas de implantação e perguntas frequentes.

### Adicionar sumário

Esta oportunidade detecta páginas que são difíceis de serem navegadas pelos agentes de IA, pois os cabeçalhos e a estrutura da seção não são claros ou estão ausentes. Para cada página afetada, ele propõe um índice estruturado com entradas vinculadas por âncora alinhadas às seções principais. Ao implantar com a opção Otimizar na Edge, esse índice é inserido no HTML para que os modelos possam mapear as consultas do usuário de forma mais confiável para as partes certas da página e citá-las.

Consulte [Adicionar sumário](/help/dashboards/opportunities/add-table-of-contents.md) para obter uma apresentação do painel, etapas de implantação e orientação sobre acesso antecipado.

### Adicionar Resumos de Transcrição de Multimídia

Essa oportunidade direciona as páginas em que informações importantes estão somente dentro da reprodução de vídeo, sem transcrições ou resumos de texto que os agentes de IA podem ler. Para cada página, ele recomenda transcrições geradas por IA e resumos curtos dos pontos principais da mídia. Com a opção Otimizar no Edge, esses resumos são adicionados à HTML como texto legível por máquina para que os agentes possam usar a mesma substância que os visitantes humanos recebem ao assistir ao vídeo.

Consulte [Adicionar resumos da transcrição de multimídia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) para obter uma apresentação do painel, etapas de implantação e perguntas frequentes.

## Otimização automática na borda

Em cada oportunidade, é possível visualizar, editar, implantar, exibir em tempo real e reverter as otimizações na borda.

>[!VIDEO](https://video.tv.adobe.com/v/3477989/?captions=por_br&learn=on&enablevpops)

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

## Recursos adicionais

Para obter detalhes adicionais sobre o recurso Otimizar no Edge, consulte a seguinte lista de reprodução [LLM Optimizer — Otimizar no Edge](https://www.youtube.com/playlist?list=PLzbVcr6JHocVSMWBCaCw4xxjQ_VFVvFh0).

## Perguntas frequentes

P: Os clientes em período de avaliação podem experimentar a Otimização na borda?

Sim, os clientes em período de avaliação podem acessar uma oportunidade de otimização e implementá-la em até 10 páginas. Por padrão, a oportunidade é Recuperar visibilidade do conteúdo, que permite que os agentes de IA acessem a versão completa do conteúdo da página.

P. Que tipo de LLMs são direcionados com o recurso Otimização na borda?

A lista de agentes de usuário a serem direcionados é definida por você durante o processo de integração.

<!--
Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.
-->

P. O que acontece se eu ainda não estiver integrado(a) ao recurso Otimização na borda?

Se você clicar em **Implantar otimizações** antes de concluir a instalação necessária, nenhuma informação será aplicada ao site. Em vez disso, uma caixa de diálogo pop-up solicita que você entre em contato com nossa equipe pelo email `llmo-at-edge@adobe.com` para obter assistência durante a integração. Até que a integração seja concluída, você ainda poderá explorar as oportunidades e sugestões detectadas, mas o fluxo de trabalho de implantação com um clique permanecerá inativo.

P: O que acontece quando o conteúdo é atualizado na origem?

Oferecemos a versão otimizada da sua página do cache, desde que a página de origem subjacente não tenha sido alterada. No entanto, quando a origem é alterada para **Recuperar Visibilidade do conteúdo**, nosso sistema é atualizado automaticamente para que os agentes de IA sempre recebam o conteúdo mais atualizado. Isso ocorre porque usamos configurações de TTL (low cache time to live) (por ordem de minutos) para que qualquer atualização de conteúdo em seu site acione uma nova otimização dentro dessa janela. Para oportunidades de conteúdo como **Adicionar Resumos Amigáveis a LLM**, o LLM Optimizer monitora as alterações na página de origem. Se uma alteração for detectada, pausaremos a otimização e a sinalizaremos para revisão humana para evitar o descompasso do conteúdo entre a página visível por agente e a página visível por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. O recurso Otimização na borda é somente para sites que usam o Adobe Edge Delivery Service (EDS)?

Não. O recurso Otimização na borda é independente da CDN e funciona com qualquer arquitetura de front-end, não apenas com as implantadas na pilha do Adobe EDS.

P: Como a pré-renderização do recurso Otimização na borda se diferencia da renderização tradicional do lado do servidor (SSR)?

Ambas resolvem problemas diferentes e podem trabalhar juntas. A SSR tradicional renderiza o conteúdo do lado do servidor, mas não inclui conteúdo carregado posteriormente no navegador. A pré-renderização do recurso Otimização na borda captura a página depois que o JavaScript e os dados do lado do cliente são carregados, produzindo a versão completa na borda da CDN. A SSR se concentra em melhorar a experiência humana, e o recurso Otimização na borda melhora a experiência da web para LLMs.

P. O Recover Visibilidade do conteúdo (ou seja, pré-renderização) está com cloaking? Parece que uma versão diferente da página está sendo disponibilizada para os agentes de IA.

Não. A pré-renderização garante que os agentes de IA possam ver o mesmo conteúdo que os visitantes humanos e os bots de SEO já veem. Muitos sites carregam conteúdo significativo com o JavaScript, que os agentes de IA típicos não executam, portanto, os agentes podem perder grandes partes da página. A pré-renderização produz um instantâneo estático que captura o texto completo para que os agentes recebam as mesmas informações que os humanos e mecanismos de pesquisa. Ele **restaura** a paridade de conteúdo para LLMs; não adiciona nem altera o conteúdo fatual.

P. E quanto a outras oportunidades de conteúdo, como Adicionar resumos amigáveis a LLM, em que uma nova cópia é exibida na página entregue aos agentes? Isso é camuflagem?

Não. Otimizar no Edge não apresenta informações que usuários humanos e rastreadores de SEO não podem acessar. O serviço reorganiza ou resume o conteúdo que já existe na página para que os agentes de IA possam interpretá-lo mais facilmente. Quando alguém segue um link de uma resposta do AI para o seu site, ainda é possível encontrar as mesmas informações subjacentes na página ativa.

P. O que acontece se eu implantar otimizações para alguns URLs em meu domínio, mas não todos?

Somente os URLs que você otimiza explicitamente são modificados. Para URLs com oportunidades implantadas, os agentes de IA recebem a versão otimizada. Para URLs sem oportunidades implantadas, nosso serviço simplesmente faz o proxy da página original como está, sem aplicar alterações ou armazená-la em nossa camada de cache de otimização. Isso garante que você possa implantar otimizações seletivamente sem afetar o restante do site.
