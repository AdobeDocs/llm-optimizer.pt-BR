---
title: Encaminhamento de logs - Fastly
description: Saiba como encaminhar logs de CDN do Fastly para o bucket do S3 do Adobe para coleta de dados de tráfego agênticos no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 4%

---


# Encaminhamento de logs: Fastly {#log-forwarding-fastly}

Esta página explica como encaminhar logs de CDN do Fastly para o bucket S3 do Adobe para coleta de dados de tráfego direto. Você usará a página de configuração do LLM Optimizer CDN para integrar-se ao LLM Optimizer. Após a conclusão do processo de integração, siga as etapas fornecidas nesta página para configurar o encaminhamento de logs no console da Web do Fastly.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Na página do LLM Optimizer [https://llmo.now/](https://llmo.now/):

1. Ir para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Introdução**.
1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecione **Fastly (BYOCDN)**.

   ![Selecionar Fastly](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. Clique em **Integrar**.

## Etapa 2: Criar um terminal S3 no Fastly {#step-2}

Para criar um ponto de extremidade S3, no **Painel de Controle do Fastly**:

1. No painel do Fastly, vá para **serviços de CDN** (não serviços de Computação).
1. Na área **Amazon Web Services S3**, clique em **Criar ponto de extremidade**.
1. Preencha os campos **Criar um ponto de extremidade do Amazon S3**:

| Texto | Descrição |
| --- | --- |
| **Nome** | Nome legível para o endpoint. |
| **Posicionamento** | Padrão |
| **Formato do log** | Use a cadeia de caracteres de formato de log mostrada na seção **cadeia de caracteres de formato de log** abaixo. |
| **Formato de carimbo de data/hora** | `%Y-%m-%dT%H:%M:%S.000` |
| **Nome do bloco** | Copie o **Nome do bucket** da página de configuração do LLM Optimizer. ![Nome do bloco](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Domínio** | Copie o **Nome do Domínio** da página de configuração do LLM Optimizer. ![Nome do domínio](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **Método de acesso** | **Credenciais de usuário** |
| **Credenciais de usuário** | Copie a **Chave de Acesso** e a **Chave Secreta** da página de configuração do LLM Optimizer. ![Chaves de acesso](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Período** | `300` |

**Cadeia de caracteres de formato de log:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>Os gerentes de senha podem preencher automaticamente o campo **Chave secreta** com sua senha do Fastly. Se a integração do AWS falhar, insira a Chave secreta manualmente.

Após concluir as etapas acima, clique em **Opções avançadas** e defina:

| Texto | Descrição |
| --- | --- |
| **Caminho** | Copie **Path** da página de configuração do LLM Optimizer. ![Caminho](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **Selecionar um formato de linha de log** | Em branco |
| **Compactação** | Gzip |
| **Nível de redundância** | Padrão |
| **ACL** | Nenhum |
| **Criptografia do servidor** | Nenhum |
| **Máximo de bytes** | 0 |

Depois de definir as opções avançadas:

1. Clique em **Criar** para criar o ponto de extremidade.
1. No menu **Ativar**, selecione **Ativar na Produção** para implantar.

>[!NOTE]
>
>O Fastly transmite logs continuamente para o S3, o site e a API do S3 disponibilizam arquivos somente após a conclusão do upload.

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
