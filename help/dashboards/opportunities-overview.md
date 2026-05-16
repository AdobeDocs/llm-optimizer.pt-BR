---
title: Oportunidades de otimização
description: Saiba como usar o painel de oportunidades para detectar automaticamente como seu site pode ser aprimorado para aumentar a visibilidade da marca.
feature: Opportunities
autotag-review: '2026-05-15T17:53:48.623Z'
TQID: 'https://experienceleague.adobe.com/FAbQhzuyT-kIitIaoVQ47dam-TpN-deU5Vbo1nmK5CA'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1227
ht-degree: 31%

---


# Oportunidades de otimização

As oportunidades de otimização são insights detectados automaticamente que mostram onde o site e a presença externa podem ser aprimorados para aumentar a visibilidade da marca em pesquisas com IA.

Essas otimizações incluem correções na página (adição de conteúdo estruturado, links canônicos ou resumos), ajustes técnicos (desbloqueio de rastreadores de IA ou resolução de erros) e influência no conteúdo de sites de terceiros com autoridade. Aproveitar essas oportunidades de otimização ajuda sua marca a ser representada com precisão e aumenta a probabilidade de ser citada em respostas generativas.

![Oportunidades de otimização](/help/dashboards/assets/oport.png)

## Painel de oportunidades

As oportunidades de otimização apresentadas no painel são priorizadas com base nas lacunas em relação aos concorrentes, nos tópicos em alta e nos dados de desempenho, e apresentadas em forma de lista. Você pode procurar uma oportunidade específica usando o campo de pesquisa. Além disso, as oportunidades são agrupadas por tags e você pode clicar diretamente em uma tag para mostrar todas as oportunidades agrupadas sob ela.

Clique em **Detalhes** para abrir uma janela separada onde mais informações e orientações adicionais serão fornecidas.

## Oportunidades aceitas

Apresentamos abaixo uma tabela de oportunidades aceitas no momento:

