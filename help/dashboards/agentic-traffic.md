---
title: Tráfego de agente
description: Saiba como usar o painel Tráfego do agente para ver como os agentes de IA interagem com seu site.
source-git-commit: e8ea9ae0d6592ea3d1e9945ec117f852112ba9d7
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Tráfego de agente {#agentic-traffic}

O painel Tráfego do agente mostra como os agentes de IA (rastreadores e chatbots) interagem com o site. Com essa visualização é possível rastrear o número total de solicitações e as métricas gerais relacionadas ao desempenho. Você também pode visualizar a distribuição do tráfego entre mercados, categorias, páginas e agentes. Os dados usados por esse painel são provenientes dos logs CDN, portanto, você deve configurar o **encaminhamento de logs CDN** para exibir as métricas. Também há filtros personalizáveis para ajudá-lo a refinar os dados exibidos.

Esta página detalha o seguinte:

* [Filtros](#filters)
* [Configuração da CDN](#cdn-setup)
* [Distribuição de tráfego](#traffic-distribution)
* [Tendências do tráfego de agente](#agentic-trends)
* [Movedores Superior e Inferior](#top-bottom-movers)
* [Análise de desempenho de URL e agente de usuário](#user-url-performance)

## Configuração da CDN {#cdn-setup}

No primeiro logon, o painel Tráfego do agente fica em branco. Para exibir interações de agente, você deve configurar o **encaminhamento de log CDN**. **TBD apontar para a configuração do CDN no início rápido/integração?**

![Configuração da CDN](/help/dashboards/assets/ag-log-forward.png)

1. Selecione seu provedor de CDN (por exemplo, Akamai, Fastly gerenciado pela Adobe, Fastly, AWS Cloudfront, Azure CDN, Cloudflare ou Outro).
2. Insira um email do contato principal.
3. Clique em **Solicitar Ativação** para habilitar o encaminhamento de log.

Depois de ativados, os registros são assimilados e o painel é preenchido com métricas como total de interações do agente, taxa de sucesso, ocorrências por mercado, análise do agente do usuário e desempenho em nível de URL.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
* **Categoria** - Filtre os resultados exibidos por categorias predefinidas. Você também pode adicionar categorias personalizadas a este campo (**SR**-como?).
* **Plataforma** - Escolha qual mecanismo de IA analisar.
* **Tipo de Agente** - Filtre pelo tipo de agente de IA que interagiu com o site. Você pode filtrar entre rastreadores, chatbots ou todos os agentes.
* **Taxa de Sucesso** - Filtre pela qualidade da interação (alta, média ou baixa). Essa métrica representa a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas e redirecionamentos diretos bem-sucedidos.
* **Tipo de Conteúdo** - Filtrar por tipo de conteúdo, HTML ou txt.

Após selecionar o filtro desejado, clique em **Aplicar Filtros** para aplicar a seleção ao painel.

## Distribuição de tráfego {#traffic-distribution}

A exibição de Distribuição de tráfego mostra como o tráfego do agente é distribuído entre mercados, categorias e tipos de página. Dessa forma, essa exibição ajuda você a determinar quais regiões geográficas, áreas de produtos ou formatos de conteúdo são acessados com mais frequência pelos agentes de IA ao interagirem com seu site.

![Distribuição de tráfego](/help/dashboards/assets/ag-main.png)

Na parte superior da página, há três métricas principais que você precisa saber:

* **Interações de agente** - Esta métrica representa o número total de solicitações feitas pelos agentes de IA ao seu site. Isso inclui todo o tráfego de mecanismos de pesquisa, chatbots e outro tráfego não humano.
* **Taxa de sucesso** - Essa métrica representa a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas e redirecionamentos diretos bem-sucedidos.
* **Média de TTFB** - Tempo até o Primeiro Byte (TTFB) mede o tempo necessário para o primeiro byte de dados ser recebido do servidor. Valores mais baixos indicam tempos de resposta mais rápidos do servidor.

Os indicadores de tendência para cada métrica principal mostram como esses valores estão mudando com o tempo em comparação ao período anterior.

## Tendências do tráfego de agente {#agentic-trends}

Use o gráfico de Tendências de Tráfego Agênico para rastrear os totais semanais de ocorrências bem-sucedidas, com falha e gerais. Dessa forma, você pode monitorar as alterações na atividade e no desempenho do agente ao longo do tempo. Você também pode passar o mouse ao longo do gráfico para ver a evolução dos dados ao longo do período semanal.

![Tendências do Tráfego de Agente](/help/dashboards/assets/ag-trends.png)

## Movedores Superior e Inferior {#top-bottom-movers}

Essas duas métricas classificam os URLs da seguinte maneira:

* **Principais movimentadores** - Os URLs com o maior aumento no tráfego de agente da semana mais antiga para a mais recente.
* **Bottom Movers** - URLs com a maior diminuição no tráfego de agente da semana mais antiga para a mais recente.

## Análise de desempenho de URL e agente de usuário {#user-url-performance}

As visualizações Agente do usuário e Análise de desempenho de URL fornecem detalhamentos adicionais de dados sobre como rastreadores e chatbots interagem com seu site. Clique nas guias abaixo para obter descrições detalhadas.

![Análise de Desempenho de URL e Agente de Usuário](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB Análise de usuário-agente]

A tabela Análise do agente do usuário fornece um detalhamento do tráfego por tipo de página e tipo de agente (por exemplo, crawlers versus chatbots). Dessa forma, é fácil entender quais agentes de IA estão rastreando quais partes do site. Ele contém as seguintes categorias:

* **Tipo de página** - O tipo de página.
* **Tipo de Agente** - O agente de IA que está rastreando a página, seja um rastreador ou um chatbot.
* **Ocorrências** - O número total de solicitações feitas pelos agentes de IA para esse tipo de página específico.

Você também pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar a análise do agente com sua equipe ou incluí-la nos relatórios executivos.

>[!TAB Análise de Desempenho de URL]

A tabela Análise de desempenho de URL mostra uma exibição detalhada de URLs individuais. Isso inclui ocorrências, agentes exclusivos, agente principal, taxas de sucesso e categorias. Dessa forma, você pode identificar páginas de alto valor, detectar lacunas de rastreamento e otimizar o conteúdo para mecanismos de IA. Os URLs são classificados por volume de tráfego. A tabela contém as seguintes categorias:

* **URL** - A URL examinada.
* **Total de ocorrências** - Número total de solicitações feitas pelos agentes de IA à URL.
* **Agentes únicos** - O número de agentes de IA diferentes que acessaram a URL.
* **Agente Principal** - O agente de IA que gerou mais tráfego para a URL.
* **Tipo de Agente Principal** - O tipo de agente de IA que gerou mais tráfego para esta URL.
* **Taxa de Êxito** - A porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas e redirecionamentos diretos bem-sucedidos.
* **Categoria** - A categoria que melhor corresponde ao conteúdo da sua página.

A tabela de desempenho de URL tem um campo de pesquisa para acesso rápido a URLs. Além disso, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela nos relatórios executivos.

>[!ENDTABS]
