---
title: Presença da marca
description: Saiba como usar o painel Presença da marca para entender como sua marca é percebida no nível de respostas geradas por IA.
source-git-commit: a37c4e7d2e26f16dc10dc7bc39ba58ba1df77cd5
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 0%

---


# Presença da marca {#brand-presence}

O painel Presença da marca fornece uma visão geral detalhada sobre como sua marca é percebida no nível de respostas geradas por IA. Ele mostra onde, com que frequência e em que contexto sua marca é mencionada. Você pode usar o painel para medir a visibilidade, rastrear a citação e explorar as tendências do sentimento. O painel é dividido em várias seções, cada uma fornecendo insights diferentes. Também há filtros personalizáveis para ajudá-lo a refinar os dados exibidos.

![Presença na marca](/help/dashboards/assets/brand-main.png)

Esta página detalha o seguinte:

* [Filtros](#filters)
* [Métricas de visão geral](##key-metrics)
* [Comparação de outros](##others-comparison)
* [Tendência do sentimento](#sentiment-trend)
* [Insights de dados](#data-insights)

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
* **Categoria** - Filtre os resultados exibidos por categorias predefinidas ou personalizadas.
* **Plataforma** - Escolha qual mecanismo de IA analisar.
* **Origem dos Prompts** - Escolha a origem dos prompts. A origem pode ser inserida pelo usuário ou gerada pela IA.
* **Marcas do Prompt** - Filtre os resultados com ou sem marcas.
* **Região** - Filtrar os resultados por região. Nem todas as regiões estarão disponíveis no lançamento.

Após selecionar o filtro desejado, clique em **Aplicar Filtros** para aplicar a seleção ao painel.

## Métricas de visão geral {#overview-metrics}

O painel destaca três métricas muito importantes na parte superior da página: pontuação de visibilidade, menções e citações. Quanto menor for a contagem dessas métricas, pior será a percepção da sua marca, e você deverá agir para melhorar a presença da sua marca. Apresentamos abaixo uma breve descrição de cada métrica e o que ela representa.

![Métricas de visão geral](/help/dashboards/assets/overview-metrics.png)

### Pontuação de visibilidade {#visibility-score}

A pontuação de visibilidade é composta por fatores como: menções, citações, sentimento e classificação. Cada fator tem um certo &quot;peso&quot; associado a ele que aumenta na pontuação final.

### Menções {#mentions}

Essa métrica representa o número total de vezes que sua marca ou categorias foram mencionadas nos prompts de IA de amostra. Por exemplo, você tem a marca &quot;Coffe B&quot;, com as categorias &quot;Máquinas&quot; e &quot;Acessórios&quot;, e essa métrica conta o número total de vezes que elas aparecem nas respostas de IA de amostra.

### Citações {#citations}

Essa métrica representa o número de vezes que seu site foi referenciado como uma origem.

Os indicadores de tendência para cada métrica principal mostram como esses valores estão mudando com o tempo em comparação ao período anterior.

## Comparação de outros {#others-comparison}

Na seção de comparação de outras marcas, é possível selecionar até cinco outras marcas e comparar suas menções e citações com a sua marca. Dessa forma, você pode visualizar e comparar seu desempenho em relação a outras marcas.

![Outra Comparação](/help/dashboards/assets/other-comparison.png)

As outras marcas são selecionadas na lista suspensa e os gráficos são atualizados quando você clica em **Aplicar Filtros**. Os gráficos exibem menções semanais e citações semanais lado a lado. Você também pode passar o mouse ao longo do gráfico para ver a evolução dos dados ao longo do período semanal.

## Análise de tendência de sentimento {#sentiment-trend}

Na seção Análise de tendência do sentimento, você pode acompanhar como sua marca é percebida nas respostas da IA de amostra. A métrica de tendência do sentimento pode ser positiva, neutra ou negativa. Por exemplo, pode ser positivo se as respostas destacarem a qualidade do produto ou negativo se mencionarem um serviço ruim. O gráfico de tendências mostra as mudanças na percepção da marca semana a semana. A seção é preenchida somente depois que sua marca é mencionada.

![Tendência de sentimento](/help/dashboards/assets/sentiment-trend.png)

## Insights de dados e compartilhamento de voz {#data-insights}

Ao arredondar o painel para cima, temos duas tabelas importantes: insights de dados e compartilhamento de voz. As informações apresentadas nessas tabelas ajudarão você a identificar onde sua marca é forte e onde a otimização é necessária.

Usando a tabela **insights de dados**, você pode explorar tópicos e perguntas ao usuário para avaliar e otimizar o impacto do conteúdo. Os resultados são detalhados por tópicos e prompts. Enquanto isso, a tabela **compartilhamento de voz** compara a voz da sua marca a outras marcas em vários tópicos e ajuda você a identificar lacunas e priorizar tópicos futuros.

![Insights de Dados](/help/dashboards/assets/data-insights.png)

Ambas as tabelas têm um campo de pesquisa para acesso rápido aos tópicos. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela nos relatórios executivos.

Clique nas guias abaixo para obter detalhes sobre cada tabela e as métricas associadas.

>[!BEGINTABS]

>[!TAB Insights de Dados]

A tabela de insights de dados ajuda a explorar tópicos e prompts do usuário para avaliar e otimizar o impacto do conteúdo. Ela exibe as seguintes métricas:

* **Tópico** - A categoria de tópico representa as palavras-chave da SEO e as perguntas do usuário relacionadas à sua marca. Você pode clicar em para expandir cada tópico e ver prompts individuais analisados para a presença da marca. Cada tópico tem um botão **Detalhes** quando você passa o mouse sobre ele. Clicar no botão exibirá uma janela separada com mais detalhes.
* **Região** - exibe a região dos prompts.
* **Popularidade** - A categoria de popularidade representa o volume de pesquisa deste tópico em relação a todos os outros tópicos da análise. O valor pode ser Alto, Medium ou Baixo.
* **Pontuação de visibilidade** - A pontuação de visibilidade desse tópico. Ele reflete fatores ponderados como menções, citações, sentimento e classificação.
* **Menções** - O número de vezes que sua marca foi mencionada nas respostas da IA para este tópico ou esta combinação de tópico/prompt.
* **Sentimento** - A percepção da marca nas respostas da IA, pois está relacionada a cada tópico, calculada como uma média em todas as semanas. Preenchido somente quando sua marca é realmente mencionada.
* **Posição** - A proeminência relativa da sua marca em respostas de IA, calculada como uma média em todas as semanas.
* **Todas as citações** - O número de fontes exclusivas citadas nas respostas da IA para este tópico ou esta combinação de tópico/prompt (inclui citações próprias).
* **Citações próprias** - O número de vezes que sua marca foi citada em respostas de IA para esta palavra-chave ou esta combinação de palavra-chave/pergunta.

>[!TAB Compartilhamento de Voz]

A tabela Compartilhamento de voz fornece uma visão comparativa de como sua marca atua entre os principais tópicos nas respostas geradoras de IA. Ele ajuda a identificar lacunas de visibilidade, rastrear o desempenho competitivo e priorizar áreas para otimização. Ela exibe as seguintes métricas:

* **Tópico** - O tópico analisado.
* **Popularidade** - O volume de pesquisa do tópico relativo a todos os outros tópicos da análise.
* **Menções** - Número de vezes que sua marca foi mencionada nas respostas da IA para o tópico ou a combinação de tópico/prompt.
* **Classificação** - A classificação da Ação de Voz da sua marca, relativa a todas as outras marcas identificadas.
* **Compartilhamento de voz** - A porcentagem do total de menções que sua marca retém nas respostas geradas por IA.
* **Cinco principais** - As cinco principais marcas mencionadas com mais frequência para os mesmos tópicos. As marcas são organizadas por seu Share of Voice (do mais alto para o mais baixo).

>[!ENDTABS]

### Uso da Tabela de Insights de Dados {#using-data-insights}

A Tabela de insights de dados ajuda você a mover de métricas para ações, detalhando o desempenho no nível de tópico e prompt.

Principais maneiras de usar a tabela:

* Priorize tópicos de alta popularidade com baixa visibilidade - otimização de foco onde a demanda de público-alvo é forte, mas a presença da sua marca é fraca.
* Rastrear as alterações do sentimento - detecte tópicos onde as menções são tendenciosas, negativas ou neutras, e coordene sua resposta.
* Comparar citações versus citações próprias - identifique prompts nos quais sua marca é mencionada, mas o conteúdo de outra marca é citado, sinalizando uma lacuna de conteúdo.
* Avaliar a faixa de posição - monitore se sua marca aparece antecipadamente nas respostas de IA (posições 1-3) ou mais abaixo (6-10).
