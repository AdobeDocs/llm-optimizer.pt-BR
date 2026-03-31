---
title: Integração do Adobe Analytics
description: Saiba como conectar o Adobe Analytics com o LLM Optimizer para medir a descoberta orientada por IA, o envolvimento do site e os resultados comerciais no painel do Tráfego de referência.
feature: Referral Traffic
source-git-commit: e7c9bc1d40267dc92608baa005f85f4be21cfda1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 2%

---


# Integração do Adobe Analytics

A integração do Adobe Analytics conecta o LLM Optimizer aos dados do Adobe Analytics de sua organização para que você possa medir como a descoberta orientada por IA se traduz em envolvimento real do site e resultados comerciais. Após a conclusão do processo de integração, os dados estarão disponíveis no painel **Tráfego de referência** na guia **Impacto nos negócios**.

Ao vincular dados de análise com insights de visibilidade de IA, o LLM Optimizer ajuda a rastrear:

* Engajamento do usuário em páginas referenciadas por IA.
* Sinais de conversão vinculados a jornadas de descoberta de IA.
* Impacto no desempenho de otimizações GEO.

Essa integração elimina a lacuna entre a medição de visibilidade da IA e a análise de desempenho comercial. As equipes agora podem ver não apenas onde a marca aparece nas respostas da IA, mas o que acontece depois que os usuários chegam.

## Disponibilidade {#availability}

>[!IMPORTANT]
>
>A integração do Adobe Analytics está incluída na oferta paga do LLM Optimizer. Os clientes que usam a avaliação gratuita não poderão conectar o Adobe Analytics até que atualizem para uma oferta paga.

## Conectar o Adobe Analytics ao painel do Tráfego de referência {#connect}

O fluxo de conexão começa no painel [Tráfego de referência](/help/dashboards/referral-traffic.md) da seguinte maneira:

