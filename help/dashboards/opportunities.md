---
title: Oportunidades de otimização
description: Saiba como usar o painel de oportunidades para detectar automaticamente como seu site pode ser aprimorado para aumentar a visibilidade da marca.
feature: Opportunities
source-git-commit: 1f665bd14349c15d92f8274742606abcf9b02000
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

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
| Conteúdo estruturado recomendado (Perguntas frequentes) | Conteúdo (no local) | Detecta prompts de alta popularidade que não possuam entradas correspondentes na seção de Perguntas frequentes. Mostra prompts relacionados, categorias e URLs afetados. | Adicione blocos de esquema de perguntas frequentes com respostas concisas para corresponder a consultas comuns. |
| Detectar hreflang ausente | Conteúdo (no local) | Sinaliza páginas sem atributos hreflang. Fornece URLs afetados e cobertura esperada por idioma/região. | Implemente tags hreflang para indicar as versões localizadas corretas. |
| Detectar canônicos ausentes | Conteúdo (no local) | Procura páginas sem tags canônicas ou com tags conflitantes. Lista URLs afetados e duplicados. | Adicione tags canônicas apontando para a versão preferida de cada página. Garanta um uso consistente entre as variantes. |
| Detectar tráfego agêntico bloqueado | GEO técnico | Analisa logs da CDN em busca de solicitações bloqueadas de agentes de IA conhecidos (por exemplo, GPTBot, PerplexityBot). Os relatórios afetaram URLs e agentes. | Atualize o arquivo robots.txt ou as configurações do servidor para permitir o acesso de rastreadores de IA compatíveis, quando apropriado. |
| Detectar problemas 404s/403s/5xx | GEO técnico | Monitora os registros da CDN em busca de respostas de erro. Frequência de relatórios, URLs afetados e perda estimada de ocorrências. | Corrigir links corrompidos, atualizar permissões e resolver problemas do lado do servidor para que o conteúdo principal retorne 200 respostas. |
| Recuperar a visibilidade do conteúdo (acesso antecipado) | GEO técnico | Sinaliza páginas em que o conteúdo crítico está oculto de agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Pré-renderize as páginas para que haja mais conteúdo sem execução de JavaScript disponível para os agentes de IA. |

## Otimização automática {#auto-optimization}

A otimização automática permite a implantação de otimizações recomendadas com um só clique, reduzindo as tarefas manuais e o tempo necessário para obter resultados. As otimizações podem ser aplicadas na fonte de conteúdo ou na borda da CDN. A otimização automática na borda está disponível atualmente em acesso antecipado para algumas oportunidades. Para obter mais detalhes, consulte a página do recurso [Otimização na borda](/help/dashboards/optimize-at-edge.md).

<!--### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.-->

### Ferramentas adicionais

O [Verificador de visibilidade de LLM](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) é uma extensão do Chrome que permite ver exatamente quanto do conteúdo da sua página web os LLMs podem acessar e também o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, ele não exige licença ou configuração do produto. Com um único clique, os usuários podem avaliar a legibilidade por máquina de qualquer site e visualizar uma comparação lado a lado do que os agentes de IA veem em relação ao que os usuários humanos veem. Além disso, ele estima quanto conteúdo poderia ser recuperado usando o LLM Optimizer.
