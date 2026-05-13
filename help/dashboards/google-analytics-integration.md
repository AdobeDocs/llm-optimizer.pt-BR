---
title: Integração do Google Analytics
description: Saiba como conectar o Google Analytics 4 com o LLM Optimizer para medir a descoberta orientada por IA, o envolvimento do site e os resultados comerciais no painel do Tráfego de referência.
feature: Referral Traffic
source-git-commit: abf88fc3e141e12d6b5c826e35d4590ae6407c9b
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---


# Integração do Google Analytics

A integração do Google Analytics 4 (GA4) conecta o LLM Optimizer aos dados GA4 de sua organização para que você possa medir como a descoberta orientada por IA em plataformas como ChatGPT, Gemini, Copilot, Claude e Perplexity se traduz em envolvimento real do site e resultados de negócios. Após conectar uma propriedade do GA4, a LLM Optimizer extrai as métricas de tráfego de referência, envolvimento e conversão que o GA4 atribui a essas fontes e as exibe no painel **Tráfego de referência** na guia **Impacto nos negócios**.

## Disponibilidade {#availability}

>[!IMPORTANT]
>
>A integração do GA4 está incluída na oferta paga do LLM Optimizer. Os clientes que usam a avaliação gratuita não poderão conectar o GA4 até que atualizem para uma oferta paga.

## Antes de começar {#before-you-begin}

Para concluir a conexão necessária:

* Uma conta do Google com pelo menos **Acesso de visualizador** na propriedade do GA4 que você deseja conectar. O acesso no nível da propriedade é gerenciado no Google Analytics em **Admin > Gerenciamento de Acesso à Propriedade**.
* Permissão para gerenciar a configuração no LLM Optimizer (caso contrário, o botão Conectar estará visível, mas desativado).
* Um navegador que permite pop-ups da origem do LLM Optimizer — a etapa de logon do Google é aberta em uma nova guia.

Você precisa **não** criar um projeto do Google Cloud, gerar uma conta de serviço, carregar uma chave JSON ou inserir uma ID de propriedade. A LLM Optimizer intermedia a conexão por meio da tela de consentimento OAuth padrão da Google.

## Conecte o GA4 ao painel do Tráfego de referência {#connect}

O fluxo de conexão começa no painel [Tráfego de referência](/help/dashboards/referral-traffic.md) da seguinte maneira:

1. Abra o **Tráfego de referência** no LLM Optimizer.

1. Abra a guia **Impacto nos negócios**.

   ![painel do Tráfego de referência, guia Impacto nos Negócios](/help/dashboards/assets/ga4-integration-01-business-impact-tab.png)

1. Selecione **Conectar ao Analytics**. O LLM Optimizer direciona você para **Configuração do cliente > Analytics**. No seletor de Provedor do Analytics, selecione **Google Analytics 4**.

   ![Configuração do cliente, guia Analytics com GA4 selecionado](/help/dashboards/assets/ga4-integration-02-analytics-ga4-picker.png)

1. Selecione **Conectar**. Uma nova guia do navegador é aberta na tela de logon do Google.

   ![Entrada do Google para conexão GA4](/help/dashboards/assets/ga4-integration-03-google-sign-in.png)

1. Faça logon com a conta da Google que tem acesso à propriedade do GA4 que você deseja conectar. Aprove a permissão `See and download your Google Analytics data` (escopo `analytics.readonly`) quando a Google solicitar.

1. O Google retorna ao LLM Optimizer, que lista as propriedades do GA4 que sua conta pode acessar. Selecione a propriedade a ser conectada e enviada.

1. Retorne à guia LLM Optimizer. A guia Analytics detecta automaticamente a conexão concluída e o cartão GA4 mostra o status **Conectado**.

### Depois que você se conectar {#after-connect}

Depois que o GA4 é conectado ao LLM Optimizer, ocorre o seguinte:

* O LLM Optimizer preenche as **últimas quatro semanas completas do calendário** e a **semana atual do calendário até a data**.
* Após o preenchimento retroativo, os dados são atualizados **diariamente** com um pull do **dia anterior completo**.

>[!NOTE]
>
>O preenchimento retroativo pode levar algumas horas para ser concluído. O painel Impacto nos negócios começa a se preencher progressivamente à medida que os dados chegam; nenhuma ação é necessária enquanto o preenchimento retroativo é executado.

Se você se reconectar (por exemplo, para alternar a conta do Google ou a propriedade do GA4), somente a semana atual do calendário será preenchida novamente, as semanas anteriores que já estiverem carregadas serão preservadas.

## Como funciona {#how-it-works}

### Modelo de conexão

A integração usa o fluxo delegado pelo usuário OAuth 2.0 padrão do Google. O LLM Optimizer armazena um token de atualização com escopo para a propriedade do GA4 selecionada e esse token permite que o LLM Optimizer chame a API de dados do GA4 em seu nome (com acesso somente leitura) até que você a revogue da sua conta do Google.

### Como o tráfego LLM é identificado

