---
title: Encaminhamento de logs - Imperva
description: Saiba como encaminhar logs de CDN de Imperva para o bucket do S3 da Adobe para coleção de dados de tráfego direto no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---


# Encaminhamento de logs: Imperva {#log-forwarding-imperva}

Este guia explica como encaminhar logs de CDN de Imperva para o bucket S3 do Adobe para coleta de dados de tráfego agênticos. Você usará a página de configuração do LLM Optimizer CDN para integrar-se ao LLM Optimizer. Depois que o processo de integração estiver concluído, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs a partir do Imperva web console.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Ir para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Clique em **Introdução**.
1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecione **Imperva (BYOCDN)**.

   ![Selecionar Imperva](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Clique em **Integrar**.

## Etapa 2: configurar o encaminhamento de logs no Imperva {#step-2}

No [console Imperva](https://my.imperva.com):

>[!NOTE]
>
>Os logs devem ser enviados diariamente.

1. Faça login em sua conta Imperva em [https://my.imperva.com](https://my.imperva.com).

2. Na barra lateral, vá para **Logs** > **Configuração de Log** (ou **Integração de Log**).

3. Selecione **Amazon S3 ARN** como o tipo de conexão (destino de log).

4. Insira o seguinte:

   | Texto | Descrição | Nota |
   |---|---|---|
   | **Nome da conexão** | Um nome descritivo para a conexão (por exemplo, registros de Produção S3). É possível renomear o padrão. | |
   | **Caminho** | O local da pasta onde os arquivos de log serão armazenados. Use o formato `<Amazon S3 bucket name>/<log folder>`. Por exemplo: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name` é o **Nome do bloco** da página de configuração do LLM Optimizer. ![Nome do bucket](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) A pasta de log é **Caminho** da página de configuração do LLM Optimizer. ![Caminho](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Clique em **Testar conexão**. Imperva executa um teste completo em que um arquivo de teste (sem dados reais) é enviado para a pasta designada e, em seguida, removido quando a transferência é concluída.

   - **Disponível** — os detalhes de armazenamento são válidos; você pode configurar logs para usar essa conexão.
   - **Indefinido** — os detalhes necessários estão ausentes ou o teste falhou.

6. Clique em **Salvar** para armazenar a configuração.

7. Configure as opções de log (tipos de log, nível de log, formato, compactação) e **Níveis de Log**. Você pode obter os valores da página de configuração do LLM Optimizer.

   | Texto | Nota |
   |---|---|
   | Modo de integração de log | ![Modo de integração de log](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Método de entrega | ![Método de entrega](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Tipos de log | ![Tipos de log](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Nível de log | ![Nível de log](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Formato | ![Formato](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Compactar logs | ![Compactar logs](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
