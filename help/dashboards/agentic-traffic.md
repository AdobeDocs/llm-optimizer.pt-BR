---
title: Tráfego de agente
description: Saiba como usar o painel Tráfego do agente para ver como os agentes de IA interagem com seu site.
source-git-commit: 4cbfbe420a8419a04c2d6c465b6a290ee00ff3d4
workflow-type: tm+mt
source-wordcount: '1127'
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

## Encaminhamento de log CDN {#cdn-setup}

Sem o **encaminhamento de log da CDN**, o painel Tráfego do Agente está em branco. Para exibir interações de agente, você deve configurar o **encaminhamento de log CDN**.  No primeiro logon, você verá uma mensagem como mostrado na imagem abaixo.

![Configuração da CDN](/help/dashboards/assets/ag-log-forward1.png)

Selecione **Ir para Configuração** e você navegará automaticamente para a guia **Configuração da CDN** do [painel de configuração do cliente](/help/dashboards/customer-configuration.md).

![Instalação do CDN integrada](/help/dashboards/assets/ag-log-forward2.png)

Nesta guia, selecione **Onboard CDN**. E a janela do provedor CDN é exibida.

![Provedor da CDN](/help/dashboards/assets/ag-log-forward3.png)

Na janela **Onboard CDN Provider**:

1. Selecione seu provedor de CDN (por exemplo, Akamai, Fastly gerenciado pela Adobe, Fastly, AWS Cloudfront, Azure CDN, Cloudflare ou Outro).
2. Clique em **Integrar** para habilitar o encaminhamento de log.

Se você selecionar **Outros**, precisará entrar em contato com a Adobe para obter assistência.

Depois de ativados, os registros são assimilados e o painel é preenchido com métricas como total de interações do agente, taxa de sucesso, ocorrências por mercado, análise do agente do usuário e desempenho em nível de URL.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todos** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas** - Selecione o intervalo de tempo para os dados exibidos. Por exemplo, as últimas 4 semanas. Você também pode personalizar o período de tempo selecionando a opção **Semanas personalizadas**.
* **Categoria** - Filtre os resultados exibidos por categorias predefinidas ou categorias personalizadas.
* **Plataforma** - Escolha qual mecanismo de IA analisar.
* **Tipo de Agente** - Filtre pelo tipo de agente de IA que interagiu com o site. Você pode filtrar entre rastreadores, chatbots ou todos os agentes.
* **Taxa de Sucesso** - Filtre pela qualidade da interação (alta, média ou baixa). Essa métrica representa a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas diretas bem-sucedidas (códigos de status 2xx) e redirecionamentos (códigos de status 3xx).
* **Tipo de Conteúdo** - Exiba a interação de agente para diferentes tipos de conteúdo, como HTML, PDF e assim por diante.

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

A visualização Top and Bottom Movers destaca os URLs com as maiores alterações semana a semana no tráfego de agentes — visitas ou ocorrências de sistemas de IA que acessam seu conteúdo. Os Top Movers mostram as páginas ganhando visibilidade ou engajamento, enquanto os Bottom Movers revelam URLs com os declínios mais acentuados. Isso ajuda a identificar rapidamente qual conteúdo está com tendência para cima, qual pode precisar de atenção e onde os padrões de descoberta orientados por IA estão mudando.

![Movimentadores Superior e Inferior](/help/dashboards/assets/movers.png)

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

A tabela de desempenho de URL tem um campo de pesquisa para acesso rápido a URLs. Você também pode exibir detalhes adicionais para cada URL clicando no ícone de informações no final de cada linha.

![Detalhes da URL](/help/dashboards/assets/details.png)

A visualização Detalhes do URL fornece uma compreensão holística do desempenho de uma página, mostrando a frequência com que ela é citada, o sentimento das respostas de IA onde é mencionada, os tópicos e prompts em que ela aparece, e as tendências no tráfego de referência e agêntica ao longo do tempo.

>[!ENDTABS]

Para ambas as tabelas, você pode usar a opção **Exportar** para baixar a tabela .csv e compartilhar os insights com sua equipe ou incluir a tabela em relatórios executivos.
