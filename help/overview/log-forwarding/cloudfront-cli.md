---
title: Encaminhamento de logs – CloudFront (AWS CLI)
description: Encaminhe os logs de CDN do CloudFront para o bloco do Adobe S3 usando a CLI do AWS para configuração e operações de entrega.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:42:44.992Z'
TQID: 'https://experienceleague.adobe.com/NoVv3qv1RbtqAWGMPYC1Rz4wO-5Au1yL2e8tRKd9Hao'
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
source-git-commit: a68e70baa717d392a03249cada83337d3f51341c
workflow-type: tm+mt
source-wordcount: 379
ht-degree: 100%

---


# Encaminhamento de log: CloudFront (AWS CLI) {#log-forwarding-cloudfront-cli}

Esta página detalha como encaminhar logs de CDN do CloudFront para o bloco S3 do Adobe para a coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de log usando a [Interface de linha de comando do AWS](https://aws.amazon.com/pt/cli/) na [Etapa 2](#step-2-cli).

>[!NOTE]
>
> Este guia explica como configurar o encaminhamento de logs usando a [Interface de linha de comando do AWS](https://aws.amazon.com/pt/cli/). Se você quiser configurar o encaminhamento de logs usando a **Interface de usuário do CloudFront**, consulte [Encaminhamento de logs: CloudFront](/help/overview/log-forwarding/cloudfront.md).

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

<!--  ![AWS Account ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)-->

1. Selecione **CloudFront (BYOCDN)**.

   ![Selecione CloudFront](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Clique em **Integrar**.

<!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: configurar o encaminhamento de log da CDN com o AWS CLI {#step-2-cli}

Configure o encaminhamento de logs da CDN com o AWS CLI da seguinte forma:

### Configurar credenciais do AWS CLI

Configurar credencial MAC do AWS CLI. Abra ~/.aws/credentials e insira os valores das variáveis abaixo:

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### Testar a conexão

Execute o comando abaixo para testar a conexão:

```bash
aws sts get-caller-identity --profile LLMO
```

Exemplo de saída bem-sucedida:

```bash
aws sts get-caller-identity --profile LLMO
{
    "UserId": "AxxxxxxxxxxxP:user",
    "Account": "012345678912",
    "Arn": "arn:aws:sts::012345678912:assumed-role/klam-master-role-BatlY3dnPVinQLC/user"
}
```

### Inicializar variáveis

Substitua `REPLACEME123@AdobeOrg` pela ID da organização no Adobe IMS e execute o comando abaixo. A ID de saída deste comando será chamada de `TRANSFORM_IMS_ID`.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

Insira os valores para `CUSTOMER`, `CDN_ID`, `ACCT1` e `TRANSFORM_IMS_ID` seguindo as diretrizes abaixo e execute os comandos do terminal.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>  ## Replace TRANSFORM_IMS_ID with the output of the command above
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### Criar a origem da entrega

No mesmo terminal em que a etapa 3 foi executada, execute o comando abaixo:

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>Se você receber o seguinte erro, procure a origem de entrega existente: *ocorreu um erro (ConflictException) ao chamar a operação PutDeliverySource: este ResourceId já foi usado em outra Origem de entrega nesta conta.*
>
>Para pesquisar a origem de entrega existente, execute este comando:
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>No próximo comando, use o nome da origem de entrega obtido nos resultados do comando acima.

### Criar a configuração de entrega

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

&lt;!--Alinhe `--record-fields` e `--s3-delivery-configuration` com a lista de campos e o sufixo de caminho mostrados na página de configuração da CDN do LLM Optimizer se a documentação ou os valores do produto forem alterados.-->
