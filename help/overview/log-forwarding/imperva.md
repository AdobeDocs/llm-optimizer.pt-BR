---
title: 'Encaminhamento de logs: Imperva'
description: Saiba como encaminhar logs da CDN da Imperva para o bloco do S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:52:22.260Z'
TQID: 'https://experienceleague.adobe.com/y2ticpRCNZjPYJ6wHg-V3QWxBnGF--mQfqGBYjVjKXY'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 100%

---


# Encaminhamento de logs: Imperva {#log-forwarding-imperva}

Este guia explica como encaminhar logs da CDN da Imperva para o bloco S3 do Adobe para coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Depois que o processo de integração estiver concluído, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs a partir do console da web da Imperva.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vá para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Clique em **Começar**.
1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecione **Imperva (BYOCDN)**.

   ![Selecionar Imperva](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Clique em **Integrar**.

## Etapa 2: configurar o encaminhamento de logs na Imperva {#step-2}

No [console da Imperva](https://my.imperva.com):

>[!NOTE]
>
>Os logs devem ser enviados diariamente.

1. Faça logon na sua conta da Imperva em [https://my.imperva.com](https://my.imperva.com).

2. Na barra lateral, vá para **Logs** > **Configuração de log** (ou **Integração de log**).

3. Selecione **Amazon S3 ARN** como o tipo de conexão (destino de log).

4. Insira o seguinte:

   | Texto | Descrição | Nota |
   |---|---|---|
   | **Nome da conexão** | Um nome descritivo para a conexão (por exemplo, registros de produção S3). É possível renomear o padrão. | |
   | **Caminho** | Localização da pasta onde os arquivos de log são armazenados. Use o formato `<Amazon S3 bucket name>/<log folder>`. Por exemplo: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name` é o **Nome do bloco** da página de configuração do LLM Optimizer. ![Nome do bloco](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) A pasta de logs é o **Caminho** da página de configuração do LLM Optimizer. ![Caminho](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Clique em **Testar conexão**. A Imperva executa um teste completo no qual um arquivo de teste (sem dados reais) é enviado para a pasta designada e, em seguida, removido quando a transferência é concluída.

   - **Disponível**: os detalhes de armazenamento são válidos; você pode configurar os logs para usar esta conexão.
   - **Indefinido**: os detalhes necessários estão faltando ou o teste falhou.

6. Clique em **Salvar** para armazenar a configuração.

7. Configure as opções de log (tipos de log, nível de log, formato, compactação) e **Níveis de log**. Você pode obter os valores na página de configuração do LLM Optimizer.

   | Texto | Nota |
   |---|---|
   | Modo de integração de logs | ![Modo de integração de logs](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Método de entrega | ![Método de entrega](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Tipos de log | ![Tipos de log](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Nível de log | ![Nível de log](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Formato | ![Formato](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Compactar logs | ![Compactar logs](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
