---
title: Encaminhamento de logs – Cloudflare
description: Saiba como encaminhar logs da CDN do Cloudflare para o bloco S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:41:23.688Z'
TQID: 'https://experienceleague.adobe.com/AfhcMa7tZ3L-4qCbNKiblInALmHaKxWLtL-O-Hkvc-U'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 100%

---


# Encaminhamento de logs: Cloudflare {#log-forwarding-cloudflare}

Esta página detalha como encaminhar logs da CDN do Cloudflare para o bloco S3 da Adobe para coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no console do painel do Cloudflare.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Acesse o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Começar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Cloudflare (BYOCDN)**.

   ![Selecione Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. Clique em **Integrar**.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: criar um trabalho de Logpush no Cloudflare {#step-2}

No [painel do Cloudflare](https://dash.cloudflare.com/login), siga estas etapas:

1. Acesse a página **Logpush** no nível de **Domínio (zona)**.
1. Selecione **Criar um trabalho de Logpush**.
1. Em **Selecionar um destino**, escolha **Amazon S3**.
1. Insira as seguintes informações de destino:

   - **Bloco** — o nome do bloco do S3. Copie o valor da página de configuração da CDN do LLM Optimizer.

     ![Nome do bloco](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **Caminho** — o local do bloco no contêiner de armazenamento. Copie o valor da página de configuração da CDN do LLM Optimizer.

     ![Caminho do Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **Organizar logs em subpastas diárias** (recomendado).

     ![Subpastas diárias](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **Região do bloco** — copie o valor da página de configuração da CDN do LLM Optimizer.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - Se a criptografia do lado do servidor não for necessária, deixe desmarcada.

   Após concluir as etapas acima, selecione **Continuar**.

1. Para comprovar a propriedade, o Cloudflare enviará um arquivo para o destino indicado. Para encontrar o token, clique no botão **Abrir** na guia **Visão geral** do arquivo de desafio de propriedade. Copie o token de propriedade da página de configuração da CDN do LLM Optimizer e cole-o no painel do Cloudflare para verificar seu acesso ao bloco. Insira o Token de propriedade e selecione **Continuar**.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. Selecione o conjunto de dados **Solicitações HTTP** para enviar ao serviço de armazenamento.

1. Configure o trabalho de Logpush:

   - Insira **Nome do trabalho**.

   - Em **Enviar os seguintes campos**, consulte os valores na página de configuração do LLM Optimizer.

     ![Campos de Logpush](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **Formato de log**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. Em **Opções avançadas**:

   - Escolha o formato dos campos de carimbo de data e hora em seus registros: `RFC3339`.

     ![Formato de carimbo de data e hora](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - Para taxas de amostragem, selecione **Todos os logs**.

     ![Taxa de amostragem](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Selecione **Enviar** assim que terminar de configurar o trabalho de Logpush.