1. Abra o painel [Tráfego de referência](/help/dashboards/referral-traffic.md). A exibição padrão é **Traffic Insights**.

   ![painel do Tráfego de referência, guia Insights de tráfego](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Selecione a guia **Impacto nos negócios**. Se nenhum provedor de análise estiver conectado, um banner será exibido: **Conectar-se para Ver o Impacto nos Negócios**, com **Conectar-se ao Analytics**.

   ![Guia Impacto nos Negócios com Conectar ao Analytics](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Selecione **Conectar ao Analytics**. Isso abre o painel [Configuração do cliente](/help/dashboards/customer-configuration.md) na guia **Analytics**.

   ![Configuração do cliente, guia Analytics](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. Em **Credenciais**, digite a **ID do Cliente** e o **Segredo do Cliente** e selecione **Verificar e Continuar**. Observe o seguinte:

   * **Verificar e Continuar** está disponível somente quando ambos os campos estão preenchidos.
   * Após uma verificação bem-sucedida, os conjuntos de relatórios são carregados.
   * Use a **ID do Cliente** e o **Segredo do Cliente** de uma [conta técnica](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) que tenha acesso ao conjunto de relatórios necessário.

   ![Credenciais do Analytics e Verificar e Continuar](/help/dashboards/assets/aa-integration-04-credentials.png)

1. Em **Configuração**, escolha um **Conjunto de Relatórios**.

   Quando um conjunto de relatórios é selecionado, o LLM Optimizer carrega as **opções de URL da página Dimension** disponíveis para esse conjunto.

   ![Conjunto de relatórios selecionado e dimensões carregando](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Escolha uma **Dimension da URL da página** (lista de dimensões específicas do conjunto) e selecione **Salvar e Habilitar**.

   * A **URL da página Dimension** permanece desabilitada até que um conjunto de relatórios seja selecionado e as dimensões sejam carregadas.
   * **Salvar e Habilitar** está disponível somente após a seleção de uma dimensão de URL de página.

   ![Dimensão de URL da página e Salvar e Habilitar](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. Depois de salvar, a configuração deve mostrar o status **Conectado**. Você pode retornar ao painel de Tráfegos de referência com **Ir para o Painel de Tráfegos de referência**. No **Tráfego de referência** da guia **Impacto nos Negócios**, o status deve aparecer como **Conectado ao Adobe Analytics**.

   ![Conectado ao Adobe Analytics na configuração e Impacto nos Negócios](/help/dashboards/assets/aa-integration-07-connected.png)

### Depois que você se conectar {#after-connect}

* O LLM Optimizer preenche as **últimas quatro semanas completas do calendário** e a **semana atual do calendário até a data**.
* Após o preenchimento retroativo, os dados são atualizados **diariamente** com um pull do **dia anterior completo**.

>[!NOTE]
>
>O preenchimento retroativo pode levar algumas horas para ser concluído.

## Como funciona {#how-it-works}

### Configuração

Durante a configuração, você define qual conjunto de relatórios e dimensão de página a LLM Optimizer usa para a assimilação do Adobe Analytics. A dimensão de página pode ser o mapeamento `variables/page` padrão ou um `eVar` personalizado, dependendo do conjunto de relatórios.

### Como o tráfego LLM é identificado

O tráfego originado por LLM é identificado com o uso do [Tipo de referenciador — Ferramentas de IA de conversação](https://experienceleague.adobe.com/pt-br/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools) do Adobe Analytics.

### Dados assimilados {#data-ingested}

Os seguintes dados são assimilados pela LLM Optimizer:

**Dimensões**

* Domínio referenciador
* Tipo de referenciador
* País
* Tipo de dispositivo
* Dimensão da página selecionada

**Métricas**

* Visualizações da página
* Visitas
* Visitantes
* Entradas
* Saídas
* Rejeições
* Visitas em única página
* Tempo gasto
* Carrinhos
* Adições ao carrinho
* Remoções do carrinho
* Visualizações do carrinho
* Check-outs
* Pedidos
* Receita
* Unidades

### Como a LLM Optimizer usa esses dados

Esse conjunto de dados capacita os insights do LLM Optimizer para:

* Desempenho do tráfego LLM em nível de página.
* Desempenho do referenciador em fontes LLM.
* Tendências regionais e no nível do dispositivo.
* Resultados de comércio downstream.

## Perguntas frequentes {#faq}

P: A integração do Adobe Analytics está disponível durante a avaliação?

Não. A integração está disponível somente para clientes pagos do LLM Optimizer.

P: Quais dados são coletados ou armazenados?

Consulte o capítulo [Dados assimilados](#data-ingested) acima. O LLM Optimizer funciona com métricas agregadas das APIs do Adobe Analytics autorizadas pela sua organização, não com os dados brutos no nível de ocorrência.

P: Como os dados são assimilados?

Sua organização autoriza a LLM Optimizer a consultar APIs da Adobe Analytics. O tráfego de referência alinhado às fontes do LLM é consumido por meio dessas APIs.

P: Com que frequência os dados são atualizados?

Os dados são atualizados **diariamente** (dia anterior completo após a conclusão do preenchimento retroativo).

P: Os dados brutos a nível de ocorrência são armazenados no LLM Optimizer?

Não. Somente métricas **agregadas** são usadas para entender padrões e tendências de tráfego.

P: URLs completos, sequências de consulta ou conteúdo de página são armazenados?

URLs completos usados para a dimensão de página selecionada podem ser assimilados; cadeias de caracteres de consulta e conteúdo de página não são assimilados para essa integração.

P: Os identificadores de usuários (ECID, endereço IP, IDs de cookies) são armazenados?

Não.

P: Por quanto tempo os dados são retidos?

Lembre-se de que as políticas de retenção podem evoluir. Atualmente, os dados são armazenados indefinidamente.

P: Os dados são criptografados em trânsito e em repouso?

Atualmente, os dados são criptografados em trânsito e não em repouso. Isso pode mudar em atualizações futuras.

P: Os dados históricos são preenchidos retroativamente?

Sim. Após uma configuração bem-sucedida, as últimas quatro semanas completas do calendário e a semana atual do calendário são preenchidas retroativamente. Consulte também [Depois de conectar](#after-connect).
