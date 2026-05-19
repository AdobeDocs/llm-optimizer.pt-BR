---
title: Integração do Adobe Analytics
description: Saiba como conectar o Adobe Analytics ao LLM Optimizer para medir a descoberta orientada por IA, o engajamento de sites e os resultados comerciais no painel Tráfego de referência.
feature: Referral Traffic
autotag-review: '2026-05-15T17:29:50.263Z'
TQID: 'https://experienceleague.adobe.com/Wo-7p-mNQRrpS3EhmnS38UF1-IcaKEJpUz5H3BwY8Yo'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: e69d5a42-0217-4ca5-9396-a9a826a170da
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 879
ht-degree: 100%

---


# Integração do Adobe Analytics

A integração do Adobe Analytics conecta o LLM Optimizer aos dados do Adobe Analytics de sua organização para que você possa medir como a descoberta orientada por IA se traduz em engajamento real do site e resultados comerciais. Após a conclusão do processo de integração, os dados estarão disponíveis no painel **Tráfego de referência**, na guia **Impacto nos negócios**.

Ao vincular dados de análise com insights de visibilidade de IA, o LLM Optimizer ajuda a monitorar:

* Engajamento do usuário em páginas referenciadas por IA.
* Sinais de conversão vinculados a jornadas de descoberta de IA.
* Impacto no desempenho de otimizações GEO.

Essa integração preenche a lacuna entre a medição de visibilidade da IA e a análise de desempenho empresarial. As equipes agora podem ver não apenas onde a marca aparece nas respostas da IA, mas o que acontece depois que os usuários chegam.

## Disponibilidade {#availability}

>[!IMPORTANT]
>
>A integração do Adobe Analytics está incluída na oferta paga do LLM Optimizer. Os clientes que usam a versão de avaliação gratuita não poderão conectar o Adobe Analytics até fazerem a atualização para uma oferta paga.

## Conectar o Adobe Analytics ao painel Tráfego de referência {#connect}

O fluxo de conexão começa no painel [Tráfego de referência](/help/dashboards/referral-traffic.md) da seguinte maneira:

