---
title: Análise de Sentimento citada
description: Saiba como o LLM Optimizer analisa os URLs mais citados para exibir recomendações que melhoram a percepção e a visibilidade de sua marca nos resultados de Pesquisas com IA.
feature: Opportunities
autotag-review: '2026-05-15T17:39:50.086Z'
TQID: 'https://experienceleague.adobe.com/ZqgWup29QoQ-j0fDM6DqhGpzRqscg1f-fdXHTMN9fIk'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1030
ht-degree: 1%

---


# Análise de Sentimento citada

Quando os sistemas de IA respondem a perguntas sobre sua marca, eles dependem de um conjunto de URLs mais citados: páginas da Web de terceiros que são frequentemente referenciadas em respostas geradas por IA. A forma como sua marca é retratada nessas páginas molda diretamente como os sistemas de IA a representam para os usuários.

A oportunidade Análise de Sentimento citada analisa os URLs mais citados detectados para prompts em seu conjunto de prompts do painel do Presença da marca. Ele avalia menções de marca, sentimentos, participações de voz e tópicos recorrentes nessas páginas. Posteriormente, ele apresenta recomendações priorizadas para melhorar como sua marca é percebida nos sistemas de IA de conteúdo que mais dependem.

Ele mostra quatro métricas principais:

- **Páginas analisadas** — Número de páginas da Web citadas examinadas para menções de marca e sentimentos.
- **Páginas ignoradas** — Número de páginas que não puderam ser analisadas (por exemplo, devido a restrições de acesso).
- **Menções de marca (páginas)** — Com que frequência sua marca é mencionada nas páginas analisadas.
- **sentimento geral (páginas)** — sentimento agregado em direção à sua marca nas páginas analisadas.

>[!NOTE]
>A Análise de Sentimento citada está atualmente na versão beta. Os recursos e a disponibilidade podem mudar à medida que a capacidade continua a se desenvolver.

![Painel de Análise de Sentimento citado](/help/dashboards/opportunities/assets/cited-sentiment-overview.png)

## Como funciona

O LLM Optimizer identifica os URLs mais citados que aparecem nas respostas geradas pela IA para prompts no conjunto de prompts do painel do Presença da marca. Ele analisa essas páginas para menções de marca, sentimentos, participações de voz e citações de IA. Ele compara o desempenho de sua marca com o desempenho de concorrentes do mercado, identifica tópicos recorrentes e gera recomendações para resolver lacunas de percepção nas páginas mais importantes para os sistemas de IA.

Se nenhum URL citado for detectado para os prompts em seu conjunto de prompts, esta oportunidade não aparecerá em seu painel.

Os resultados são exibidos em duas guias: **Sugestões** e **Desempenho**.

## Sugestões

Esta guia mostra recomendações para melhorar a percepção da sua marca em URLs mais citados. As sugestões são organizadas em três subguias: **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**.

![Guia Sugestões](/help/dashboards/opportunities/assets/cited-sentiment-suggestions.png)

A tabela de sugestões inclui as seguintes colunas:

- **Sugestão** — a melhoria recomendada para resolver uma lacuna de percepção.
- **Prioridade** — Nível de urgência (Crítico, Alto, Medium, Baixo).
- **Itens de Ação** — Abre um painel com etapas específicas para implementar a recomendação, incluindo as equipes responsáveis.

Expandir uma sugestão revela uma seção **Análise de IA** com:

- **Por que isso precisa de melhoria** — uma explicação da lacuna de percepção identificada, incluindo quais URLs citadas estão sub-representando sua marca e contexto competitivo.
- **Como melhorar** — Orientação específica sobre ações de alcance, criação de conteúdo ou parceria para resolver a lacuna.
- **Resultado Esperado** — O resultado antecipado da implementação da recomendação.

## Desempenho

A guia **Desempenho** fornece uma análise detalhada de como a sua marca está se saindo nas páginas mais citadas. Está organizado em quatro seções.

### Cenário do mercado

Compara o desempenho de sua marca com as marcas associadas e os concorrentes do mercado, com base nas menções nas páginas citadas.

![Cenário do mercado](/help/dashboards/opportunities/assets/cited-sentiment-landscape.png)

