---
title: Inspetor de URL
description: Aprenda a usar o Inspetor de URL para analisar o desempenho de páginas específicas do seu domínio nas pesquisas de IA.
feature: URL Inspector
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: ht
source-wordcount: '687'
ht-degree: 100%

---


# Inspetor de URL

O Inspetor de URL ajuda você a analisar o desempenho de páginas específicas do seu domínio nas pesquisas de IA. Ele combina visibilidade, tráfego agêntico e dados de referência no nível do URL para fornecer uma visualização granular de quais URLs são citados e com que frequência eles aparecem nas respostas.

![Inspetor de URL](/help/dashboards/assets/url-insp.png)

## Filtros

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetam **todas** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas**: selecione o intervalo de tempo dos dados exibidos. Por exemplo, as últimas 4 semanas. Também é possível personalizar o período selecionando a opção **Semanas personalizadas**.
* **Categoria**: filtre os resultados exibidos por categorias.
* **Plataforma**: escolha qual mecanismo de IA analisar.
* **Tipo de conteúdo da página**: filtre por tipo de conteúdo.
* **Região**: filtre os resultados por região. Nem todas as regiões estarão disponíveis no lançamento.

Após selecionar o filtro desejado, clique em **Aplicar filtros** para aplicar a seleção ao painel.

## Métricas de visão geral

O Inspetor de URL fornece várias métricas de visão geral para que você possa avaliar rapidamente como suas páginas estão se saindo nas pesquisas com IA. As seguintes métricas são fornecidas:

* **Prompts únicos com citações próprias**: o número total de prompts únicos de IA com citações próprias.
* **Total de prompts únicos**: o número total de prompts únicos de IA.
* **URLs únicos citados**: o número de URLs próprios únicos que foram citados.
* **Total de vezes citado**: o total de vezes que um URL próprio foi citado em respostas geradas por IA.
* **Total de ocorrências agênticas**: o número total de ocorrências de agentes de IA nos seus URLs.
* **Ocorrências de referência de LLMs**: o número total de ocorrências direcionadas de respostas geradas por IA para seus URLs.

Os indicadores de tendência para cada métrica de visão geral mostram como esses valores estão mudando ao longo do tempo em comparação com o período anterior.

## Seus URLs citados

A visualização de URLs citados lista todos os URLs da sua marca que foram citados em respostas geradas por IA, com métricas de apoio. Ambas as tabelas têm um campo de pesquisa para acesso rápido a tópicos, e você pode personalizar quais métricas são exibidas clicando no botão **Configurar colunas**. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela em relatórios executivos.

![URLs citados](/help/dashboards/assets/cited-urls.png)

As seguintes métricas são fornecidas:

* **URL**: o URL analisado.
* **Vezes citado**: o número de vezes que o URL foi citado em respostas geradas por IA.
* **Prompts que citaram**: o número de prompts únicos de IA que citaram o URL.
* **Categorias**: as categorias de produto ou tópicos associados ao URL.
* **Regiões**: a região geográfica onde o URL foi citado.
* **Ocorrências agênticas**: o número total de ocorrências de agentes de IA nos URLs.
* **Ocorrências de referência**: o número de ocorrências direcionadas de respostas geradas por IA para os URLs.

## URLs em alta competindo por citações

A visualização “URLs em alta competindo por citações” destaca URLs externos que estão atualmente citados em respostas relevantes para sua marca, a fim de medir quem está ganhando citações no seu segmento. A tabela de dados possui um campo de pesquisa para acesso rápido a URLs específicos. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela em relatórios executivos.

![URLs em alta competindo por citações](/help/dashboards/assets/trend-url.png)

As seguintes métricas são fornecidas:

* **URL**: o URL analisado
* **Tipo de conteúdo**: o tipo de conteúdo (próprio, social, orgânico, outro).
* **Vezes citado**: o número de vezes que o URL foi citado em respostas geradas por IA.
* **Prompts que citaram**: o número de prompts de IA exclusivos que citaram o URL.
* **Categorias**: as categorias ou tópicos de produtos associados ao URL.
* **Regiões**: a região geográfica onde o URL foi citado.

### Janela de detalhes

Nas exibições de citações e tendência, os URLs têm um botão **Detalhes** no final de cada linha. Clicar no botão exibe uma janela separada com detalhes adicionais. A janela de detalhes mostra a frequência com que o URL é citado, <!--the sentiment of AI responses where it is mentioned,-->, os tópicos e prompts em que ele aparece e as tendências de tráfego agêntico e de referência ao longo do tempo (para URLs próprios).

![Janela de detalhes](/help/dashboards/assets/details-url.png)
