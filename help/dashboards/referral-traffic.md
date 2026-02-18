---
title: Tráfego de referência
description: Saiba como usar o painel Tráfego de referência para ver como visitantes chegam ao seu site a partir de plataformas externas, citações de IA e links de referência.
feature: Referral Traffic
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: ht
source-wordcount: '605'
ht-degree: 100%

---


# Tráfego de referência

O Tráfego de referência mostra como os visitantes chegam ao site a partir de plataformas externas, citações de IA e links de referência. Ele rastreia e analisa fontes de tráfego, padrões de referência e métricas de conversão de plataformas e sites externos. Isso ajudará você a entender quais fontes, regiões e páginas direcionam o tráfego mais engajado. <!--Data is sourced from the CDN logs, a privacy-preserving source that does not capture personal user data.--> Também há filtros personalizáveis para ajudar você a refinar os dados exibidos.

![Página de referência](/help/dashboards/assets/referral-traffic.png)

Esta página detalha o seguinte:

* [Configuração](#setup)
* [Filtros](#filters)
* [Desempenho geral de referência](#overall-performance)
* [Principais URLs de referência](#top-referrals)
* [Detalhes do tráfego de referência](#traffic-details)

## Configuração {#setup}

No primeiro logon, o painel Tráfego de referência pode aparecer em branco. Para exibir os dados, você deve configurar o [Encaminhamento de logs da CDN](/help/dashboards/customer-configuration.md#cdn-configuration), selecionando **Ir para a configuração**.

![Configuração de referência](/help/dashboards/assets/referral-setup1.png)

<!--- 1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM-->

Uma vez ativado, o painel será preenchido com métricas de tráfego de referência.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetam **todas** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas**: selecione o intervalo de tempo dos dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período selecionando a opção **Semanas personalizadas**.
* **Plataforma**: escolha uma fonte de tráfego específica, como Google, OpenAI ou redes sociais.
* **Intenção da página**: filtre o tráfego de referência por intenção do usuário.
* **Origem do canal**: filtre pela origem do canal. As opções incluem: LLMs, canais de referência orgânica, pagos ou mistos.
* **Tipo de dispositivo**: analise o tráfego pelo tipo de dispositivo do visitante: desktop, dispositivo móvel ou todos os dispositivos.
  **Região**: visualize padrões de referência em diferentes regiões.

Após selecionar o filtro desejado, clique em **Aplicar filtros** para aplicar a seleção ao painel.

## Desempenho geral de referência {#overall-performance}

O painel destaca o desempenho geral da referência ao exibir as métricas principais, incluindo:

* **Tráfego de referência total**: o tráfego de referência total de todas as fontes.
* **Tráfego de referência do LLM**: o tráfego de referência total do LLM.
* **Taxa de consentimento**: a porcentagem de visitantes que aceitam um prompt de consentimento.
* **Taxa de rejeição**: a porcentagem de sessões de fontes de referência que não tiveram eventos de engajamento.

![Página de referência](/help/dashboards/assets/referral-traffic.png)

Além das métricas de desempenho gerais apresentadas acima, há três painéis adicionais que mostram a distribuição do tráfego em diferentes mercados, fontes de referência e categorias de intenção de página <!-- the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits. Trend indicators for the metrics show how these values are changing over time compared to the previous period.-->

<!--## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site's most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)-->

## Detalhes de fontes de referência e Análise de desempenho do URL {#traffic-details}

As tabelas Detalhes das fontes de referência e Análise de desempenho do URL ajudam a avaliar o volume de tráfego e a qualidade. Clique em cada guia abaixo para obter mais detalhes:

![Detalhes do tráfego de referência](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB Detalhes das fontes de referência]

A visualização Detalhes das fontes de referência detalha o tráfego proveniente de diferentes plataformas, como OpenAI, Microsoft, Google e Perplexity. Ela exibe métricas principais como visitas, taxa de rejeição e tipo de canal, ajudando você a entender quais fontes de IA e pesquisa estão direcionando o tráfego mais engajado para o site.

* **Origem**: a origem do tráfego de referência.
* **Visitas**: o número total de visitas de cada origem.
* **Taxa de rejeição**: a porcentagem de sessões da fonte de referência que não tiveram eventos de engajamento.
* **Canal**: o canal da origem: orgânico, pago ou ambos.

>[!TAB Análise de desempenho do URL]

A visualização Análise de desempenho do URL classifica as páginas com melhor desempenho com base no volume do tráfego de referência de LLMs e outras fontes. Ela destaca métricas como tráfego, taxa de rejeição, taxa de consentimento e intenção da página, ajudando a identificar quais páginas atraem e retêm os visitantes mais engajados com as referências promovidas pela IA. A tabela tem um campo de pesquisa para acesso rápido aos tópicos.

>[!ENDTABS]

Em ambas as tabelas, você pode usar a opção **Exportar** para baixar a tabela em .csv e compartilhar os insights com a sua equipe ou incluir as tabelas em relatórios executivos. Além disso, ambas as tabelas permitem personalizar quais métricas são exibidas clicando no botão **Configurar colunas**.
