---
title: Oportunidades de otimização
description: Esta é a visão geral do artigo.
source-git-commit: e35ddb9b055d2f974fd94b3a21e13e92d05c8799
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# Oportunidades de otimização

As oportunidades de otimização são insights detectados automaticamente que mostram onde o site e a presença externa podem ser aprimorados para aumentar a visibilidade da marca na pesquisa de IA. Essas otimizações incluem correções na página (adição de conteúdo estruturado, canônicos ou resumos), ajustes técnicos (desbloqueio de rastreadores de IA ou resolução de erros) e influência no conteúdo em sites autorizados de terceiros. Lidar com essas oportunidades de otimização ajuda sua marca a ser representada com precisão e mais propensa a ser citada em respostas geradoras.

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
| Detectar Canônicos Ausentes | Conteúdo (no local) | Detecta parágrafos que excedem os limites de comprimento recomendados. Mostra URLs afetados e trechos de texto superdimensionados. | Crie resumos ou divida textos longos em seções menores e digitalizáveis. |
| Detectar cabeçalhos vazios | Conteúdo (no local) | Sinaliza páginas em que as tags de cabeçalho existem, mas não contêm texto. Mostra o URL e o local das tags vazias. | Adicione texto descritivo a cabeçalhos que refletem o conteúdo abaixo deles. |
| Detectar cabeçalhos duplicados | Conteúdo (no local) | Varre tags de cabeçalho e sinalizadores do HTML e cabeçalhos repetidos. Mostra URLs afetados e trechos de texto duplicados. | Revise os cabeçalhos para serem exclusivos e mantenha a hierarquia (H1 → H2 → H3). Mesclar ou renomear seções duplicadas. |
| Detectar tráfego de agente bloqueado | GEO técnico | Analisa logs de CDN para solicitações bloqueadas de agentes de IA conhecidos (por exemplo, GPTBot, PerplexityBot). Os relatórios afetavam URLs e agentes. | Atualize o robots.txt ou as configurações do servidor para permitir o acesso a rastreadores de IA compatíveis, quando apropriado. |
| Detectar problemas 404s / 403s / 5xx | GEO técnico | Monitora logs de CDN para obter respostas de erro. Frequência de relatórios, URLs afetados e perda estimada de ocorrências. | Corrigir links corrompidos, atualizar permissões e resolver problemas do lado do servidor para que o conteúdo principal retorne 200 respostas. |