| Oportunidade | Tipo | Problemas identificados | Sugestões de correção |
|---------|----------|----------|----------|
| [Adicionar Resumos amigáveis a LLM](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | Conteúdo (no local) | O código identifica páginas de alto tráfego que não têm resumos concisos e pontos-chave estruturados no nível da página ou da seção, dificultando a verificação e a interpretação das declarações de marca pelos agentes de IA. Mostra os URLs afetados e onde os resumos são recomendados. | Revise resumos gerados por IA e pontos-chave com base no conteúdo existente e implante na borda da CDN com a opção Otimizar no Edge para que os agentes recebam um contexto mais claro e verificável. |
| [Adicionar perguntas frequentes relevantes](/help/dashboards/opportunities/add-relevant-faqs.md) | Conteúdo (no local) | O código identifica páginas de alto tráfego que não têm conteúdo estruturado de perguntas e respostas alinhado ao seu conjunto de prompts, dificultando aos agentes de IA corresponder as perguntas do usuário à sua página. Mostra os URLs afetados e onde as perguntas frequentes são recomendadas. | Revise o conteúdo das perguntas frequentes gerado por IA e alinhado à intenção, com base no material da página existente, e implante na borda da CDN com a opção Otimizar na Edge para que os agentes recebam um contexto de perguntas e respostas mais claro. |
| [Adicionar Resumos de Transcrição de Multimídia](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | Conteúdo (no local) | Identifica páginas em que as informações principais são incorporadas em vídeo ou outras mídias sem transcrições ou resumos legíveis por máquina, tornando esse conteúdo difícil de ser usado pelos agentes de IA. Mostra URLs afetados e texto recomendado. | Revise os resumos de transcrição gerados por IA com base na mídia e página e implante na borda da CDN com Otimizar no Edge para que os agentes recebam texto legível por máquina (por exemplo, próximo ao vídeo relevante). |
| [Tráfego bloqueado por robots.txt](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | GEO técnico | Analisa o arquivo robots.txt para regras que bloqueiam seletivamente os agentes de IA de conteúdos que de outra forma seriam acessíveis publicamente. Os relatórios afetavam URLs e agentes bloqueados. | Atualize o arquivo robots.txt para permitir o acesso a rastreadores de IA compatíveis, quando apropriado. |
| [Erros de Tráfego de Agente](/help/dashboards/opportunities/agentic-traffic-errors.md) | GEO técnico | Monitora os logs de CDN para respostas de erro 404, 403 e 5xx retornadas aos agentes de IA. Os relatórios afetavam as URLs e o total de ocorrências perdidas. | Corrigir links corrompidos, atualizar permissões e resolver problemas do lado do servidor para que o conteúdo principal retorne 200 respostas. |
| [Simplificar conteúdo complexo](/help/dashboards/opportunities/simplify-complex-content.md) | Conteúdo (no local) | O código identifica páginas de alto tráfego em que a cópia complexa ou densa fica abaixo dos limites de legibilidade, dificultando a interpretação das informações principais pelos agentes de IA. Mostra os URLs afetados e onde o texto simplificado é recomendado. | Revise o Texto aprimorado gerado pela IA com base no conteúdo da página existente e implante na borda da CDN com a opção Otimizar no Edge para que os agentes recebam passagens mais claras e fáceis de digitalizar. |
| [Recuperar Visibilidade do conteúdo](/help/dashboards/opportunities/recover-content-visibility.md) | GEO técnico | Sinaliza páginas em que o conteúdo crítico está oculto de agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Pré-renderizar as páginas na camada de CDN usando Otimizar no Edge para que mais conteúdo fique disponível para agentes de IA sem execução do JavaScript. |
| [Adicionar Sumário](/help/dashboards/opportunities/add-table-of-contents.md) | GEO técnico | Detecta páginas que não têm organização estrutural clara ou cabeçalhos de navegação, dificultando a análise e o mapeamento do conteúdo para consultas do usuário pelos agentes de IA. Mostra os URLs afetados e onde um índice estruturado é recomendado. | Revise o índice estruturado sugerido com cabeçalhos vinculados por âncora que refletem as seções principais da página e implante na borda do CDN com Otimizar no Edge para que um índice seja inserido no HTML, melhorando a estrutura da página para que os modelos possam extrair, mapear e citar seções relevantes com mais facilidade. |
| [Análise da Wikipédia](/help/dashboards/opportunities/wikipedia-analysis.md) | Fora do local | Analisa a página da Wikipédia de sua empresa em relação aos concorrentes do setor em referências, seções, duração do conteúdo, imagens e integridade da caixa de informações. Identifica lacunas específicas em que sua página fica abaixo dos referenciais do setor. | Revise as recomendações estratégicas geradas pela IA para melhorar a presença na Wikipédia, incluindo a adição de referências, o enriquecimento de sua caixa de informações, a expansão de seções e a melhoria da qualidade do artigo. |
| [Análise do YouTube Sentimento (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa vídeos do YouTube citados para o prompt de Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. Aparece somente quando os vídeos do YouTube são detectados como citações para o conjunto de prompts. | Revise as recomendações priorizadas para melhorar a percepção da marca em todo o conteúdo do YouTube, incluindo ações sugeridas e as equipes responsáveis pela implementação. |
| [Reddit Sentimento Analysis (Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa as threads do Reddit citadas para o prompt do Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. Aparece somente quando as threads do Reddit são detectadas como citações para o seu conjunto de prompt. | Revise as recomendações priorizadas para melhorar a percepção da marca em todo o conteúdo do Reddit, incluindo ações sugeridas e as equipes responsáveis por implementá-las. |
| [Análise de Sentimento citada (Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa URLs mais citados detectados para o prompt do Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. | Revise as recomendações priorizadas para melhorar a percepção da marca nas páginas que os sistemas de IA citam mais ao responder às solicitações sobre sua marca. |
| [Enriquecer Catálogo de Produtos (Beta)](/help/dashboards/opportunities/enrich-product-catalog.md) | Conteúdo (no local), Adobe Commerce | Identifica os produtos do catálogo do Commerce cujos nomes ou descrições são muito genéricos, tecnicamente densos ou ambíguos para serem interpretados pelos LLMs. Mostra PDPs avaliados, contexto de tráfego agêntrico e enriquecimentos narrativos gerados por IA. | Revise e edite os nomes e as descrições de produtos propostos e implante otimizações para publicar atualizações diretamente no catálogo do Adobe Commerce (com reversão de Sugestões fixas). |
| [Enriquecer Páginas De Detalhes Do Produto](/help/dashboards/opportunities/enrich-product-detail-pages.md) | GEOGRAFIA técnica, Adobe Commerce | Para as vitrines do Adobe Commerce, compara os dados completos do catálogo ao que os agentes de IA podem acessar em cada página de detalhes do produto; mostra PDPs em que as variantes, as especificações, os atributos e os campos de catálogo relacionados estão ausentes no HTML visível para agentes, priorizados pelo tráfego de agente. | Destaca as informações recuperáveis do catálogo que estão faltando na visualização do agente e por que elas são importantes para a descoberta de produtos orientada por LLM; implante com a opção Otimizar no Edge para fornecer um instantâneo do HTML totalmente pré-renderizado e compatível com IA para agilizar o tráfego na borda da CDN, para que os agentes recebam um contexto de produto avançado do seu catálogo sem alterações no CMS ou catálogo. |

## Otimização automática {#auto-optimization}

A otimização automática permite a implantação de otimizações recomendadas com um só clique, reduzindo as tarefas manuais e o tempo necessário para obter resultados. As otimizações podem ser aplicadas na fonte de conteúdo ou na borda da CDN. A otimização automática na borda está disponível atualmente em acesso antecipado para algumas oportunidades. Para obter mais detalhes, consulte a página do recurso [Otimização na borda](/help/dashboards/optimize-at-edge/overview.md).

<!--
### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.
-->

### Ferramentas adicionais

O [Verificador de visibilidade de LLM](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) é uma extensão do Chrome que permite ver exatamente quanto do conteúdo da sua página web os LLMs podem acessar e também o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, ele não exige licença ou configuração do produto. Com um único clique, os usuários podem avaliar a legibilidade por máquina de qualquer site e visualizar uma comparação lado a lado do que os agentes de IA veem em relação ao que os usuários humanos veem. Além disso, ele estima quanto conteúdo poderia ser recuperado usando o LLM Optimizer.

<!--
| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |
-->
