---
title: Encaminhamento de logs - Akamai
description: Saiba como encaminhar logs da CDN do Akamai para o bloco do S3 da Adobe para a coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:35:22.816Z'
TQID: 'https://experienceleague.adobe.com/cO-qqOveWFee1-QnVSlzmO-n383sptHl59Ni2qQcvAU'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 100%

---


# Encaminhamento de logs: Akamai {#log-forwarding-akamai}

Esta página explica como encaminhar logs da CDN do Akamai para o bloco do S3 da Adobe para coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no Painel de controle do Akamai.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Acesse o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Começar**.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Akamai (BYOCDN)**.

   ![Selecione o Akamai](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. Clique em **Integrar**.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: crie um fluxo no Akamai {#step-2}

No painel de controle do Akamai [https://control.akamai.com/](https://control.akamai.com/), siga as etapas da documentação oficial do Akamai para [criar um fluxo](https://techdocs.akamai.com/datastream2/docs/create-stream).

## Etapa 3: escolha parâmetros de dados {#step-3}

Depois de criar o fluxo, no painel de controle do Akamai, clique em Avançar para continuar na guia **Conjuntos de dados**. Siga as etapas da documentação oficial do Akamai para escolher os [parâmetros de dados](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters). Os seguintes campos da configuração do LLM Optimizer serão necessários:

![Campos de configuração do LLMO](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

O mapeamento deve ser o seguinte:

* **Informações de log**
reqTimeSec -> Tempo de solicitação
* **Dados geográficos**
país -> País/Região
* **Dados de troca de mensagens**
reqHost -> Host de solicitação
reqPath -> Caminho da solicitação
queryStr -> String de consulta
reqMethod -> Método de solicitação
ua -> User-Agent
statusCode -> Código de status HTTP
rspContentType -> Tipo de conteúdo da resposta
* **Dados do cabeçalho da solicitação**
referer -> Referenciador
* **Dados de desempenho da rede**
timeToFirstByte -> Tempo até o primeiro byte

Os campos do conjunto de dados da Akamai (incluindo IDs) são os seguintes:

1100, # reqTimeSec -> Tempo de solicitação
2012, # país -> País/Região
1011, # reqHost -> Host de solicitação
1013, # reqPath -> Request path
2009, # queryStr -> String de consulta
1012, # reqMethod -> Método de solicitação
1017, # ua -> Agente do usuário
1008, # statusCode -> Código de status HTTP
1032, # referer -> Referenciador
1016, # rspContentType -> Tipo de conteúdo da resposta
2025  # timeToFirstByte -> Tempo até o primeiro byte

## Etapa 4: configurar destino {#step-4}

Após criar os fluxos de dados e escolher os parâmetros, você precisa configurar o destino. Para configurar o destino, siga estas etapas:

1. Em **Destino**, selecione **S3**.
2. Em **Nome**, insira uma descrição legível para o destino.
3. Em **Bloco**, copie o **Nome do bloco** da página de configuração do LLM Optimizer.

   ![Nome do bloco](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. Em **Caminho da pasta**, copie o **Caminho** da página de configuração do LLM Optimizer.

   ![Configuração de caminho](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. Em **Região**, copie a **Região** da página de configuração do LLM Optimizer.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. Em **ID da chave de acesso** e **Chave de acesso secreta**, copie ambos os valores da página de configuração do LLM Optimizer.

   ![Chaves de acesso](/help/overview/assets/log-forwarding/common/access-keys.png)

7. Clique em **Validar e Salvar** para validar a conexão com o destino e salvar os detalhes fornecidos. Como parte desse processo de validação, o sistema usa o identificador da chave de acesso fornecido e a chave de acesso secreta para criar um arquivo de verificação em sua pasta S3, com um carimbo de data e hora no nome do arquivo no formato `Akamai_access_verification_[TimeStamp].txt`. Você só poderá visualizar este arquivo se o processo de validação for bem-sucedido e você tiver acesso ao bloco e à pasta do Amazon S3 para os quais está tentando enviar os logs.

8. No menu **Opções de entrega**, edite o campo **Nome do arquivo** da seguinte forma:

   a. Altere o **prefixo**. Copie o valor da página de configuração do LLM Optimizer em **Prefixo do arquivo de log**:

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b. Altere o **sufixo**. Copie o valor da página de configuração do LLM Optimizer em **Sufixo do arquivo de log**.

9. Altere a **Frequência de push**. Copie o valor da página de configuração do LLM Optimizer em **Intervalo de log**.

   ![Intervalo de log](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. Clique em **Próximo** para concluir o processo.

Antes da validação final, a configuração deve ser semelhante a este exemplo:

![Validação de configuração](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