A LLM Optimizer solicita o GA4 somente para as sessões que o próprio GA4 atribui a uma plataforma LLM. Hoje, essas são sessões cujo `sessionSourceMedium` corresponde a um dos `chatgpt`, `gemini.google.com`, `copilot.microsoft.com`, `claude` ou `perplexity`. A lista de fontes de LLM compatíveis é mantida pela Adobe e pode se expandir ao longo do tempo.

### Dados assimilados {#data-ingested}

Cada baixa diária recupera um relatório agregado contendo o seguinte:

**Dimensões**

| Dimensão GA4 | O que ele representa |
| --- | --- |
| `date` | O dia em que a sessão ocorreu. |
| `landingPage` | A primeira página que o visitante viu em seu site. |
| `countryId` | O país do visitante, conforme determinado pela localização geográfica do IP do GA4. |
| `deviceCategory` | Móvel/desktop/tablet. |
| `sessionSourceMedium` | A fonte/mídia LLM atribuída pelo GA4. |

**Métricas**

| Métrica GA4 | O que ele representa |
| --- | --- |
| `sessions` | Número de sessões no bucket. |
| `screenPageViews` | Exibições de página no bucket. |
| `bounceRate` | Fração de sessões que foi rejeitada. |
| `totalPurchasers` | Compradores distintos (se o comércio eletrônico estiver configurado no GA4). |
| `transactions` | Contagem de transações (se o comércio eletrônico estiver configurado). |
| `purchaseRevenue` | Receita de compra (US$). |
| `totalRevenue` | Receita total (US$). |

### Como a LLM Optimizer usa esses dados

O LLM Optimizer usa esses dados para preencher o desempenho em nível de página do painel de impacto nos negócios, detalhamentos de origem, divisões de país e dispositivo e tendências de tempo. Nenhum dado é usado para treinar modelos ou compartilhado fora do locatário.

### O que não é assimilado

Nenhum identificador de usuário (ID de cliente do Google, endereço IP, ID de dispositivo), nenhuma linha em nível de sessão, nenhuma linha em nível de evento, nenhuma dimensão ou métrica personalizada além das listadas acima e nenhuma definição de público-alvo ou segmento do GA4.

## Perguntas frequentes {#faq}

P: A integração do GA4 está disponível durante a avaliação?

Não. A integração está disponível somente para clientes pagos do LLM Optimizer.

P: Preciso criar um projeto ou uma conta de serviço da Google Cloud?

Não. A conexão é um logon padrão do Google. O LLM Optimizer gerencia o cliente OAuth do Google no lado do Adobe; você só precisa de uma conta do Google com acesso de visualizador na propriedade do GA4.

P: Quais dados são coletados ou armazenados?

O LLM Optimizer funciona com métricas agregadas da API de dados do GA4 autorizada pela sua organização, não dados brutos no nível do evento.

P: Como os dados são assimilados?

Sua organização autoriza o LLM Optimizer a consultar a API de dados do GA4 para a propriedade selecionada. O tráfego de referência alinhado às fontes do LLM é consumido por meio dessa API.

P: Com que frequência os dados são atualizados?

Os dados são atualizados **diariamente** (dia anterior completo após a conclusão do preenchimento retroativo).

P: Os dados brutos a nível de evento são armazenados no LLM Optimizer?

Não. Somente métricas **agregadas** são usadas para entender padrões e tendências de tráfego.

P: URLs completos, sequências de consulta ou conteúdo de página são armazenados?

Os caminhos de página de aterrissagem são assimilados como parte do relatório padrão; as sequências de consulta e o conteúdo da página não são assimilados para essa integração.

P: Os identificadores de usuário (ID do cliente do Google, endereço IP, ID do dispositivo) são armazenados?

Não.

P: Por quanto tempo os dados são retidos?

Atualmente, os dados são armazenados indefinidamente.

P: Os dados são criptografados em trânsito e em repouso?

Atualmente, os dados são criptografados em trânsito, não em repouso. Isso pode mudar em atualizações futuras.

P: Os dados históricos são preenchidos retroativamente?

Sim. Após uma configuração bem-sucedida, as últimas quatro semanas completas do calendário e a semana atual do calendário são preenchidas retroativamente. Consulte também [Depois de conectar](#after-connect).

P: Posso desconectar ou revogar o acesso?

Sim — a qualquer momento. Você pode se reconectar a uma conta ou propriedade diferente do cartão GA4 no LLM Optimizer, ou revogar o acesso da LLM Optimizer totalmente da sua conta do Google em [https://myaccount.google.com/permissions](https://myaccount.google.com/permissions). A revogação do acesso interrompe novas extrações de dados; os dados agregados assimilados anteriormente permanecem no LLM Optimizer.

P: Minha propriedade do GA4 está conectada, mas o Impacto nos negócios está vazio — por quê?

O LLM Optimizer só extrai sessões que o próprio GA4 atribui a uma origem/meio de LLM compatível (hoje: ChatGPT, Gemini, Copilot, Claude, Perplexity). Se sua propriedade do GA4 ainda não tiver registrado sessões de referência de qualquer uma dessas fontes na janela de tempo mostrada, o painel estará vazio, mesmo que a conexão esteja íntegra.
