---
title: Encaminhamento de logs - CloudFront
description: Saiba como encaminhar logs da CDN do CloudFront para o bloco S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:43:07.178Z'
TQID: 'https://experienceleague.adobe.com/TXnY-eK1SUuKrlVoGWd2hZO5bjUqEspvyFmcyOuei3Q'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 100%

---


# Encaminhamento de logs: CloudFront {#log-forwarding-cloudfront}

Esta página explica como encaminhar os logs da CDN do CloudFront para o bloco S3 da Adobe para coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Após a conclusão do processo de integração, siga os passos indicados nesta página para configurar o encaminhamento de logs no console do painel do CloudFront.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Acesse o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Começar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Insira a ID da sua **conta AWS**.

   ![ID da conta do AWS](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. Selecione **CloudFront (BYOCDN)**.

   ![Selecione CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Clique em **Integrar**.

   ![Botão Integrar](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Etapa 2: habilitar registro padrão (console do CloudFront) {#step-2}

Para habilitar o registro padrão, no [Console de gerenciamento do AWS](https://aws.amazon.com/pt/console/):

1. Acesse o [console do CloudFront](https://console.aws.amazon.com/cloudfront/v4/home) e [atualize uma distribuição existente](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure).

1. Abra a guia **Registro**.

1. Selecione **Adicionar** e, em seguida, escolha o serviço no qual deseja receber os logs, neste caso, **Amazon S3**.

1. Para **Destino**, selecione ou crie o recurso. Insira o **nome do bloco**; você pode copiar o valor da página de configuração da CDN do LLM Optimizer.

   ![Nome do bloco do CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. Definir **Configurações adicionais**:

   - **Seleção de campos** — escolha os campos do arquivo de log. Consulte os campos obrigatórios na página de configuração da CDN do LLM Optimizer.

     ![Seleção de campos do CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **Particionamento** — copie o **sufixo de caminho** da página de configuração do LLM Optimizer.

     ![Particionamento do CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **Formato de saída** — o formato deve ser JSON.

     ![Formato de saída do CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. Conclua as etapas para atualizar ou criar a distribuição.

1. Na página **Logs**, confirme se **Habilitado** aparece ao lado de distribuição.

## Habilite o registro padrão para entrega entre contas {#cross-account}

A **conta de origem** (com a distribuição do CloudFront) envia logs de acesso para a **conta de destino** (o bloco S3 indicado na página de configuração da CDN do LLM Optimizer). Ambas as contas devem ter as permissões corretas.

Por exemplo: a conta de origem `111111111111` envia logs para um bloco S3 na conta de destino`222222222222`. Você pode usar a [Interface de linha de comando do AWS](https://aws.amazon.com/pt/cli/).

>[!NOTE]
>
>Nos comandos abaixo, substitua o valor do ARN de destino de entrega (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) pelo valor do **ARN de destino de entrega** da página de configuração do LLM Optimizer.

![ARN de destino de entrega](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### Configure a conta de origem {#source-account}

Em seguida, você precisa configurar a conta de origem:

1. **Criar uma origem de entrega** - substitua o nome e o ARN de distribuição:

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **Criar a entrega** - vincule a origem ao destino; use o ARN de destino da etapa &quot;Configurar a conta de destino&quot;:

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **Verificar:**

   - Na conta de **origem**: console do CloudFront > sua distribuição > guia **Registro**. Em **Tipo**, você deverá ver a entrega de logs entre contas do S3.
   - Na conta de **destino**: console S3 > bloco. Você deve ver o prefixo (por exemplo, `MyLogPrefix`) e os logs nessa pasta.