1. Abra o painel [Tráfego de referência](/help/dashboards/referral-traffic.md). A visualização padrão é **Insights de tráfego**.

   ![Painel Tráfego de referência, guia Insights de tráfego](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Selecione a guia **Impacto nos negócios**. Se nenhum provedor de análise estiver conectado, um banner será exibido: **Conecte-se para ver o impacto nos negócios**, com **Conecte-se ao Analytics**.

   ![Guia Impacto nos negócios com Conecte-se ao Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Selecione **Conecte-se ao Analytics**. Isso abre o painel [Configuração do cliente](/help/dashboards/customer-configuration.md) na guia **Analytics**.

   ![Configuração do cliente, guia Analytics](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. Em **Credenciais**, insira a **ID do cliente** e o **Segredo do cliente** e selecione **Verificar e continuar**. Observe o seguinte:

   * **Verificar e continuar** está disponível somente quando os dois campos estão preenchidos.
   * Após uma verificação bem-sucedida, os conjuntos de relatórios são carregados.
   * Use a **ID do cliente** e o **Segredo do cliente** de uma [conta técnica](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) que tenha acesso ao conjunto de relatórios necessário.

   ![Credenciais do Analytics e Verificar e continuar](/help/dashboards/assets/aa-integration-04-credentials.png)

1. Em **Configuração**, escolha um **Conjunto de relatórios**.

   Quando um conjunto de relatórios é selecionado, o LLM Optimizer carrega as opções de **Dimensão URL da página** disponíveis para esse conjunto.

   ![Conjunto de relatórios selecionado e dimensões carregando](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Escolha uma **Dimensão URL da página** (lista de dimensões específicas do conjunto) e selecione **Salvar e habilitar**.

   * A **Dimensão URL da página** permanece desabilitada até que um conjunto de relatórios seja selecionado e as dimensões sejam carregadas.
   * **Salvar e habilitar** está disponível somente após a seleção de uma dimensão URL da página.

   ![Dimensão URL da página e Salvar e habilitar](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. Depois de salvar, a configuração deve mostrar o status **Conectado**. É possível retornar ao painel Tráfego de referência com **Ir para o painel Tráfego de referência**. Em **Tráfego de referência** na guia **Impacto nos negócios**, o status deve aparecer como **Conectado ao Adobe Analytics**.

   ![Conectado ao Adobe Analytics na configuração e em Impacto nos negócios](/help/dashboards/assets/aa-integration-07-connected.png)

### Depois que você se conectar {#after-connect}

* O LLM Optimizer preenche retroativamente as **últimas quatro semanas completas do calendário** e a **semana atual do calendário até a data**.
* Após o preenchimento retroativo, os dados são atualizados **diariamente** com um pull do **dia anterior completo**.

>[!NOTE]
>
>O preenchimento retroativo pode levar algumas horas para ser concluído.

## Como funciona {#how-it-works}

### Configuração

Durante a configuração, você define qual conjunto de relatórios e dimensão de página o LLM Optimizer usa na ingestão do Adobe Analytics. A dimensão de página pode ser o mapeamento `variables/page` padrão ou um `eVar` personalizado, dependendo do conjunto de relatórios.

### Como o tráfego LLM é identificado

O tráfego originado por LLM é identificado usando [Tipo de referenciador — Ferramentas de IA para conversas](https://experienceleague.adobe.com/pt-br/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools) do Adobe Analytics.

### Dados ingeridos {#data-ingested}

Os seguintes dados são ingeridos pelo LLM Optimizer:

**Dimensões**

* Domínio do referenciador
* Tipo de referenciador
* País
* Tipo de dispositivo
* Dimensão da página selecionada

**Métrica**

* Visualizações da página
* Visitas
* Visitantes
* Entradas
* Saídas
* Rejeições
* Visitas de página única
* Tempo gasto
* Carrinhos
* Adições ao carrinho
* Remoções de itens do carrinho
* Visualizações do carrinho
* Check-outs
* Pedidos
* Receita
* Unidades

### Como o LLM Optimizer usa esses dados

Este conjunto de dados fornece insights do LLM Optimizer para:

* Desempenho do tráfego LLM em nível de página.
* Desempenho do referenciador em fontes de LLM.
* Tendências regionais e no nível do dispositivo.
* Resultados do comércio downstream.

## Perguntas frequentes {#faq}

P: A integração com o Adobe Analytics está disponível durante a versão de avaliação?

Não. A integração está disponível apenas para clientes que usam a versão paga do LLM Optimizer.

P: Quais dados são coletados ou armazenados?

Consulte o capítulo [Dados ingeridos](#data-ingested) acima. O LLM Optimizer funciona com métricas agregadas das APIs do Adobe Analytics autorizadas pela sua organização, e não com os dados brutos de cada ocorrência.

P: Como os dados são ingeridos?

Sua organização autoriza o LLM Optimizer a consultar as APIs do Adobe Analytics. O tráfego de referência alinhado às fontes do LLM é consumido por meio dessas APIs.

P: Com que frequência os dados são atualizados?

Os dados são atualizados **diariamente** (dia anterior completo após a conclusão do preenchimento retroativo).

P: Os dados brutos de cada ocorrência são armazenados no LLM Optimizer?

Não. Somente as métricas **agregadas** são usadas para entender os padrões e as tendências de tráfego.

P: URLs completos, strings de consulta ou conteúdo da página são armazenados?

É possível ingerir URLs completos usados para a dimensão de página selecionada. As strings de consulta e o conteúdo da página não são ingeridos para esta integração.

P: Os identificadores de usuário (ECID, endereço IP, IDs de cookies) são armazenados?

Não.

P: Por quanto tempo os dados ficam retidos?

Tenha em mente que as políticas de retenção podem evoluir. Atualmente, os dados são armazenados por tempo indeterminado.

P: Os dados são criptografados quando estão em trânsito e inativos?

Atualmente, os dados são criptografados quando estão em trânsito, não inativos. Isso pode mudar em atualizações futuras.

P: Os dados históricos são preenchidos retroativamente?

Sim. Após uma configuração bem-sucedida, as últimas quatro semanas completas do calendário e a semana atual são preenchidas retroativamente. Veja também [Depois que você se conecta](#after-connect).
