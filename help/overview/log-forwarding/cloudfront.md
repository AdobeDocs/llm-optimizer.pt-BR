---
title: Encaminhamento de logs - CloudFront
description: Saiba como encaminhar logs de CDN do CloudFront para o bucket do S3 da Adobe para a coleta de dados de tráfego direto no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Encaminhamento de log: CloudFront {#log-forwarding-cloudfront}

Esta página explica como encaminhar logs de CDN do CloudFront para o bucket S3 do Adobe para a coleta de dados de tráfego direto. Você usará a página de configuração do LLM Optimizer CDN para integrar-se ao LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no console de painel do CloudFront.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vá para o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Introdução**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Digite sua ID da **Conta da AWS**.

   ![ID da Conta da AWS](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. Selecione **CloudFront (BYOCDN)**.

   ![Selecionar CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Clique em **Integrar**.

   ![Botão Integrar](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Etapa 2: ativar o registro padrão (console CloudFront) {#step-2}

Para habilitar o log padrão, no [console de Gerenciamento do AWS](https://aws.amazon.com/console/):

1. Acesse o [console CloudFront](https://console.aws.amazon.com/cloudfront/v4/home) e [atualize uma distribuição existente](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure).

1. Abra a guia **Log**.

1. Escolha **Adicionar** e selecione o serviço para receber logs, neste caso **Amazon S3**.

1. Para **Destino**, selecione ou crie o recurso. Insira o **nome do bucket**, você pode copiar o valor da página de configuração do LLM Optimizer CDN.

   ![Nome do bucket do CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. Definir **configurações adicionais**:

   - **Seleção de campo** — escolha os campos do arquivo de log. Consulte os campos obrigatórios na página de configuração do LLM Optimizer CDN.

     ![Seleção de campo CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **Particionamento** — copie o **sufixo de caminho** da página de configuração do LLM Optimizer.

     ![Particionamento CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **Formato de saída** — o formato deve ser JSON.

     ![Formato de saída CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. Complete as etapas para atualizar ou criar a distribuição.

1. Na página **Logs**, confirme se **Enabled** aparece ao lado da distribuição.

## Habilitar log padrão para entrega entre contas {#cross-account}

A **conta de origem** (com a distribuição CloudFront) envia logs de acesso para a **conta de destino** (o compartimento S3 mostrado na página de configuração do LLM Optimizer CDN). Ambas as contas devem ter as permissões certas.

Por exemplo: a conta de origem `111111111111` envia logs para um bucket S3 na conta de destino `222222222222`. Você pode usar a [Interface de Linha de Comando do AWS](https://aws.amazon.com/cli/).

>[!NOTE]
>
>Nos comandos abaixo, substitua o valor ARN de destino de entrega (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) pelo valor de **ARN de destino de entrega** da página de configuração do LLM Optimizer.

![ARN de destino de entrega](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### Configurar a conta de origem {#source-account}

Em seguida, é necessário configurar a conta de origem:

1. **Criar uma fonte de entrega** - substituir o nome e o ARN de distribuição:

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **Criar a entrega** - vincular origem ao destino; use o ARN de destino da etapa &quot;Configurar a conta de destino&quot;:

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **Verificar:**

   - Na conta de **origem**: console CloudFront > sua distribuição > guia **Logging**. Em **Type**, você deve ver a entrega de logs entre contas do S3.
   - Na conta **destination**: console S3 > bucket. Você deve ver o prefixo (por exemplo, `MyLogPrefix`) e os logs nessa pasta.
