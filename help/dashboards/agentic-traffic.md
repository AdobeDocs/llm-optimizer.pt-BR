---
title: Tráfego agêntico
description: Saiba como usar o painel Tráfego agêntico para ver como os agentes de IA interagem com o site.
feature: Agentic Traffic
source-git-commit: 26926f3ed4df3a408b74b0208f0d1eb064b97d28
workflow-type: ht
source-wordcount: '1316'
ht-degree: 100%

---


# Tráfego agêntico {#agentic-traffic}

O painel Tráfego agêntico mostra como os agentes de IA (rastreadores e chatbots) interagem com o site. Ao usar essa visualização, é possível monitorar o número total de solicitações e as métricas gerais relacionadas ao desempenho. Também é possível visualizar a distribuição do tráfego em mercados, categorias, páginas e agentes. Os dados usados por esse painel são provenientes dos logs da CDN, portanto, é necessário configurar o **encaminhamento de log da CDN** para exibir as métricas. Também há filtros personalizáveis para ajudar você a refinar os dados exibidos.

![Distribuição de tráfego](/help/dashboards/assets/ag-main.png)

Esta página detalha o seguinte:

* [Filtros](#filters)
* [Configuração da CDN](#cdn-setup)
* [Distribuição do tráfego](#traffic-distribution)
* [Tendências do tráfego agêntico](#agentic-trends)
* [Melhor e pior desempenho](#top-bottom-movers)
* [Agente de usuário e a análise de desempenho do URL](#user-url-performance)

## Encaminhamento de logs da CDN {#cdn-setup}

Sem o **encaminhamento de logs da CDN**, o painel Tráfego agêntico fica em branco. Para exibir interações agênticas, é necessário configurar o **encaminhamento de logs da CDN**.  No primeiro logon, uma mensagem será visualizada, conforme exibido na imagem abaixo.

![Configuração da CDN](/help/dashboards/assets/ag-log-forward1.png)

Selecione **Ir para a configuração** para navegar automaticamente para a guia **Configuração da CDN** do [painel de configuração do cliente](/help/dashboards/customer-configuration.md).

![Integrar configuração da CDN](/help/dashboards/assets/ag-log-forward2.png)

Nesta guia, selecione **Integrar CDN**. E a janela do provedor da CDN é exibida.

<!-- [CDN Provider](/help/dashboards/assets/ag-log-forward3.png)-->
Na janela **Integrar provedor de CDN**:

1. Selecione seu provedor de CDN (por exemplo: Akamai, Fastly gerenciado pela Adobe, Fastly, AWS Cloudfront, Azure CDN, Cloudflare ou outro).
2. Clique em **Integrar** para habilitar o encaminhamento de logs.

Caso selecione **Outro**, você precisará entrar em contato com llmo-now@adobe.com para obter ajuda.

Depois de ativados, os logs são ingeridos e o painel será preenchido com métricas como total de interações do agente, taxa de sucesso, ocorrências por mercado, análise do agente do usuário e desempenho no nível do URL.

O LLM Optimizer processa um subconjunto de campos dos logs da CDN. Embora os nomes de campo brutos de logs variem de acordo com o provedor da CDN, eles são normalizados e apresentados como:

* URL (somente caminho)
* Agente do usuário
* Código de status
* Cabeçalho do referenciador
* Cabeçalho do host
* Tempo até o primeiro byte (TTFB)
* Método de solicitação
* Carimbo de data e hora
* Tipo de conteúdo

Esses campos normalizados são expostos por meio da visualização agêntica. No painel [Tráfego de referência](/help/dashboards/referral-traffic.md), os logs da CDN são utilizados para exibir as métricas de contagem de visitas.Nenhuma informação pessoal identificável (PII) é processada ou armazenada em qualquer estágio da ingestão de logs da CDN ou do tratamento de dados subsequente.

## Filtros {#filters}

Na parte superior da página, é possível aplicar filtros para refinar a visualização. Os filtros escolhidos afetarão **todas** as seções presentes no painel. Você pode personalizar o seguinte:

* **Intervalo de datas**: selecione o intervalo de tempo dos dados exibidos. Por exemplo, as últimas 4 semanas. Existe também a opção de personalizar o período de tempo ao selecionar **Semanas personalizadas**.
* **Categoria**: filtre os resultados exibidos por categorias predefinidas ou categorias personalizadas.
* **Plataforma**: escolha um mecanismo de IA para analisar.
* **Tipo de agente**: filtre pelo tipo de agente de IA que interagiu com o site. É possível filtrar entre rastreadores, chatbots ou todos os agentes.
* **Taxa de sucesso**: filtre pela qualidade da interação (alta, média ou baixa). Essa métrica representa a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas diretas bem-sucedidas (códigos de status 2xx) e redirecionamentos (códigos de status 3xx).
* **Tipo de conteúdo**: veja a interação agêntica de diferentes tipos de conteúdo, como HTML, PDF e assim por diante.

Após selecionar o filtro desejado, clique em **Aplicar filtros** para aplicar a seleção ao painel.

## Distribuição do tráfego {#traffic-distribution}

A exibição Distribuição do tráfego mostra como o tráfego de agentes é distribuído entre mercados, categorias e tipos de página. Dessa forma, essa exibição ajuda a determinar quais regiões geográficas, áreas de produtos ou formatos de conteúdo são acessados com mais frequência pelos agentes de IA ao interagirem com o site.

![Distribuição de tráfego](/help/dashboards/assets/ag-main.png)

Na parte superior da página, há três métricas principais das quais é necessário ter conhecimento:

* **Interações agênticas**: representa o número total de solicitações feitas ao site pelos agentes de IA. Isso inclui todo o tráfego de mecanismos de pesquisa, chatbots e qualquer outro tráfego não humano.
* **Taxa de sucesso**: representa a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas e redirecionamentos diretos bem-sucedidos.
* **TTFB médio**: tempo até o primeiro byte (TTFB) mede o tempo necessário para que o primeiro byte dos dados seja recebido do servidor. O valor médio é ponderado com base no número de solicitações que retornam cada código e exclui solicitações que resultaram em respostas 5xx. Valores mais baixos indicam tempos de resposta mais rápidos do servidor.

Os indicadores de tendência de cada métrica principal mostram como esses valores mudam com o tempo em comparação ao período anterior.

## Tendências do tráfego agêntico {#agentic-trends}

Use o gráfico de tendências do tráfego agêntico para monitorar os totais semanais de ocorrências bem-sucedidas, com falha e gerais. Dessa forma, é possível monitorar as alterações na atividade e no desempenho do agente ao longo do tempo. Você também pode passar o mouse ao longo do gráfico para ver a evolução dos dados ao longo do intervalo de tempo semanal.

![Tendências do tráfego agêntico](/help/dashboards/assets/ag-trends.png)

## Melhor e pior desempenho {#top-bottom-movers}

A exibição Desempenhos superiores e inferiores destaca os URLs com as maiores alterações de semana a semana no tráfego agêntico: visitas ou ocorrências de sistemas de IA que acessam o conteúdo. **Desempenhos superiores** mostra páginas ganhando visibilidade ou engajamento, enquanto **Desempenhos inferiores** revela os URLs com declínios mais acentuados. Isso ajuda a identificar rapidamente qual conteúdo está em tendência de crescimento, qual pode precisar de atenção e onde os padrões de descoberta orientados por IA estão mudando.

![Desempenhos superiores e inferiores](/help/dashboards/assets/movers.png)

## Agente de usuário e a análise de desempenho do URL {#user-url-performance}

As exibições Agente do usuário e Análise de desempenho do URL fornecem detalhamentos de dados adicionais sobre como rastreadores e chatbots interagem com o site. Clique nas guias abaixo para obter descrições detalhadas.

![Agente do usuário e Análise de desempenho do URL](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB Análise de agente do usuário]

A tabela Análise de agente do usuário fornece um detalhamento do tráfego por tipo de página e tipo de agente (por exemplo: rastreadores versus chatbots). Dessa forma, é fácil entender quais agentes de IA estão rastreando quais partes do site. Ela contém as seguintes categorias:

* **Tipo de página**: o tipo de página.
* **Tipo de agente**: o agente de IA que investiga a página, seja um rastreador ou um chatbot.
* **Ocorrências**: o número total de solicitações feitas pelos agentes de IA para esse tipo de página específico.

É possível personalizar quais métricas são exibidas ao clicar em **Configurar colunas**.

>[!TAB Análise de desempenho do URL]

A tabela Análise de desempenho do URL mostra uma exibição detalhada de URLs individuais. Isso inclui ocorrências, agentes únicos, agente principal, taxas de sucesso e categorias. Dessa forma, é possível identificar páginas de alto valor, detectar lacunas no rastreio e otimizar o conteúdo para mecanismos de IA. Os URLs são classificados por volume de tráfego. A tabela contém as seguintes categorias:

* **URL**: o URL examinado.
* **Total de ocorrências**: número total de solicitações feitas por agentes de AI ao URL.
* **Agentes únicos**: número dos agentes de IA distintos que acessaram o URL.
* **Agente principal**: o agente de IA que gerou o maior tráfego para o URL.
* **Tipo do agente principal**: tipo do agente de IA que gerou o maior tráfego para este URL.
* **Taxa de sucesso**: a porcentagem de solicitações HTTP bem-sucedidas, incluindo respostas e redirecionamentos diretos bem-sucedidos.
* **Categoria**: categoria que melhor corresponde ao conteúdo da página.
* **TTFB médio (ms)**: tempo até o primeiro byte (TTFB) mede o tempo necessário para que o primeiro byte dos dados seja recebido do servidor (em milissegundos). O valor médio é ponderado com base no número de solicitações que retornam cada código e exclui solicitações que resultaram em respostas 5xx. Valores mais baixos indicam tempos de resposta mais rápidos do servidor.
* **Códigos de resposta**: os códigos de status HTTP observados para o URL.

A tabela de desempenho de URL tem um campo de pesquisa para acesso rápido a URLs e é possível personalizar quais métricas serão exibidas ao clicar em **Configurar colunas**. Também é possível exibir detalhes adicionais de cada URL ao clicar no ícone **Detalhes** no final de cada linha.

![Detalhes do URL](/help/dashboards/assets/details.png)

A exibição Detalhes do URL fornece uma compreensão integral do desempenho de uma página, mostrando a frequência com que ela é citada, o sentimento das respostas de IA onde é mencionada, os tópicos e prompts em que ela aparece e as tendências no tráfego agêntico e de referência ao longo do tempo.

>[!ENDTABS]

Em ambas as tabelas, é possível usar a opção **Exportar** para baixar a tabela `.csv` e compartilhar os insights com sua equipe ou incluir as tabelas em relatórios executivos.
