---
title: Oportunidades de otimização
description: Saiba como usar o painel de oportunidades para detectar automaticamente como seu site pode ser aprimorado para aumentar a visibilidade da marca.
feature: Opportunities
source-git-commit: c6e37395362262eb5fe8366473e76086e36d77e9
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Oportunidades de otimização

As oportunidades de otimização são insights detectados automaticamente que mostram onde o site e a presença externa podem ser aprimorados para aumentar a visibilidade da marca na pesquisa de IA.

Essas otimizações incluem correções na página (adição de conteúdo estruturado, canônicos ou resumos), ajustes técnicos (desbloqueio de rastreadores de IA ou resolução de erros) e influência no conteúdo em sites autorizados de terceiros. Lidar com essas oportunidades de otimização ajuda sua marca a ser representada com precisão e mais propensa a ser citada em respostas geradoras.

![Oportunidades de otimização](/help/dashboards/assets/oport.png)

## Painel de Oportunidades

As oportunidades de otimização apresentadas no painel são priorizadas com base em lacunas do player, tópicos de tendência e dados de desempenho e apresentadas como uma lista. Você pode pesquisar uma oportunidade específica usando o campo de pesquisa. Além disso, as oportunidades são agrupadas por tags e você pode clicar diretamente em uma tag para mostrar todas as oportunidades agrupadas sob essa tag.

Clicar em **Detalhes** abrirá uma janela separada onde mais informações e orientações adicionais serão fornecidas.

## Oportunidades suportadas

Apresentamos abaixo uma tabela de oportunidades aceitas no momento:

| Oportunidade | Tipo | Problemas identificados | Corrigir sugestões |
|---------|----------|----------|----------|
| Resumir parágrafos longos | Conteúdo (no local) | Detecta parágrafos que excedem os limites de comprimento recomendados. Mostra URLs afetados e trechos de texto superdimensionados. | Crie resumos ou divida textos longos em seções menores e digitalizáveis. |
| Conteúdo estruturado recomendado (Perguntas frequentes) | Conteúdo (no local) | Detecta prompts de alta popularidade sem entradas de FAQ correspondentes. Mostra prompts relacionados, categorias e URLs afetados. | Adicione blocos de esquema de perguntas frequentes com respostas concisas para corresponder a consultas comuns. |
| Detectar Hreflang Ausente | Conteúdo (no local) | Sinaliza páginas sem atributos hreflang. Fornece URLs afetados e cobertura esperada por idioma/região. | Implemente tags hreflang para indicar as versões localizadas corretas. |
| Detectar Canônicos Ausentes | Conteúdo (no local) | Procura páginas sem tags canônicas ou com tags conflitantes. Lista URLs e duplicatas afetados. | Adicione tags canônicas apontando para a versão preferida de cada página. Garanta um uso consistente entre as variantes. |
| Detectar cabeçalhos vazios | Conteúdo (no local) | Sinaliza páginas em que as tags de cabeçalho existem, mas não contêm texto. Mostra o URL e o local das tags vazias. | Adicione texto descritivo a cabeçalhos que refletem o conteúdo abaixo deles. |
| Detectar cabeçalhos duplicados | Conteúdo (no local) | Varre tags de cabeçalho e sinalizadores do HTML e cabeçalhos repetidos. Mostra URLs afetados e trechos de texto duplicados. | Revise os cabeçalhos para serem exclusivos e mantenha a hierarquia (H1 → H2 → H3). Mesclar ou renomear seções duplicadas. |
| Detectar tráfego de agente bloqueado | GEO técnico | Analisa logs de CDN para solicitações bloqueadas de agentes de IA conhecidos (por exemplo, GPTBot, PerplexityBot). Os relatórios afetavam URLs e agentes. | Atualize o robots.txt ou as configurações do servidor para permitir o acesso a rastreadores de IA compatíveis, quando apropriado. |
| Detectar problemas 404s / 403s / 5xx | GEO técnico | Monitora logs de CDN para obter respostas de erro. Frequência de relatórios, URLs afetados e perda estimada de ocorrências. | Corrigir links corrompidos, atualizar permissões e resolver problemas do lado do servidor para que o conteúdo principal retorne 200 respostas. |
| Recuperar visibilidade do conteúdo (acesso antecipado) | GEO técnico | Sinaliza páginas em que o conteúdo crítico está oculto dos agentes de IA. Mostra as URLs afetadas e o conteúdo esperado que pode ser recuperado. | Pré-renderizar as páginas para que mais conteúdo esteja disponível para os agentes de IA sem execução do JavaScript. |

### Recuperar oportunidade de visibilidade de conteúdo {#recover-contet}

Como dito acima, a oportunidade de visibilidade de conteúdo sinaliza as páginas em que o conteúdo principal é perdido para os agentes de IA devido à renderização do lado do cliente. Para cada página identificada, ele mostra exatamente qual conteúdo está faltando na visualização do agente de IA, ajudando a apontar as lacunas de visibilidade. Ele também é compatível com um recurso de pré-renderização baseado em borda que pode fornecer mais conteúdo HTML para tráfego agêntico sem exigir alterações no Content Management System (CMS). No momento, essa funcionalidade está em Acesso antecipado e requer configuração da equipe do LLM Optimizer. Contate `llmo-at-edge@adobe.com` para ativar a oportunidade de visibilidade de conteúdo.

### Ferramentas adicionais

O [verificador de visibilidade LLM](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) é uma extensão do Chrome que permite ver exatamente o quanto os LLMs de conteúdo de página da Web podem acessar e também o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, ele não requer licença ou configuração do produto. Com um único clique, os usuários podem avaliar a legibilidade automática de qualquer site, visualizar uma comparação lado a lado do que os agentes de IA veem em relação ao que os usuários humanos veem. Além disso, o estima a quantidade de conteúdo que pode ser recuperada usando o LLM Optimizer.
