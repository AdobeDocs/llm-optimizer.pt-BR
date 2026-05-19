---
title: Análise de sentimentos de citações
description: Saiba como o LLM Optimizer analisa os URLs mais citados para exibir recomendações que melhoram a percepção e a visibilidade da sua marca nos resultados de pesquisa com IA.
feature: Opportunities
autotag-review: '2026-05-15T17:39:50.086Z'
TQID: 'https://experienceleague.adobe.com/ZqgWup29QoQ-j0fDM6DqhGpzRqscg1f-fdXHTMN9fIk'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1030
ht-degree: 100%

---


# Análise de sentimentos de citações

Quando os sistemas de IA respondem a perguntas sobre sua marca, eles dependem de um conjunto de URLs mais citados: páginas da web de terceiros que são frequentemente referenciadas em respostas geradas por IA. A forma como sua marca é retratada nessas páginas define diretamente como os sistemas de IA a representam para os usuários.

A oportunidade de Análise de sentimentos citados analisa os URLs mais citados detectados para prompts em seu conjunto de prompts do painel Presença da marca. Ela avalia menções de marca, sentimentos, participação de voz e tópicos recorrentes nessas páginas. Em seguida, apresenta recomendações priorizadas para melhorar a percepção da sua marca no conteúdo em que os sistemas de IA mais se baseiam.

Mostra quatro métricas principais:

- **Páginas analisadas**: número de páginas da web citadas examinadas para menções de marca e sentimentos.
- **Páginas ignoradas**: número de páginas que não puderam ser analisadas (por exemplo, devido a restrições de acesso).
- **Menções de marca (páginas)**: com que frequência sua marca é mencionada nas páginas analisadas.
- **Sentimento geral (páginas)**: sentimento agregado em relação à sua marca nas páginas analisadas.

>[!NOTE]
>A Análise de sentimentos citados está atualmente em versão beta. As funcionalidades e a disponibilidade podem mudar à medida que o recurso for desenvolvido.

![Painel de Análise de sentimentos citados](/help/dashboards/opportunities/assets/cited-sentiment-overview.png)

## Como funciona

O LLM Optimizer identifica os URLs mais citados que aparecem nas respostas geradas por IA para prompts no conjunto de prompts do painel do Presença da marca. Ele analisa essas páginas em relação a menções de marca, sentimentos, participações de voz e citações de IA. Ele compara o desempenho da sua marca com o dos concorrentes de mercado, identifica tópicos recorrentes e gera recomendações para resolver lacunas de percepção nas páginas mais importantes para os sistemas de IA.

Se nenhum URL citado for detectado nos prompts em seu conjunto de prompts, esta oportunidade não aparece no painel.

Os resultados são exibidos em duas guias: **Sugestões** e **Desempenho**.

## Sugestões

Esta guia mostra recomendações para melhorar a percepção da marca nos URLs mais citados. As sugestões são organizadas em três subguias: **Sugestões atuais**, **Sugestões fixas** e **Sugestões ignoradas**.

![Guia Sugestões](/help/dashboards/opportunities/assets/cited-sentiment-suggestions.png)

A tabela de sugestões inclui as seguintes colunas:

- **Sugestão** — A melhoria recomendada para resolver uma lacuna de percepção.
- **Prioridade**: nível de urgência (Crítico, Alto, Médio, Baixo).
- **Itens de ação**: abre um painel com etapas específicas para implementar a recomendação, incluindo as equipes responsáveis.

Expandir uma sugestão revela uma seção **Análise de IA** com:

- **Por que isso precisa ser melhorado**: uma explicação da falta de percepção identificada, incluindo quais URLs citados estão sub-representando sua marca e contexto competitivo.
- **Como melhorar**: orientação específica sobre ações de alcance, criação de conteúdo ou parceria para resolver a lacuna.
- **Resultado esperado**: o resultado antecipado da implementação da recomendação.

## Desempenho

A guia **Desempenho** fornece uma análise detalhada de como a sua marca está se saindo nas páginas mais citadas. Está organizada em quatro seções.

### Cenário do mercado

Compara o desempenho da sua marca com as marcas associadas e os concorrentes do mercado, com base nas menções nas páginas citadas.

