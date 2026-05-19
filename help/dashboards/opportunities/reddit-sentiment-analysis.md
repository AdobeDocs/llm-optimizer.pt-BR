---
title: Análise de sentimentos do Reddit
description: Saiba como o LLM Optimizer analisa as threads do Reddit para exibir recomendações que melhoram a percepção e a visibilidade da sua marca nos resultados de pesquisa com IA.
feature: Opportunities
autotag-review: '2026-05-15T17:56:59.489Z'
TQID: 'https://experienceleague.adobe.com/LRC3nhHrAZoODy4gfsZiR7gc0i8n-IYqvZFj1TAUxsQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1163
ht-degree: 100%

---


# Análise de sentimentos do Reddit

O Reddit é uma fonte de dados essencial para grandes modelos de linguagem. Quando os usuários perguntam aos assistentes de IA sobre sua marca, as respostas são influenciadas pelo sentimento do conteúdo do Reddit. A forma como sua marca é discutida em diferentes subreddits influencia diretamente a maneira como os sistemas de IA a entendem e a representam nas respostas geradas.

A oportunidade Análise de sentimentos do Reddit aparece quando as threads do Reddit são detectadas como citações de prompts no seu conjunto de prompts do painel de Presença da marca. Ela analisa as threads citadas e seus comentários em busca de sentimentos, participações de voz e tópicos recorrentes. A oportunidade revela recomendações priorizadas para melhorar como sua marca é percebida e citada pelos sistemas de IA.

Ela analisa sua marca em quatro dimensões:

- **Posts analisados**: número de posts do Reddit examinados quanto a menções à marca e sentimento.
- **Comentários analisados**: número de comentários examinados nas postagens analisadas.
- **Menções à marca (threads)**: com que frequência sua marca é mencionada nas threads analisadas.
- **Sentimento geral (threads)**: sentimento agregado em relação à sua marca em threads analisadas.

>[!NOTE]
>A Análise de sentimentos do Reddit está atualmente na versão beta. As funcionalidades e a disponibilidade podem mudar à medida que o recurso for desenvolvido.

![Painel de Análise de sentimentos do Reddit](/help/dashboards/opportunities/assets/reddit-sentiment-overview.png)

## Como funciona

O LLM Optimizer monitora as threads do Reddit citadas por sistemas de IA para prompts no conjunto de prompts do painel de Presença da marca. Quando threads citadas são detectadas, o sistema analisa essas threads e seus comentários em busca de menções à marca, sentimento, participação de voz e citações de IA. Ele compara o desempenho da sua marca com os concorrentes do mercado, identifica tópicos recorrentes que determinam o sentimento e gera recomendações para resolver a falta de percepção.

Se nenhuma thread do Reddit for citada em seu conjunto de prompts, esta oportunidade não aparece no painel.

Os resultados são exibidos em duas guias: **Sugestões** e **Desempenho**.

## Sugestões

Esta guia mostra recomendações para melhorar a percepção da marca no Reddit. As sugestões são organizadas em três subguias: **Sugestões atuais**, **Sugestões fixas** e **Sugestões ignoradas**.

![Guia Sugestões](/help/dashboards/opportunities/assets/reddit-sentiment-suggestions.png)

A tabela de sugestões inclui as seguintes colunas:

- **Sugestão** — A melhoria recomendada para resolver uma lacuna de percepção.
- **Prioridade**: nível de urgência (Crítico, Alto, Médio, Baixo).
- **Itens de ação**: abre um painel com etapas específicas para implementar a recomendação, incluindo as equipes responsáveis (por exemplo, RP, Gerenciamento da Comunidade, Marketing de produtos).
- **Evidência**: abre uma tabela Origens mostrando as threads do Reddit por trás da sugestão.

Expandir uma sugestão revela uma seção **Análise de IA** com:

- **Por que isso precisa ser melhorado**: uma explicação da falta de percepção identificada, incluindo o contexto competitivo e como o problema está se formando nas threads do Reddit.
- **Como melhorar**: orientação específica sobre qual conteúdo ou ações resolveriam o problema.
- **Resultado esperado**: o resultado antecipado da implementação da recomendação.

A tabela **Origens** mostra as threads do Reddit que orientam a sugestão, com as seguintes colunas:

- **Thread** — Título e link para o thread do Reddit.
- **Subreddit**: o subreddit no qual a thread foi postada.
- **Engajamento** — Nível de engajamento (baixo, médio, alto).
- **Menções da marca** — Contagem de menções da sua marca em relação ao total de menções no thread.
- **Participação de voz** — A participação da sua marca nas menções em relação a todas as marcas mencionadas.
- **5 principais marcas** — As marcas mais mencionadas no thread.
- **Sentimento** — Sentimento geral em relação à sua marca no thread.
- **Citações de IA**: número de respostas de IA que citaram esta thread.

## Desempenho

