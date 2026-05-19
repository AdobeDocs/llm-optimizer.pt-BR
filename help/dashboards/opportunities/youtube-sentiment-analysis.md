---
title: Análise de sentimentos do YouTube
description: Saiba como o LLM Optimizer analisa vídeos e comentários do YouTube para exibir recomendações que melhoram a percepção e a visibilidade de sua marca nos resultados de pesquisa com IA.
feature: Opportunities
autotag-review: '2026-05-15T18:12:18.358Z'
TQID: 'https://experienceleague.adobe.com/XevtwbOrmn6QTjMxnErSTI91WUv9m6GYWJ7LeLXdXXg'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1255
ht-degree: 100%

---


# Análise de sentimentos do YouTube

O YouTube é uma das plataformas mais influentes que moldam a percepção do consumidor e a reputação da marca. Quando os sistemas de IA respondem às solicitações sobre sua marca, eles citam cada vez mais os vídeos do YouTube como fontes, tornando a forma como sua marca é discutida nesse conteúdo uma entrada direta nas respostas geradas por IA.

A oportunidade “Análise de sentimentos do YouTube” é exibida quando vídeos do YouTube são detectados como citações de prompts no conjunto de prompts do painel Presença da marca. Ela analisa os vídeos citados e seus comentários em busca de sentimentos, participações de voz e tópicos recorrentes. Em seguida, ela apresenta recomendações priorizadas para melhorar como sua marca é percebida e representada em respostas geradas por IA.

Ela analisa sua marca em seis dimensões:

- **Vídeos analisados** — Número de vídeos do YouTube examinados quanto a menção de marca e sentimento.
- **Comentários analisados** — Número de comentários examinados nos vídeos analisados.
- **Menções da marca (vídeos)** — Com que frequência a marca é mencionada em conteúdo de vídeo.
- **Menções da marca (comentários)** — Com que frequência a marca é mencionada nos comentários.
- **Sentimento geral (vídeos)** — Sentimento agregado em relação à marca em conteúdo em vídeo.
- **Sentimento geral (comentários)** — Sentimento agregado em relação à marca nos comentários.

>[!NOTE]
>A Análise de sentimentos do YouTube está atualmente na versão beta. As funcionalidades e a disponibilidade podem mudar à medida que o recurso for desenvolvido.

![Painel de análise de sentimentos do YouTube](/help/dashboards/opportunities/assets/youtube-sentiment-overview.png)

## Como funciona

O LLM Optimizer monitora os vídeos do YouTube citados pelos sistemas de IA em prompts no conjunto de prompts do painel Presença da marca. Quando os vídeos citados são detectados, ele analisa esses vídeos e seus comentários quanto a menções de marca, sentimentos, participações de voz e citações de IA. Ele compara o desempenho de sua marca com os concorrentes do mercado e marcas associadas, identifica tópicos recorrentes que impulsionam o sentimento e gera recomendações para resolver lacunas de percepção.

Se nenhum vídeo do YouTube for citado nos prompts do seu conjunto de prompts, esta oportunidade não aparecerá em seu painel.

Os resultados são exibidos em duas guias: **Sugestões** e **Desempenho**.

## Sugestões

Esta guia mostra recomendações para melhorar a percepção da sua marca no YouTube. As sugestões são organizadas em três subguias: **Sugestões atuais**, **Sugestões fixas** e **Sugestões ignoradas**.

![Guia Sugestões](/help/dashboards/opportunities/assets/youtube-sentiment-suggestions.png)

A tabela de sugestões inclui as seguintes colunas:

- **Sugestão** — A melhoria recomendada para resolver uma lacuna de percepção.
- **Prioridade**: nível de urgência (Crítico, Alto, Médio, Baixo).
- **Itens de ação** — Abre um painel com etapas específicas para implementar a recomendação, incluindo as equipes responsáveis (por exemplo, Estratégia de conteúdo, Marketing de influência, Marketing de produto).
- **Evidência** — Abre uma tabela de Fontes mostrando os vídeos por trás da sugestão.

Expandir uma sugestão revela uma seção **Análise de IA** com:

- **Por que isso precisa ser melhorado** — Uma explicação da lacuna de percepção identificada, incluindo o contexto competitivo e como o problema está se formando no conteúdo do YouTube.
- **Como melhorar**: orientação específica sobre qual conteúdo ou ações resolveriam o problema.
- **Resultado esperado**: o resultado antecipado da implementação da recomendação.

A tabela **Fontes** mostra os vídeos do YouTube que orientam a sugestão, com as seguintes colunas:

- **Vídeo** — Título e link para o vídeo do YouTube.
- **Canal** — O canal do YouTube que publicou o vídeo.
- **Engajamento** — Nível de engajamento (baixo, médio, alto).
- **Menções de marca** — Contagem de suas menções de marca versus o total de menções no vídeo.
- **Participação de voz** — A participação da sua marca em menções relativas relacionadas a todas as marcas mencionadas.
- **Cinco marcas principais** — As marcas mais mencionadas no vídeo.
- **Sentimento** — Sentimento geral em relação à sua marca no vídeo.
- **Citações de IA** — Número de respostas de IA que citaram este vídeo.

## Desempenho

A guia **Desempenho** fornece uma análise detalhada de como a sua marca está se saindo no conteúdo do YouTube. Está organizada em quatro seções.

### Cenário do mercado

