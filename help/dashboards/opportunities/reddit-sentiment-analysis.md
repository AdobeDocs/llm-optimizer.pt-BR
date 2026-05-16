---
title: Editar análise de Sentimento
description: Saiba como o LLM Optimizer analisa os threads do Reddit para exibir recomendações que melhoram a percepção e a visibilidade de sua marca nos resultados de Pesquisas com IA.
feature: Opportunities
autotag-review: '2026-05-15T17:56:59.489Z'
TQID: 'https://experienceleague.adobe.com/LRC3nhHrAZoODy4gfsZiR7gc0i8n-IYqvZFj1TAUxsQ'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1163
ht-degree: 0%

---


# Editar análise de Sentimento

O Reddit é uma fonte de dados crítica para grandes modelos linguísticos. Quando os usuários perguntam aos assistentes de IA sobre sua marca, as respostas são influenciadas pelo sentimento de conteúdo Reddit. A maneira como sua marca é discutida nos subreddits determina diretamente como os sistemas de IA a entendem e representam em respostas geradas.

A oportunidade Análise de Sentimento Reddit aparece quando as threads Reddit são detectadas como citações de prompts no seu conjunto de prompts do painel de Presença da marca. Ele analisa as threads citadas e seus comentários em busca de sentimentos, participações de voz e tópicos recorrentes. A oportunidade revela recomendações priorizadas para melhorar como sua marca é percebida e citada pelos sistemas de IA.

Ele analisa sua marca em quatro dimensões:

- **Publicações analisadas** — Número de publicações do Reddit examinadas para menções de marca e sentimentos.
- **Comentários analisados** — Número de comentários examinados nas postagens analisadas.
- **Menções de marca (threads)** — Com que frequência sua marca é mencionada nas threads analisadas.
- **sentimento geral (threads)** — sentimento agregado em direção à sua marca em threads analisados.

>[!NOTE]
>A Análise de Sentimento Reddit está atualmente na versão beta. Os recursos e a disponibilidade podem mudar à medida que a capacidade continua a se desenvolver.

![Editar painel de Análise de Sentimento](/help/dashboards/opportunities/assets/reddit-sentiment-overview.png)

## Como funciona

O LLM Optimizer monitora as threads do Reddit citadas pelos sistemas de IA para prompts no conjunto de prompts do painel do Presença da marca. Quando os segmentos citados são detectados, ele analisa esses segmentos e seus comentários para menções de marca, sentimentos, participações de voz e citações da IA. Ele compara o desempenho de sua marca com os concorrentes do mercado, identifica tópicos recorrentes que impulsionam o sentimento e gera recomendações para resolver lacunas de percepção.

Se nenhuma thread Reddit for citada para as solicitações em seu prompt definido, esta oportunidade não aparecerá em seu painel.

Os resultados são exibidos em duas guias: **Sugestões** e **Desempenho**.

## Sugestões

Esta guia mostra recomendações para melhorar a percepção da sua marca no Reddit. As sugestões são organizadas em três subguias: **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**.

![Guia Sugestões](/help/dashboards/opportunities/assets/reddit-sentiment-suggestions.png)

A tabela de sugestões inclui as seguintes colunas:

- **Sugestão** — a melhoria recomendada para resolver uma lacuna de percepção.
- **Prioridade** — Nível de urgência (Crítico, Alto, Medium, Baixo).
- **Itens de Ação** — Abre um painel com etapas específicas para implementar a recomendação, incluindo as equipes responsáveis (por exemplo, RP, Gerenciamento da Comunidade, Marketing de Produtos).
- **Evidence** — Abre uma tabela Origens mostrando as threads do Reddit por trás da sugestão.

Expandir uma sugestão revela uma seção **Análise de IA** com:

- **Por que isso precisa ser melhorado** — Uma explicação da lacuna de percepção identificada, incluindo o contexto competitivo e como o problema está se formando nas threads do Reddit.
- **Como melhorar** — Orientação específica sobre qual conteúdo ou ações resolveriam a lacuna.
- **Resultado Esperado** — O resultado antecipado da implementação da recomendação.

A tabela **Fontes** mostra as threads do Reddit que orientam a sugestão, com as seguintes colunas:

- **Thread** — Título e link para o thread Reddit.
- **Subreddit** — O subreddit no qual o thread foi postado.
- **Envolvimento** — Nível de envolvimento (Baixo, Medium, Alto).
- **Menções de marca** — Contagem de suas menções de marca versus o total de menções no thread.
- **Participação de voz** — a participação da sua marca em menções relativas a todas as marcas mencionadas.
- **Cinco marcas principais** — As marcas mais mencionadas na thread.
- **Sentimento** — sentimento geral em direção à sua marca no thread.
- **Citações de IA** — Número de respostas de IA que citaram este thread.

## Desempenho