Ele mostra:

- **Menções de marca em páginas** — sua participação de voz versus marcas associadas e concorrentes de mercado.
- **Rastreamento de Mercado** — Um gráfico filtrável onde você pode selecionar até cinco marcas de concorrentes para comparar o participação de voz nas páginas analisadas.

### Análise de sentimentos

Rastreia a percepção da marca nas páginas analisadas com um gráfico **Distribuição de Sentimentos** mostrando a divisão de porcentagem de sentimentos favoráveis, neutros e desfavoráveis entre páginas.

![Análise de Sentimento](/help/dashboards/opportunities/assets/cited-sentiment-distribution.png)

### Páginas

Uma tabela detalhada das páginas da Web citadas analisadas com as seguintes colunas:

- **Página** — URL da página analisada.
- **Menções de marca** — Contagem de suas menções de marca versus o total de menções na página.
- **Participação de voz** — a participação da sua marca em menções relativas a todas as marcas mencionadas.
- **Cinco marcas principais** — as marcas mais mencionadas na página.
- **Sentimento** — sentimento geral em direção à sua marca na página.
- **Citações de IA** — Número de respostas de IA que citaram esta página.

### Assuntos

Uma tabela de tópicos recorrentes identificados nas páginas analisadas, mostrando:

- **Tópico** — O tema ou assunto recorrente identificado.
- **Menções de marca** — Número de menções de marca associadas ao tópico.
- **Sentimento** — sentimento geral associado ao tópico.

Clicar em **Detalhes** em qualquer tópico abre um detalhamento com um resumo de análise e as páginas de origem da contribuição.

## Experimente na demonstração

Veja a oportunidade Análise de Sentimentos Citados em ação usando o ambiente de demonstração Frescopa - [Exibir Análise de Sentimentos Citados na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/cited-analysis/d3a8b217-9f4c-4e88-a612-6b7f91e5c044?siteId=frescopa-demo).

## Perguntas frequentes

**Por que os URLs mais citados são importantes para a Pesquisa com IA?**

Os URLs mais citados são as páginas de terceiros para as quais os sistemas de IA fazem referência com mais frequência ao gerar respostas sobre sua marca. O sentimento e o enquadramento nessas páginas têm uma influência direta e desmedida sobre como a IA representa sua marca, mais do que as páginas que são raramente citadas. Melhorar a forma como sua marca é retratada nessas páginas específicas é uma das ações de maior aproveitamento que você pode realizar para a visibilidade da IA.

**Por que esta oportunidade não está sendo mostrada no meu painel?**

Essa oportunidade só aparece quando URLs citados são detectados para prompts no conjunto de prompts do painel do Presença da marca. Se nenhum URL citado tiver sido identificado para esses prompts, a oportunidade não será exibida.

**O que significa Páginas Ignoradas?**

Páginas ignoradas são URLs citados que não puderam ser analisados, normalmente porque a página está atrás de um paywall, requer autenticação ou bloqueia o acesso automatizado. Essas páginas são contadas, mas excluídas da análise de sentimento e menção de marca.

**O que é o Participação de voz?**

Participação de voz é a porcentagem da sua marca no total de menções de marca em uma determinada página ou em todas as páginas analisadas, em relação a todas as outras marcas mencionadas.

**O que são Citações de IA?**

As citações de IA mostram quantas respostas de IA citaram uma determinada página. As contagens mais altas de citação de IA indicam que a página está sendo usada ativamente pelos sistemas de IA ao gerar respostas sobre tópicos relacionados, tornando o sentimento nessas páginas especialmente importante para a representação de IA da sua marca.

**Como os concorrentes do mercado são identificados?**

Os concorrentes são identificados automaticamente com base no setor da sua marca e nas marcas comencionadas com mais frequência nas páginas analisadas. Você também pode selecionar manualmente até cinco marcas para comparação no gráfico Rastreamento de mercado.

**Com que frequência a análise é atualizada?**

A análise reflete os URLs citados detectados até a data mostrada no cabeçalho do painel. Revise a oportunidade depois de implementar as recomendações para rastrear as alterações no sentimento e no participação de voz.
