---
title: Tráfego de referência
description: Saiba como usar o painel Tráfego de referência para ver como os visitantes chegam ao seu site a partir de plataformas externas, citações de IA e links de referência.
source-git-commit: a699f8f3c50f77d07f29cd354fd1ef8e6eed8ff9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Tráfego de referência

O Tráfego de referência mostra como os visitantes chegam ao seu site a partir de plataformas externas, citações de IA e links de referência. Ele rastreia e analisa fontes de tráfego, padrões de referência e métricas de conversão de sites e plataformas externas. Isso ajudará você a entender quais fontes, regiões e páginas direcionam o tráfego mais engajado. Os dados são obtidos dos logs CDN ou da [Telemetria Operacional do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/operational-telemetry-for-aem-as-a-cloud-service). Ambas as fontes preservam a privacidade e não capturam dados pessoais do usuário. Também há filtros personalizáveis para ajudá-lo a refinar os dados exibidos.

![Página de indicação](/help/dashboards/assets/referral-traffic.png)

Esta página detalha o seguinte:

* [Configurar](#setup)
* [Filtros](#filters)
* [Desempenho geral da referência](#overall-performance)
* [Principais URLs de referência](#top-referrals)
* [Detalhes do tráfego de referência](#traffic-details)

## Configurar {#setup}

No primeiro logon, o painel Tráfego de referência pode aparecer em branco. Para exibir seus dados, você deve configurar um provedor de tráfego de referência, selecionando **Ir para Configuração**.

![Configuração de Referência](/help/dashboards/assets/referral-setup1.png)

<!--- 1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM-->

Depois que um provedor de tráfego de referência for selecionado, o painel será preenchido com métricas de tráfego de referência.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
* **Plataforma** - Escolha uma fonte de tráfego específica, como Google, OpenAI ou redes sociais.
* **Intenção de página** - Filtrar o tráfego de referência por intenção de usuário.
* **Channel Source** - Filtrar pela origem do canal. as opções incluem: LLMs, canais de referência ganhos, pagos ou mistos.
* **Tipo de dispositivo** - Analise o tráfego pelo tipo de dispositivo do visitante: desktop, dispositivo móvel ou todos os dispositivos.
  **Região** - Exibir padrões de referência em diferentes regiões.

Após selecionar o filtro desejado, clique em **Aplicar Filtros** para aplicar a seleção ao painel.

## Desempenho geral da referência {#overall-performance}

O painel destaca o desempenho geral da indicação ao exibir as métricas principais, incluindo:

* **Tráfego de Referência Total** - O tráfego de referência total de todas as fontes.
* **Taxa de consentimento** - A porcentagem de visitantes que aceitam um prompt de consentimento.
* **Taxa de rejeição** - A porcentagem de sessões de fontes de referência que não tiveram evento de envolvimento.

![Página de indicação](/help/dashboards/assets/referral-traffic.png)

Além das métricas de desempenho gerais apresentadas acima, o painel **Regiões principais** detalha o tráfego por região. Enquanto isso, o painel **Principais Fontes de Referência** mostra as plataformas que estão promovendo mais visitas. Os indicadores de tendência das métricas mostram como esses valores estão mudando com o tempo em comparação ao período anterior.

<!--## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site’s most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)-->

## Detalhes de Origens de Referência e Análise de Desempenho de URL {#traffic-details}

As tabelas Detalhes das fontes de referência e Análise de desempenho de URL ajudam a avaliar o volume de tráfego e a qualidade. Clique em cada guia abaixo para obter mais detalhes:

![Detalhes do tráfego de referência](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB Detalhes de Indicação de Fontes]

A visualização Detalhes das fontes de referência detalha o tráfego proveniente de diferentes plataformas, como OpenAI, Microsoft, Google e Perplexity. Ele exibe métricas principais como visitas, taxa de rejeição e tipo de canal, ajudando você a entender quais fontes de IA e pesquisa estão direcionando o tráfego mais envolvido para o site.

* **Source** - A origem do tráfego de referência.
* **Visitas** - O número total de visitas para cada origem.
* **Taxa de rejeição** - A porcentagem de sessões da fonte de referência que não tiveram evento de envolvimento.
* **Canal** - O canal da origem, recebido, pago ou ambos.

>[!TAB Análise de Desempenho de URL]

A visualização Análise de desempenho de URL classifica as páginas com melhor desempenho com base no volume de tráfego de referência de LLMs e outras fontes. Ele destaca métricas como tráfego, taxa de rejeição, taxa de consentimento e intenção de página, ajudando a identificar quais páginas atraem e retêm os visitantes mais envolvidos com as referências orientadas por IA. A tabela tem um campo de pesquisa para acesso rápido aos tópicos.

>[!ENDTABS]

Em ambas as tabelas, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela de tráfego de referência em relatórios executivos.