A guia **Performance** fornece uma análise detalhada de como sua marca está se saindo no conteúdo Reddit. Está organizado em quatro seções.

### Cenário do mercado

Compara o desempenho da sua marca com o desempenho de marcas associadas e concorrentes do mercado, com base em menções presentes em segmentos.

![Cenário do mercado](/help/dashboards/opportunities/assets/reddit-sentiment-landscape.png)

Ele mostra:

- **Menções de marca em threads** — Sua participação de voz versus marcas associadas e concorrentes do mercado.
- **Rastreamento de Mercado** — Um gráfico filtrável onde você pode selecionar até cinco marcas de concorrentes para comparar participações de voz entre threads.

### Análise de sentimentos

Rastreia a percepção da marca em threads analisados com um gráfico **Distribuição de Sentimentos** mostrando a divisão da porcentagem de sentimentos favoráveis, neutros e desfavoráveis entre threads.

![Análise de Sentimento](/help/dashboards/opportunities/assets/reddit-sentiment-distribution.png)

### Threads

Uma tabela detalhada de threads Reddit analisados com as seguintes colunas:

- **Thread** — Título e link para o thread Reddit.
- **Subreddit** — O subreddit no qual o thread foi postado.
- **Envolvimento** — Nível de envolvimento (Baixo, Medium, Alto).
- **Menções de marca** — Contagem de suas menções de marca versus o total de menções no thread.
- **Participação de voz** — a participação da sua marca em menções relativas a todas as marcas mencionadas.
- **Cinco marcas principais** — As marcas mais mencionadas na thread.
- **Sentimento** — sentimento geral em direção à sua marca no thread.
- **Citações de IA** — Número de respostas de IA que citaram este thread.

### Assuntos

Uma tabela de tópicos recorrentes identificados entre threads analisados, mostrando:

- **Tópico** — O tema ou assunto recorrente identificado.
- **Menções de marca** — Número de menções de marca associadas ao tópico.
- **Sentimento** — sentimento geral associado ao tópico.

Clicar em **Detalhes** em qualquer tópico abre um painel de detalhamento com duas guias:

- **Análise** — Um resumo de como sua marca é discutida entre threads associados a esse tópico.
- **Fontes** — Os threads específicos do Reddit que contribuem para o sinal de sentimento do tópico.

## Experimente na demonstração

Veja a oportunidade da Análise de Sentimento Reddit em ação usando o ambiente de demonstração Frescopa.

[Ver Reddit Sentimento Analysis na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/reddit-analysis/b7e4d9a0-3c1f-4e2b-9d5a-8f2c1e0a7b4d?siteId=frescopa-demo)

## Perguntas frequentes

**Por que o Reddit é importante para as Pesquisas com IA?**

O Reddit é uma das fontes mais ponderadas em dados de treinamento de LLM e recuperação em tempo real. Quando os sistemas de IA geram respostas sobre marcas, produtos e tópicos, as discussões do Reddit frequentemente informam o tom, o enquadramento e as reivindicações fatuais nessas respostas. Uma marca que é discutida desfavoravelmente ou de forma imprecisa no Reddit é mais provável de ser representada dessa forma em respostas geradas por IA.

**Por que esta oportunidade não está sendo mostrada no meu painel?**

Esta oportunidade só aparece quando os threads do Reddit são detectados como citações para prompts no seu conjunto de prompts do painel do Presença da marca. Se nenhuma thread Reddit estiver sendo citada para essas seleções, a oportunidade não será mostrada. À medida que sua marca ganha mais cobertura do Reddit e esses threads são citados pelos sistemas de IA para o seu conjunto de prompt, a oportunidade ficará disponível.

**O que significa o Sentimento Geral?**

O sentimento geral reflete o tom agregado de threads onde sua marca é mencionada: favorável, neutro ou desfavorável calculado em todos os threads analisados.

**O que é o Participação de voz?**

Participação de voz é a porcentagem da sua marca no total de menções de marca em um determinado segmento ou em todos os segmentos analisados, em relação a todas as outras marcas mencionadas.

**O que são Citações de IA?**

As citações de IA mostram quantas respostas de IA citaram um determinado segmento. As contagens mais altas de citação de IA indicam que a thread está sendo usada ativamente pelos sistemas de IA ao gerar respostas sobre tópicos relacionados, tornando o sentimento nessas threads especialmente importante para a representação de IA da sua marca.

**Como os concorrentes do mercado são identificados?**

Os concorrentes são identificados automaticamente com base no setor da sua marca e nas marcas comencionadas com mais frequência nos threads analisados. Você também pode selecionar manualmente até cinco marcas para comparação no gráfico Rastreamento de mercado.

**Com que frequência a análise é atualizada?**

A análise Reddit reflete o conteúdo analisado até a data mostrada no cabeçalho do painel. Revise a oportunidade depois de implementar as recomendações para rastrear as alterações no sentimento e no participação de voz.
