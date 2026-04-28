---
title: Oportunidades de otimização
description: Saiba como usar o painel de oportunidades para detectar automaticamente como seu site pode ser aprimorado para aumentar a visibilidade da marca.
feature: Opportunities
source-git-commit: 96bb7d73c8cdd2151df12030bbf28723857c78e1
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 58%

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
| Resumir parágrafos longos | Conteúdo (no local) | Detecta parágrafos que excedem os limites de comprimento recomendados. Mostra URLs afetados e trechos de texto excessivamente longos. | Crie resumos ou divida textos longos em seções menores analisáveis. |
| Conteúdo estruturado recomendado | Conteúdo (no local) | Detecta prompts de alta popularidade que não possuam entradas correspondentes na seção de Perguntas frequentes. Mostra prompts relacionados, categorias e URLs afetados. | Adicione blocos de esquema de perguntas frequentes com respostas concisas para corresponder a consultas comuns. |
| [Tráfego bloqueado por robots.txt](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | GEO técnico | Analisa o arquivo robots.txt para regras que bloqueiam seletivamente os agentes de IA de conteúdos que de outra forma seriam acessíveis publicamente. Os relatórios afetavam URLs e agentes bloqueados. | Atualize o arquivo robots.txt para permitir o acesso a rastreadores de IA compatíveis, quando apropriado. |
| [Erros de Tráfego de Agente](/help/dashboards/opportunities/agentic-traffic-errors.md) | GEO técnico | Monitora os logs de CDN para respostas de erro 404, 403 e 5xx retornadas aos agentes de IA. Os relatórios afetavam as URLs e o total de ocorrências perdidas. | Corrigir links corrompidos, atualizar permissões e resolver problemas do lado do servidor para que o conteúdo principal retorne 200 respostas. |
| Simplificar conteúdo complexo | Conteúdo (no local) | Identifica parágrafos longos e complexos que excedem os limites de legibilidade que podem reduzir a compreensão da IA. | Pré-renderize as páginas para que haja mais conteúdo sem execução de JavaScript disponível para os agentes de IA. |
| [Recuperar Visibilidade do conteúdo](/help/dashboards/opportunities/recover-content-visibility.md) | GEO técnico | Sinaliza páginas em que o conteúdo crítico está oculto de agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Pré-renderizar as páginas na camada de CDN usando Otimizar no Edge para que mais conteúdo fique disponível para agentes de IA sem execução do JavaScript. |
| [Análise da Wikipédia](/help/dashboards/opportunities/wikipedia-analysis.md) | Fora do local | Analisa a página da Wikipédia de sua empresa em relação aos concorrentes do setor em referências, seções, duração do conteúdo, imagens e integridade da caixa de informações. Identifica lacunas específicas em que sua página fica abaixo dos referenciais do setor. | Revise as recomendações estratégicas geradas pela IA para melhorar a presença na Wikipédia, incluindo a adição de referências, o enriquecimento de sua caixa de informações, a expansão de seções e a melhoria da qualidade do artigo. |
| [Análise do YouTube Sentimento (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa vídeos do YouTube citados para o prompt de Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. Aparece somente quando os vídeos do YouTube são detectados como citações para o conjunto de prompts. | Revise as recomendações priorizadas para melhorar a percepção da marca em todo o conteúdo do YouTube, incluindo ações sugeridas e as equipes responsáveis pela implementação. |
| [Reddit Sentimento Analysis (Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa as threads do Reddit citadas para o prompt do Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. Aparece somente quando as threads do Reddit são detectadas como citações para o seu conjunto de prompt. | Revise as recomendações priorizadas para melhorar a percepção da marca em todo o conteúdo do Reddit, incluindo ações sugeridas e as equipes responsáveis por implementá-las. |
| [Análise de Sentimento citada (Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | Fora do site, Social e Comunidade | Analisa URLs mais citados detectados para o prompt do Presença da marca definido para menções de marca, sentimento, participação de voz e tópicos recorrentes. | Revise as recomendações priorizadas para melhorar a percepção da marca nas páginas que os sistemas de IA citam mais ao responder às solicitações sobre sua marca. |

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
