---
title: Presença da marca
description: Saiba como usar o painel Presença da marca para entender como sua marca é percebida no nível de respostas geradas por IA.
feature: Brand Presence
source-git-commit: 24183fbe2577bb9402f8b6aaaf1e46c75403383d
workflow-type: ht
source-wordcount: '1299'
ht-degree: 100%

---


# Presença da marca {#brand-presence}

O painel Presença da marca fornece uma visão geral detalhada sobre como sua marca é percebida no nível de respostas geradas por IA. Ele mostra onde, com que frequência e em que contexto sua marca é mencionada. Você pode usar o painel para medir a visibilidade, monitorar as citações e explorar tendências de sentimento. O painel é dividido em várias seções, cada uma com insights diferentes. Também há filtros personalizáveis para ajudar você a refinar os dados exibidos.

![Presença da marca](/help/dashboards/assets/brand-main.png)

Esta página detalha o seguinte:

* [Filtros](#filters)
* [Métricas de visão geral](##key-metrics)
* [Comparação com outras marcas](##others-comparison)
* [Tendência de sentimentos](#sentiment-trend)
* [Insights de dados](#data-insights)

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetam **todas** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas**: selecione o intervalo de tempo dos dados exibidos. Por exemplo, as últimas 4 semanas. Também é possível personalizar o período selecionando a opção **Semanas personalizadas**.
* **Categoria**: filtre os resultados exibidos por categorias predefinidas ou personalizadas.
* **Tópico**: filtre por tópico para analisar temas de conteúdo e áreas específicas nas quais sua marca aparece nas respostas da IA.
* **Plataforma**: escolha qual mecanismo de IA analisar. Atualmente, o LLM Optimizer é compatível com ChatGPT, Google AI Overviews, Google AI Mode, Microsoft Copilot, Google Gemini e Perplexity.
* **Origem dos prompts**: escolha a origem dos prompts. A origem pode ser inserida pelo usuário ou gerada pela IA.
* **Prompt Branding**: filtre os resultados por prompts com marca ou sem marca.
* **Região**: filtre os resultados por região. Nem todas as regiões estarão disponíveis no lançamento.

Após selecionar o filtro desejado, clique em **Aplicar filtros** para aplicar a seleção ao painel.

## Métricas de visão geral {#overview-metrics}

O painel destaca três métricas muito importantes na parte superior da página: pontuação de visibilidade, menções e citações. Quanto menor for a contagem dessas métricas, pior será a percepção da sua marca, o que significa que você deve agir para melhorar a presença da marca. Apresentamos abaixo uma breve descrição de cada métrica e o que ela representa.

![Métricas de visão geral](/help/dashboards/assets/overview-metrics.png)

### Pontuação de visibilidade {#visibility-score}

A pontuação de visibilidade é composta por fatores como: menções, citações, sentimento e classificação. Cada fator tem um “peso” atribuído a ele, o qual contribui para a pontuação final.

### Menções de marca {#mentions}

Essa métrica representa o número total de vezes que sua marca ou categorias foram mencionadas nos prompts de IA de amostra. Por exemplo, se você tiver a marca “Café B”, com as categorias “Máquinas” e “Acessórios”, essa métrica conta o número total de vezes que elas aparecem nas respostas de amostra da IA.

### Citações {#citations}

Essa métrica representa o número de vezes que seu site foi referenciado como uma origem.

Os indicadores de tendência de cada métrica principal mostram como esses valores mudam com o tempo em comparação ao período anterior.

## Comparação com outras marcas {#others-comparison}

Na seção Comparação com outras marcas, é possível selecionar até cinco outras marcas e comparar suas menções e citações com a sua marca. Dessa forma, você pode visualizar e comparar seu desempenho em relação a outras marcas.

![Comparação com outras marcas](/help/dashboards/assets/other-comparison.png)

As outras marcas são selecionadas na lista suspensa e os gráficos são atualizados ao clicar em **Aplicar filtros**. Os gráficos exibem menções de marca semanais e citações de marca semanais lado a lado. Você também pode passar o mouse ao longo do gráfico para ver a evolução dos dados ao longo do intervalo de tempo semanal.

## Análise de tendências de sentimento {#sentiment-trend}

Na seção de análise de tendências de sentimento, você pode acompanhar a percepção da sua marca nas respostas de amostra da IA. A métrica de tendência de sentimento pode ser positiva, neutra ou negativa. Por exemplo, ela pode ser positiva se as respostas destacarem a qualidade do produto ou negativa se falarem sobre um atendimento ruim. O gráfico de tendências mostra as mudanças na percepção da marca a cada semana. Esta seção é preenchida somente depois que sua marca é mencionada.

![Tendência de sentimento](/help/dashboards/assets/sentiment-trend.png)

## Insights de dados e participação de voz {#data-insights}

Para finalizar o painel, temos duas tabelas importantes: insights de dados e participação de voz. As informações apresentadas nessas tabelas ajudam você a identificar os pontos fortes de sua marca e onde são necessárias otimizações.

Ao usar a tabela de **insights de dados**, você pode explorar tópicos e perguntas do usuário para avaliar e otimizar o impacto do conteúdo. Os resultados são detalhados por tópicos e prompts. Enquanto isso, a tabela de **participação de voz** compara a voz da sua marca a outras marcas em vários tópicos e ajuda a identificar lacunas e priorizar tópicos futuros.

![Insights de dados](/help/dashboards/assets/data-insights.png)

Ambas as tabelas têm um campo de pesquisa para acesso rápido a tópicos e você pode personalizar quais métricas serão exibidas clicando no botão **Configurar colunas**. Além disso, você pode usar a opção **Exportar** para baixar a tabela em .csv e compartilhar os insights com sua equipe ou incluir as tabelas em relatórios executivos.

Clique nas guias abaixo para obter detalhes sobre cada tabela e as métricas associadas.

>[!BEGINTABS]

>[!TAB Insights de dados]

A tabela de insights de dados ajuda você a explorar tópicos e sugestões do usuário para avaliar e otimizar o impacto do conteúdo. Ela exibe as seguintes métricas:

* **Tópico**: a categoria de tópico representa as palavras-chave de SEO e as perguntas do usuário relacionadas à sua marca. Você pode clicar para expandir cada tópico e ver prompts individuais analisados em relação à presença da marca. Cada tópico exibe um botão **Detalhes** ao passar o mouse sobre ele. Clicar no botão abre uma janela separada e apresenta mais detalhes.
* **Região**: exibe a região dos prompts.
* **Popularidade**: a categoria de popularidade representa o volume de pesquisa deste tópico em relação a todos os outros tópicos da análise. O valor pode ser Alta, Média ou Baixa.
* **Pontuação de visibilidade**: a pontuação de visibilidade desse tópico. Isso reflete fatores ponderados como menções, citações, sentimento e classificação.
* **Menções**: o número de vezes que sua marca foi mencionada nas respostas da IA para este tópico ou esta combinação de tópico/prompt.
* **Sentimento**: a percepção da marca nas respostas da IA, pois se relaciona a cada tópico calculado como uma média em todas as semanas. Preenchido somente quando a marca é realmente mencionada.
* **Posição**: a importância relativa da sua marca em respostas de IA, calculada como uma média em todas as semanas.
* **Todas as citações**: o número de origens únicas citadas nas respostas de IA para este tópico ou esta combinação de tópico/prompt (inclui citações próprias).
* **Citações próprias**: o número de vezes que sua marca foi citada em respostas de IA para esta palavra-chave ou esta combinação de palavra-chave/pergunta.
  <!--* **Executions**-->

Você também pode ver detalhes adicionais sobre cada tópico clicando no ícone **Detalhes** no final de cada linha.

>[!TAB Participação de voz]

A tabela Participação de voz oferece uma visão comparativa do desempenho da sua marca em relação a tópicos-chave nas respostas da IA generativa. Ela ajuda a identificar lacunas de visibilidade, acompanhar o desempenho da concorrência e priorizar áreas para otimização. Ela exibe as seguintes métricas:

* **Tópico**: o tópico analisado.
* **Popularidade**: o volume de buscas pelo tópico em relação a todos os outros tópicos em sua análise.
* **Menções**: número de vezes que sua marca foi mencionada nas respostas da IA para o tópico ou a combinação tópico/prompt.
* **Classificação**: a classificação da participação de voz da sua marca em relação a todas as outras marcas identificadas.
* **Participação de voz**: a porcentagem do total de menções que sua marca retém em respostas geradas por IA.
* **Outras 5 marcas principais**: as cinco principais marcas mencionadas com mais frequência nos mesmos tópicos. As marcas são organizadas por participação de voz (da maior para a menor).

>[!ENDTABS]

### Uso da tabela de insights de dados {#using-data-insights}

A tabela de insights de dados ajuda você a transformar métricas em ações, detalhando o desempenho por tópico e por prompt.

Principais maneiras de usar a tabela:

* Priorize tópicos de alta popularidade com baixa visibilidade: otimização de foco onde a demanda de público-alvo é forte, mas sua presença de marca é fraca.
* Monitorar alterações no sentimento: detecte tópicos em que as menções estão em tendência negativa ou neutra e coordene sua resposta.
* Comparar citações com citações próprias: identifique prompts nos quais sua marca é mencionada, mas que também citam o conteúdo de outra marca, sinalizando uma lacuna de conteúdo.
* Avaliar o intervalo de posição: monitore se a sua marca aparece antecipadamente nas respostas de IA (posições 1-3) ou mais abaixo (6-10).
