---
title: Inspetor de URL
description: Saiba como usar o Inspetor de URL para analisar o desempenho de páginas específicas do seu domínio em pesquisas de IA.
source-git-commit: 5e8efde82c10c9afa09d51ec9ef20fc006363210
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

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

* **Solicitações exclusivas com citações próprias** - O número total de solicitações exclusivas de IA com citações próprias.
* **Total de prompts exclusivos** - O número total de prompts exclusivos de IA.
* **URLs citadas únicas** - O número de URLs de propriedade exclusiva que foram citadas.
* **Total de citações** - Total de vezes que uma URL própria foi citada em respostas geradas por IA.
<!-- * **Total agentic hits** - The total number of hits from AI agents on your URLs.
* **Referral hits from LLMs** - The total number of hits directed from AI-generated answers to your URLs.-->

Os indicadores de tendência para cada métrica de visão geral mostram como esses valores estão mudando com o tempo em comparação com o período anterior.

## Seus URLs citados

A visualização de URLs citados lista todos os URLs da sua marca que foram citados em respostas geradas por IA, com métricas de suporte. A tabela de dados também tem um campo de pesquisa para acesso rápido a URLs específicos. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela nos relatórios executivos.

![URLs citadas](/help/dashboards/assets/cited-urls.png)

As seguintes métricas são fornecidas:

* **URL** - a URL analisada.
* **Citações** - O número de vezes que a URL foi citada em respostas geradas por IA.
* **Solicitações citadas em** - O número de solicitações de IA exclusivas que citaram a URL.
* **Categorias** - As categorias de produtos ou os tópicos associados à URL.
* **Regiões** - A região geográfica onde a URL foi citada.
* **Ocorrências de agente** - O número total de ocorrências de agentes de IA nas URLs.
* **Ocorrências de referência** - O número de ocorrências direcionadas de respostas geradas por IA para as URLs.

## URLs de tendência que competem por citações

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

Para as exibições citada e de tendências, os URLs têm um botão **Detalhes** quando você passa o mouse sobre um URL específico. Clicar no botão exibirá uma janela separada com detalhes adicionais. A janela de detalhes mostra a frequência com que o URL é citado, o sentimento das respostas da IA onde é mencionado, os tópicos e prompts em que ele aparece e as tendências no tráfego de referência e agêntica ao longo do tempo (para URLs próprios).

![Janela de detalhes](/help/dashboards/assets/details-url.png)