A guia **Desempenho** fornece uma análise detalhada de como sua marca está se saindo no conteúdo do Reddit. Está organizada em quatro seções.

### Cenário do mercado

Compara o desempenho da sua marca com o desempenho de marcas associadas e concorrentes do mercado, com base em menções em threads.

![Cenário do mercado](/help/dashboards/opportunities/assets/reddit-sentiment-landscape.png)

Ele mostra:

- **Menções de marca em threads** — Sua participação de voz versus marcas associadas e concorrentes do mercado.
- **Rastreamento de mercado** — Um gráfico filtrável onde você pode selecionar até cinco marcas de concorrentes para comparar participações de voz entre threads.

### Análise de sentimentos

Rastreia a percepção da marca em threads analisados com um gráfico **Distribuição de sentimentos** mostrando o detalhamento da porcentagem de sentimentos favoráveis, neutros e desfavoráveis entre threads.

![Análise de sentimentos](/help/dashboards/opportunities/assets/reddit-sentiment-distribution.png)

### Threads

Uma tabela detalhada de threads do Reddit analisados com as seguintes colunas:

- **Thread** — Título e link para o thread do Reddit.
- **Subreddit**: o subreddit no qual a thread foi postada.
- **Engajamento** — Nível de engajamento (baixo, médio, alto).
- **Menções da marca** — Contagem de menções da sua marca em relação ao total de menções no thread.
- **Participação de voz** — A participação da sua marca nas menções em relação a todas as marcas mencionadas.
- **5 principais marcas** — As marcas mais mencionadas no thread.
- **Sentimento** — Sentimento geral em relação à sua marca no thread.
- **Citações de IA**: número de respostas de IA que citaram esta thread.

### Assuntos

Uma tabela com os tópicos recorrentes identificados nos threads analisados, mostrando:

- **Tópico** — O tema ou assunto recorrente identificado.
- **Menções de marca** — Número de menções de marca associadas ao tópico.
- **Sentimento** — Sentimento geral associado ao tópico.

Clicar em **Detalhes** em qualquer tópico abre um painel de detalhamento com duas guias:

- **Análise** — Um resumo de como sua marca é mencionada nos threads relacionados a esse tópico.
- **Fontes** — Os threads específicos do Reddit que contribuem para o sinal de sentimento do tópico.

## Experimente na demonstração

Veja a oportunidade de Análise de sentimentos do Reddit em ação usando o ambiente de demonstração do Frescopa.

[Visualizar a Análise de sentimentos do Reddit na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/reddit-analysis/b7e4d9a0-3c1f-4e2b-9d5a-8f2c1e0a7b4d?siteId=frescopa-demo)

## Perguntas frequentes

**Por que o Reddit é importante para a pesquisa com IA?**

O Reddit é uma das fontes com maior peso nos dados de treinamento e na recuperação em tempo real de LLMs. Quando os sistemas de IA geram respostas sobre marcas, produtos e tópicos, as discussões do Reddit frequentemente influenciam o tom, o enquadramento e as afirmações factuais dessas respostas. Uma marca que é discutida de forma desfavorável ou imprecisa no Reddit tem maior probabilidade de ser representada dessa forma em respostas geradas por IA.

**Por que essa oportunidade não está aparecendo no meu painel?**

Essa oportunidade só aparece quando os threads do Reddit são detectados como citações em prompts no conjunto de prompts do painel Presença da marca. Se nenhum thread do Reddit for citado para esses prompts, a oportunidade não será exibida. À medida que sua marca ganha mais visibilidade no Reddit e esses threads são citados por sistemas de IA para seu conjunto de prompts, a oportunidade se tornará disponível.

**O que significa Sentimento geral?**

O sentimento geral reflete o tom agregado dos threads em que sua marca é mencionada: favorável, neutro ou desfavorável, calculado com base em todos os threads analisados.

**O que é Participação de voz?**

Participação de voz é a porcentagem da sua marca no total de menções de marca em um determinado thread ou em todos os threads analisados, em relação a todas as outras marcas mencionadas.

**O que são Citações de IA?**

As citações de IA mostram quantas respostas de IA citaram um determinado thread. As contagens mais altas de citação de IA indicam que o thread está sendo usado ativamente pelos sistemas de IA ao gerar respostas sobre tópicos relacionados, tornando o sentimento nesses threads especialmente importante para a representação de IA da sua marca.

**Como os concorrentes do mercado são identificados?**

Os concorrentes são identificados automaticamente com base no setor da sua marca e nas marcas mencionadas com mais frequência em conjunto nos threads analisados. Você também pode selecionar manualmente até cinco marcas para comparar no gráfico de Rastreamento do mercado.

**Com que frequência a análise é atualizada?**

A análise do Reddit reflete o conteúdo analisado até a data mostrada no cabeçalho do painel. Reavalie a oportunidade após implementar as recomendações para rastrear as mudanças no sentimento e na participação de voz.
