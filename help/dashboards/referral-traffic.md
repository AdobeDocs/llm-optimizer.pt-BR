---
title: Tráfego de referência
description: Saiba como usar o painel Tráfego de referência para ver como os visitantes chegam ao seu site a partir de plataformas externas, citações de IA e links de referência.
source-git-commit: e8ea9ae0d6592ea3d1e9945ec117f852112ba9d7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Tráfego de referência

O Tráfego de referência mostra como os visitantes chegam ao seu site a partir de plataformas externas, citações de IA e links de referência. Ele rastreia e analisa fontes de tráfego, padrões de referência e métricas de conversão de sites e plataformas externas. Isso ajudará você a entender quais fontes, regiões e páginas direcionam o tráfego mais engajado. Os dados são originados dos logs CDN ou da Telemetria Operacional do AEM **(adicionar link)**. Ambas as fontes preservam a privacidade e não capturam dados pessoais do usuário.

Também há filtros personalizáveis para ajudá-lo a refinar os dados exibidos.

Esta página detalha o seguinte:

* [Configurar](#setup)
* [Filtros](#filters)
* [Desempenho geral da referência](#overall-performance)
* [Principais URLs de referência](#top-referrals)
* [Detalhes do tráfego de referência](#traffic-details)

## Configurar {#setup}

No primeiro logon, o painel Tráfego de referência pode aparecer em branco. Para exibir seus dados, você deve configurar um provedor de tráfego de referência.

![Configuração de Referência](/help/dashboards/assets/referral-setup.png)

1. Selecione sua Source (logs CDN ou Telemetria operacional da AEM).
2. Insira um email do contato principal.
3. Clique em **Solicitar ativação** para habilitar a assimilação de dados.

Uma vez ativado, o painel será preenchido com métricas de tráfego de referência.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

**Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
**Plataforma** - Escolha uma fonte de tráfego específica, como Google, OpenAI ou redes sociais.
**Canal** - Filtrar entre canais como ganho ou pago. Se preferir uma combinação entre os dois, selecione a opção **Todos os canais**.
**Channel Source** - Filtrar pela origem do canal. as opções incluem: exibição, pesquisa, referência, vídeo e redes sociais. Você também pode usar **Todas as plataformas** para exibir todas as fontes de canal.
**Tipo de dispositivo** - Analise o tráfego pelo tipo de dispositivo do visitante: desktop, dispositivo móvel ou todos os dispositivos.
**Região** - Exibir padrões de referência em diferentes regiões.

Após selecionar o filtro desejado, clique em **Aplicar Filtros** para aplicar a seleção ao painel.

## Desempenho geral da referência {#overall-performance}

O painel destaca o desempenho geral da referência ao exibir as seguintes métricas principais:

* **Tráfego de Referência Total** - O tráfego de referência total de todas as fontes.
* **Taxa de consentimento** - A porcentagem de visitantes que aceitam um prompt de consentimento.
* **Taxa de rejeição** - A porcentagem de sessões de fontes de referência que não tiveram evento de envolvimento.

![Página de indicação](/help/dashboards/assets/referral-traffic.png)

Além das métricas de desempenho gerais apresentadas acima, o painel **Regiões principais** detalha o tráfego por região. Enquanto isso, o painel **Principais Fontes de Referência** mostra as plataformas que estão promovendo mais visitas.

## Principais URLs de referência {#top-referrals}

A lista Principais URLs de referência exibe as páginas mais visitadas do site a partir de referências.

![Principais URLs de Referência](/help/dashboards/assets/top-url.png)

## Detalhes do tráfego de referência {#traffic-details}

A tabela Detalhes do tráfego de referência ajuda a avaliar o volume e a qualidade do tráfego. Ele fornece um detalhamento por origem, incluindo contagens de visitas, taxas de rejeição e tipo de canal.

![Detalhes do tráfego de referência](/help/dashboards/assets/traffic-details.png)

A tabela contém as seguintes categorias:

**Source** - A origem do tráfego de referência.
**Visitas** - O número total de visitas para cada origem.
**Taxa de rejeição** - A porcentagem de sessões da fonte de referência que não tiveram evento de envolvimento.
**Canal** - O canal da origem, recebido, pago ou ambos.

Você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela de tráfego de referência nos relatórios executivos.
