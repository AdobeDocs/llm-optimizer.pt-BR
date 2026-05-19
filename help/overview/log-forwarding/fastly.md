---
title: Encaminhamento de logs – Fastly
description: Saiba como encaminhar logs de CDN do Fastly para o bloco S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:51:51.808Z'
TQID: 'https://experienceleague.adobe.com/9SH1I6ajHKLFeEWXy-NpvPm-Ylk2xBKhQro3qobVEX8'
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
source-wordcount: 381
ht-degree: 100%

---


# Encaminhamento de logs: Fastly {#log-forwarding-fastly}

Esta página explica como encaminhar logs de CDN do Fastly para o bloco S3 da Adobe para coleção de dados de tráfego agêntico. Você usará a página de configuração da CDN do LLM Optimizer para fazer a integração com o LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no console da Web do Fastly.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Vá para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Começar**.
1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecione **Fastly (BYOCDN)**.

   ![Selecionar Fastly](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. Clique em **Integrar**.

## Etapa 2: Criar um ponto de acesso S3 no Fastly {#step-2}

Para criar um ponto de acesso S3, no **Painel de controle do Fastly**:

1. No painel do Fastly, vá para **serviços de CDN** (não serviços de Computação).
1. Na área **Amazon Web Services S3**, clique em **Criar ponto de acesso**.
1. Preencha os campos **Criar um ponto de acesso do Amazon S3**:

| Texto | Descrição |
| --- | --- |
| **Nome** | Nome legível para o ponto de acesso. |
| **Posicionamento** | Padrão |
| **Formato do log** | Use a string de formato de log mostrada na seção **String de formato de log** abaixo. |
| **Formato de carimbo de data e hora** | `%Y-%m-%dT%H:%M:%S.000` |
| **Nome do bloco** | Copie o **Nome do bloco** da página de configuração do LLM Optimizer. ![Nome do bloco](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Domínio** | Copie o **Nome do domínio** da página de configuração do LLM Optimizer. ![Nome do domínio](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **Método de acesso** | **Credenciais do usuário** |
| **Credenciais do usuário** | Copie a **Chave de acesso** e a **Chave secreta** da página de configuração do LLM Optimizer. ![Chaves de acesso](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Ponto** | `300` |

**String de formato de log:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>Os gerenciadores de senhas podem preencher automaticamente o campo **Chave secreta** com a senha do Fastly. Se a integração do AWS falhar, insira a Chave secreta manualmente.

Após concluir as etapas acima, clique em **Opções avançadas** e defina:

| Texto | Descrição |
| --- | --- |
| **Caminho** | Copie o **Caminho** da página de configuração do LLM Optimizer. ![Caminho](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **Selecionar um formato de linha de log** | Em branco |
| **Compactação** | Gzip |
| **Nível de redundância** | Padrão |
| **ACL** | Nenhum |
| **Criptografia no lado do servidor** | Nenhum |
| **Máximo de bytes** | 0 |

Depois de definir as opções avançadas:

1. Clique em **Criar** para criar o ponto de acesso.
1. No menu **Ativar**, selecione **Ativar na Produção** para implantar.

>[!NOTE]
>
>O Fastly transmite logs continuamente para o S3; o site e a API do S3 disponibilizam arquivos somente após a conclusão do upload.

### Exemplo de entrada de log {#example}

Veja abaixo um exemplo de string de formato para envio de dados ao Amazon S3:

```json
{
  "timestamp": "2026-02-10T05:05:36+0000",
  "host": "example.com",
  "url": "/my/path",
  "request_method": "GET",
  "request_referer": "https://example.com/my/other/path",
  "request_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
  "response_status": 200,
  "response_content_type": "text/css; charset=utf-8",
  "client_country_code": "argentina",
  "time_to_first_byte": "0.138"
}
```
