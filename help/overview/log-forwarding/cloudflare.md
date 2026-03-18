---
title: Encaminhamento de logs - Cloud Flare
description: Saiba como encaminhar logs de CDN do Cloudflare para o bucket do S3 da Adobe para coleta de dados de tráfego direto no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Encaminhamento de logs: Cloud Flare {#log-forwarding-cloudflare}

Esta página detalha como encaminhar logs CDN do Cloudflare para o bucket S3 do Adobe para coleta de dados de tráfego direto. Você usará a página de configuração do LLM Optimizer CDN para integrar-se ao LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no console do painel do Cloud.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vá para o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Introdução**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Cloudflare (BYOCDN)**.

   ![Selecionar Cloudflare](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. Clique em **Integrar**.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: Criar um trabalho Logpush no Cloud Flare {#step-2}

No [painel Cloudflare](https://dash.cloudflare.com/login), siga estas etapas:

1. Vá para a página **Logpush** no nível **Domínio (zona)**.
1. Selecione **Criar um trabalho de Logpush**.
1. Em **Selecionar um destino**, escolha **Amazon S3**.
1. Especifique as seguintes informações de destino:

   - **Compartimento** — o nome do compartimento S3. Copie o valor da página Configuração do LLM Optimizer CDN.

     ![Nome do bloco](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **Caminho** — o local do bucket no contêiner de armazenamento. Copie o valor da página Configuração do LLM Optimizer CDN.

     ![Caminho da nuvem](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **Organizar logs em subpastas diárias** (recomendado).

     ![Subpastas diárias](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **Região do bucket** — copie o valor da página Configuração de CDN do LLM Optimizer.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - Se a criptografia do lado do servidor não for necessária, deixe desmarcada.

   Após concluir as etapas acima, selecione **Continuar**.

1. Para comprovar a propriedade, o Cloud Flare enviará um arquivo para o destino designado. Para localizar o token, clique no botão **Abrir** na guia **Visão geral** do arquivo de desafio de propriedade. Copie o token de propriedade da página de configuração do LLM Optimizer CDN e cole-o no painel do Cloud Flare para verificar seu acesso ao bucket. Insira o Token de Propriedade e selecione **Continuar**.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. Selecione o conjunto de dados **Solicitações HTTP** para enviar para o serviço de armazenamento.

1. Configure seu trabalho Logpush:

   - Insira o **Nome do trabalho**.

   - Em **Enviar os seguintes campos**, consulte os valores na página de configuração do LLM Optimizer.

     ![Campos de push de log](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **Formato do log**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. Em **Opções Avançadas**:

   - Escolha o formato dos campos de carimbo de data/hora em seus logs: `RFC3339`.

     ![Formato de carimbo de data/hora](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - Para taxas de amostragem, selecione **Todos os logs**.

     ![Taxa de amostragem](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Selecione **Enviar** depois de concluir a configuração do trabalho Logpush.