![Cenário do mercado](/help/dashboards/opportunities/assets/cited-sentiment-landscape.png)

Ele mostra:

- **Menções de marca nas páginas**: sua participação de voz versus marcas associadas e concorrentes de mercado.
- **Rastreamento de mercado**: um gráfico filtrável onde você pode selecionar até cinco marcas de concorrentes para comparar a participação de voz nas páginas analisadas.

### Análise de sentimentos

Rastreia a percepção da marca nas páginas analisadas com um gráfico **Distribuição de sentimentos** mostrando o detalhamento da porcentagem de sentimentos favoráveis, neutros e desfavoráveis nas páginas.

![Análise de sentimentos](/help/dashboards/opportunities/assets/cited-sentiment-distribution.png)

### Páginas

Uma tabela detalhada das páginas da Web citadas analisadas com as seguintes colunas:

- **Página** — URL da página analisada.
- **Menções de marca** — Contagem de menções de marca versus o total de menções na página.
- **Participação de voz** — A participação da sua marca em menções em relação a todas as marcas mencionadas.
- **Cinco marcas principais** — As marcas mais mencionadas na página.
- **Sentimento** — Sentimento geral em relação à sua marca na página.
- **Citações de IA** — Número de respostas de IA que citaram esta página.

### Assuntos

Uma tabela de tópicos recorrentes identificados nas páginas analisadas, mostrando:

- **Tópico** — O tema ou assunto recorrente identificado.
- **Menções de marca** — Número de menções de marca associadas ao tópico.
- **Sentimento** — Sentimento geral associado ao tópico.

Clicar em **Detalhes** em qualquer tópico abre um detalhamento com um resumo de análise e as páginas de origem da contribuição.

## Experimente na demonstração

Veja a oportunidade de Análise de sentimentos citados em ação usando o ambiente de demonstração do Frescopa -[Visualizar Análise de sentimentos citados na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/cited-analysis/d3a8b217-9f4c-4e88-a612-6b7f91e5c044?siteId=frescopa-demo).

## Perguntas frequentes

**Por que os URLs mais citados são importantes para a pesquisa com IA?**

Os URLs mais citados são as páginas de terceiros às quais os sistemas de IA mais frequentemente fazem referência ao gerar respostas sobre a sua marca. O sentimento e o enquadramento dessas páginas exercem uma influência direta e desproporcional sobre como a IA representa sua marca, mais do que páginas raramente citadas. Melhorar a forma como sua marca é representada nessas páginas específicas é uma das ações de maior impacto que você pode tomar para obter visibilidade em IA.

**Por que essa oportunidade não está aparecendo no meu painel?**

Essa oportunidade só aparece quando URLs citados são detectados em prompts do conjunto de prompts do painel Presença da marca. Se não forem identificados URLs citados para esses prompts, a oportunidade não será exibida.

**O que significa Páginas ignoradas?**

As páginas ignoradas são URLs citados que não puderam ser analisados, geralmente porque a página está protegida por acesso pago, exige autenticação ou bloqueia o acesso automatizado. Essas páginas são contabilizadas, mas excluídas da análise de sentimento e menção de marca.

**O que é Participação de voz?**

A Participação de voz é a porcentagem da marca em relação ao total de menções da marca em uma determinada página ou em todas as páginas analisadas, comparada a todas as outras marcas mencionadas.

**O que são citações de IA?**

Citações de IA mostram quantas respostas de IA citaram uma determinada página. Um número maior de citações de IA indica que a página está sendo usada ativamente por sistemas de IA ao gerar respostas sobre tópicos relacionados, tornando o sentimento expresso nessas páginas especialmente importante para a representação da marca pela IA.

**Como os concorrentes de mercado são identificados?**

Os concorrentes são identificados automaticamente com base no setor da sua marca e nas marcas mencionadas com mais frequência em conjunto nas páginas analisadas. Você também pode selecionar manualmente até cinco marcas para comparar no gráfico de Rastreamento do mercado.

**Com que frequência a análise é atualizada?**

A análise reflete os URLs citados detectados até a data exibida no cabeçalho do painel. Reavalie a oportunidade após implementar as recomendações para rastrear as mudanças no sentimento e na participação de voz.
