---
title: Inspetor de URL
description: Saiba como usar o Inspetor de URL para analisar o desempenho de páginas específicas do seu domínio em pesquisas de IA.
feature: URL Inspector
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---


# Inspetor de URL

O Inspetor de URL ajuda a analisar o desempenho de páginas específicas do seu domínio em pesquisas de IA. Ele combina visibilidade, tráfego agenciador e dados de referência no nível do URL para fornecer uma visualização granular de quais URLs são citados e com que frequência eles aparecem nas respostas.

![Inspetor de URL](/help/dashboards/assets/url-insp.png)

## Filtros

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
* **Categoria** - Filtre os resultados exibidos por categorias.
* **Plataforma** - Escolha qual mecanismo de IA analisar.
* **Tipo de conteúdo da página** - Filtrar por tipo de conteúdo.
* **Região** - Filtrar os resultados por região. Nem todas as regiões estarão disponíveis no lançamento.

Após selecionar o filtro desejado, clique em **Aplicar Filtros** para aplicar a seleção ao painel.

## Métricas de visão geral

O Inspetor de URL fornece várias métricas de visão geral para que você possa avaliar rapidamente o desempenho de suas páginas em pesquisas de IA. As seguintes métricas são fornecidas:

* **Solicitações exclusivas com o citação própria** - O número total de solicitações exclusivas do AI com o citação própria.
* **Total de prompts exclusivos** - O número total de prompts exclusivos de IA.
* **URLs citadas únicas** - O número de URLs de propriedade exclusiva que foram citadas.
* **Total de citações** - Total de vezes que uma URL própria foi citada em respostas geradas por IA.
* **Total de ocorrências de agente** - O número total de ocorrências de agentes de IA em suas URLs.
* **Consulta de ocorrências de LLMs** - O número total de ocorrências direcionadas de respostas geradas por IA para suas URLs.

Os indicadores de tendência para cada métrica de visão geral mostram como esses valores estão mudando com o tempo em comparação com o período anterior.

## Seus URLs citados

A visualização de URLs citados lista todos os URLs da sua marca que foram citados em respostas geradas por IA, com métricas de suporte. Ambas as tabelas têm um campo de pesquisa para acesso rápido a tópicos e você pode personalizar quais métricas são exibidas clicando no botão **Configurar Colunas**. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela nos relatórios executivos.

![URLs citadas](/help/dashboards/assets/cited-urls.png)

As seguintes métricas são fornecidas:

* **URL** - a URL analisada.
* **Citações** - O número de vezes que a URL foi citada em respostas geradas por IA.
* **Solicitações citadas em** - O número de solicitações de IA exclusivas que citaram a URL.
* **Categorias** - As categorias de produtos ou os tópicos associados à URL.
* **Regiões** - A região geográfica onde a URL foi citada.
* **Ocorrências de agente** - O número total de ocorrências de agentes de IA nas URLs.
* **Ocorrências de referência** - O número de ocorrências direcionadas de respostas geradas por IA para as URLs.

## URLs em alta competindo por citações

Os URLs de tendência que competem pela visualização de citações destacam URLs externos que são atualmente citados em respostas relevantes para sua marca, medindo quem está ganhando citações em seu espaço. A tabela de dados tem um campo de pesquisa para acesso rápido a URLs específicos. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela nos relatórios executivos.

![URLs de tendência competindo por Citações](/help/dashboards/assets/trend-url.png)

As seguintes métricas são fornecidas:

* **URL** - a URL analisada
* **Tipo de Conteúdo** - O tipo de conteúdo (próprio, social, ganho, outro).
* **Citações** - O número de vezes que a URL foi citada em respostas geradas por IA.
* **Solicitações citadas em** - O número de solicitações de IA exclusivas que citaram a URL.
* **Categorias** - As categorias de produtos ou os tópicos associados à URL.
* **Regiões** - A região geográfica onde a URL foi citada.

### Janela de detalhes

Para as exibições citada e de tendência, as URLs têm um botão **Detalhes** no final de cada linha. Clicar no botão exibirá uma janela separada com detalhes adicionais. A janela de detalhes mostra a frequência com que a URL é citada, <!--the sentiment of AI responses where it is mentioned,--> os tópicos e prompts em que ela aparece e as tendências na agilidade e no tráfego de referência ao longo do tempo (para URLs próprias).

![Janela de detalhes](/help/dashboards/assets/details-url.png)
