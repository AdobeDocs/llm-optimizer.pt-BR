---
title: Encaminhamento de logs - Akamai
description: Saiba como encaminhar logs de CDN do Akamai para o bucket do S3 da Adobe para a coleta de dados de tráfego direto no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# Encaminhamento de logs: Akamai {#log-forwarding-akamai}

Esta página explica como encaminhar logs de CDN do Akamai para o bucket S3 do Adobe para coleta de dados de tráfego direto. Você usará a página de configuração do LLM Optimizer CDN para integrar-se ao LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no Painel de controle do Akamai.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vá para o **Painel de configuração do cliente**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Introdução**.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Akamai (BYOCDN)**.

   ![Selecionar Akamai](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. Clique em **Integrar**.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: criar um fluxo no Akamai {#step-2}

No painel de controle do Akamai [https://control.akamai.com/](https://control.akamai.com/), siga as etapas da documentação oficial do Akamai para [criar um fluxo](https://techdocs.akamai.com/datastream2/docs/create-stream).

## Etapa 3: Escolher parâmetros de dados {#step-3}

Depois de criar o fluxo, no painel de controle do Akamai, clique em Avançar para continuar na guia **Conjuntos de dados**. Siga as etapas da documentação oficial do Akamai para escolher os [parâmetros de dados](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters). Os seguintes campos da configuração do LLM Optimizer serão necessários:

![campos de configuração do LLMO](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

O mapeamento deve ser o seguinte:

* **Informações de Log**
reqTimeSec -> Tempo de solicitação
* **Dados Geográficos**
país -> País/região
* **Dados de troca de mensagens**
reqHost -> Solicitar host
reqPath -> Caminho da solicitação
queryStr -> Sequência de consulta
reqMethod -> método de solicitação
ua -> User-Agent
statusCode -> Código de status HTTP
rspContentType -> Tipo de conteúdo de resposta
* **Solicitar dados de cabeçalho**
referenciador -> Referenciador
* **Dados de desempenho da rede**
timeToFirstByte -> Tempo até o primeiro byte

Os campos do conjunto de dados do Akamai (incluindo IDs) são os seguintes:

1100, # reqTimeSec -> Tempo de solicitação
2012, # país -> País/região
1011, # reqHost -> Solicitar host
1013, # reqPath -> Caminho da solicitação
2009, # queryStr -> Sequência de consulta
1012, # reqMethod -> Método de solicitação
1017, # ua -> Usuário-agente
1008, # statusCode -> Código de status HTTP
1032, # referenciador -> Referenciador
1016, # rspContentType -> Resposta Content-Type
2025 # timeToFirstByte -> Tempo até o primeiro byte

## Etapa 4: configurar destino {#step-4}

Após criar os fluxos de dados e escolher os parâmetros, é necessário configurar o destino. Para configurar o destino, siga estas etapas:

1. Em **Destino**, selecione **S3**.
2. Em **Name**, insira uma descrição legível para o destino.
3. Em **Bucket**, copie o **Nome do Bucket** da página de configuração do LLM Optimizer.

   ![Nome do bloco](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. Em **Caminho da pasta**, copie o **Caminho** da página de configuração do LLM Optimizer.

   ![Configuração de caminho](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. Em **Region**, copie a **Region** da página de configuração do LLM Optimizer.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. Em **ID da chave de acesso** e **Chave de acesso secreta**, copie ambos os valores da página de configuração do LLM Optimizer.

   ![Chaves de acesso](/help/overview/assets/log-forwarding/common/access-keys.png)

7. Clique em **Validar e salvar** para validar a conexão com o destino e salvar os detalhes fornecidos. Como parte desse processo de validação, o sistema usa o identificador de chave de acesso fornecido e a chave de acesso secreta para criar um arquivo de verificação na pasta S3, com um carimbo de data e hora no nome do arquivo no formato `Akamai_access_verification_[TimeStamp].txt`. Você só poderá ver esse arquivo se o processo de validação for bem-sucedido e você tiver acesso ao bucket e à pasta do Amazon S3 para os quais está tentando enviar logs.

8. No menu **Opções de entrega**, edite o campo **Nome do arquivo** da seguinte maneira:

   a) Alterar o **prefixo**. Copie o valor da página de configuração do LLM Optimizer em **Prefixo do arquivo de log**:

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b) Altere o **sufixo**. Copie o valor da página de configuração do LLM Optimizer em **Sufixo do arquivo de log**.

9. Altere a **frequência de envio**. Copie o valor da página de configuração do LLM Optimizer em **Intervalo de Log**.

   ![Intervalo de log](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. Clique em **Avançar** para concluir o processo.

Antes da validação final, a configuração deve ser semelhante a este exemplo:

![Validação da configuração](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