Compara o desempenho da sua marca com o de marcas associadas e concorrentes do mercado com base nas menções.

![Cenário do mercado](/help/dashboards/opportunities/assets/youtube-sentiment-market-landscape.png)

Ele mostra:

- **Menções de marca em vídeos** — Sua participação de voz versus marcas associadas e concorrentes do mercado.
- **Menções de marca em comentários** — A mesma comparação no conteúdo de comentários.
- **Rastreamento de mercado** — Um gráfico filtrável onde você pode selecionar até cinco marcas de concorrentes para comparar a participação de voz entre vídeos e comentários.

### Análise de sentimentos

Rastreia a percepção da marca no conteúdo analisado com um gráfico de **Distribuição de sentimentos** mostrando o detalhamento da porcentagem de sentimentos favoráveis, neutros e desfavoráveis para vídeos e comentários.

![Análise de sentimentos](/help/dashboards/opportunities/assets/youtube-sentiment-distribution.png)

### Vídeos

Uma tabela detalhada dos vídeos analisados do YouTube com as seguintes colunas:

- **Vídeo** — Título e link para o vídeo do YouTube.
- **Canal** — O canal do YouTube que publicou o vídeo.
- **Engajamento** — Nível de engajamento (baixo, médio, alto).
- **Menções de marca** — Contagem de suas menções de marca versus o total de menções no vídeo.
- **Participação de voz** — A participação da sua marca em menções relativas relacionadas a todas as marcas mencionadas.
- **Cinco marcas principais** — As marcas mais mencionadas no vídeo.
- **Sentimento** — Sentimento geral em relação à sua marca no vídeo.
- **Citações de IA** — Número de sinais de citação de IA associados ao vídeo.

A guia Desempenho mostra os painéis **Vídeos** e **Tópicos** em uma exibição (com **Vídeos** selecionados). A figura a seguir inclui a tabela no nível do vídeo e, abaixo dela, o resumo de **Tópicos**.

![Tabelas de Vídeos e Tópicos na guia Desempenho](/help/dashboards/opportunities/assets/youtube-sentiment-videos.png)

### Comentários

Uma tabela detalhada de comentários analisados do YouTube com as mesmas colunas da tabela Vídeos, filtrada para dados no nível de comentário.

### Assuntos

Uma tabela de tópicos recorrentes identificados no conteúdo analisado, mostrando:

- **Tópico** — O tema ou assunto recorrente identificado.
- **Menções de marca** — Número de menções de marca associadas ao tópico.
- **Sentimento** — Sentimento geral associado ao tópico.

A tabela **Tópicos** aparece na mesma exibição de Desempenho da tabela Vídeos. Consulte a figura na seção [Vídeos](#videos) acima.

## Experimente na demonstração

Veja a oportunidade de Análise de Sentimento do YouTube em ação usando o ambiente de demonstração do Frescopa.

[Visualizar Análise de sentimentos do YouTube na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/youtube-analysis/971280f5-6a07-4506-85bf-d7419dca9803?siteId=frescopa-demo)

## Perguntas frequentes

**Por que o YouTube é importante para as pesquisas com IA?**

Os sistemas de IA citam cada vez mais os vídeos do YouTube ao gerar respostas sobre marcas, produtos e tópicos. Quando esses vídeos citados discutem sua marca de forma desfavorável ou imprecisa, esse sentimento é alimentado diretamente em como os sistemas de IA representam sua marca. Melhorar a maneira como sua marca é discutida no conteúdo do YouTube que os sistemas de IA já estão citando é uma das maneiras mais diretas de influenciar a percepção da marca gerada por IA.

**Por que esta oportunidade não está sendo mostrada no meu painel?**

Essa oportunidade só aparece quando vídeos do YouTube são detectados como citações de prompts no conjunto de prompts do painel Presença da marca. Se nenhum vídeo do YouTube estiver sendo citado para esses prompts, a oportunidade não será exibida. À medida que sua marca ganha mais cobertura do YouTube e esses vídeos são citados pelos sistemas de IA para o seu conjunto de prompts, a oportunidade se tornará disponível.

**O que significa Sentimento geral?**

O sentimento geral reflete o tom agregado de conteúdo onde sua marca é mencionada: favorável, neutro ou desfavorável. Ele é calculado separadamente para vídeos e comentários, pois eles podem diferir significativamente.

**O que é Participação de voz?**

Participação de voz é a porcentagem da sua marca no total de menções de marca em um determinado conteúdo ou em todo o conteúdo analisado, em relação a todas as outras marcas mencionadas.

**O que são Citações de IA?**

As citações de IA mostram quantas respostas de IA citaram um determinado vídeo. As contagens mais altas de citações de IA indicam que o vídeo está sendo usado ativamente pelos sistemas de IA ao gerar respostas sobre tópicos relacionados, tornando o sentimento nesses vídeos especialmente importante para a representação da IA de sua marca.

**Como os concorrentes do mercado são identificados?**

Os concorrentes são identificados automaticamente com base no setor da sua marca e nas marcas mencionadas com mais frequência em conjunto no conteúdo analisado. Você também pode selecionar manualmente até cinco marcas para comparar no gráfico de Rastreamento do mercado.

**Com que frequência a análise é atualizada?**

A análise do YouTube reflete o conteúdo analisado até a data mostrada no cabeçalho do painel. Reavalie a oportunidade após implementar as recomendações para rastrear as mudanças no sentimento e na participação de voz.
