---
title: Encaminhamento de logs – Outros (upload manual)
description: Saiba como fazer upload manual de logs da CDN para o bloco S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer ao usar um provedor de CDN incompatível.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:54:15.685Z'
TQID: 'https://experienceleague.adobe.com/YBfhS4oM0qYRkFvS3zPzzcFAeLNBucRH5QmMBUH8h4E'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 670
ht-degree: 100%

---


# Encaminhamento de logs: outros (upload manual) {#log-forwarding-other}

O método de provisionamento **Outro BYOCDN** é uma opção abrangente para clientes que desejam fornecer logs da CDN ao LLM Optimizer quando:

- **Uploads manuais** são preferíveis, por exemplo, as equipes operacionais exportam logs e fazem upload deles periodicamente.
- São utilizados **processos automatizados ad-hoc**: scripts pontuais, exportações programadas, trabalhos sem servidor.
- O cliente usa uma **CDN que não é suportada nativamente** pelas integrações de encaminhamento de logs integradas.

Este método imita o modelo de “encaminhamento contínuo”: os registros são produzidos e enviados como upload no local esperado do S3 e, eventualmente, sendo posteriormente processados automaticamente pelos pipelines de ingestão.

## Etapa 1: integrar no LLM Optimizer {#step-1}

Em [LLM Optimizer](https://llmo.now/):

1. Vá para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia de Configuração da CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Começar**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego com IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Outro**.

   ![Selecione Outro](/help/overview/assets/log-forwarding/other/other-select.png)

1. Clique em **Integrar**.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Passo 2: Preparar e fazer upload dos logs {#step-2}

### Formato de log obrigatório (linhas JSON) {#log-format}

Os logs devem ser enviados como JSON delimitado por nova linha (**um objeto JSON por linha**). Cada linha de log deve incluir os seguintes campos **exatamente como escrito abaixo**.

#### Esquema campo por campo {#schema}

| Texto | Tipo | Descrição | Exemplo |
|---|---|---|---|
| **Carimbo de data e hora** | String | O carimbo de data e hora da solicitação seguindo o formato **ISO 8601**. | `"2025-02-01T23:00:05Z"` |
| **host** | String | O domínio da web solicitado pelo cliente. | `"www.example.com"` |
| **url** | String | O **caminho** e os **parâmetros de consulta** são obrigatórios, enquanto o domínio **não** deve ser incluído. | `"/home?utm_source=google"` |
| **request_method** | String | O método de solicitação HTTP, às vezes chamado de verbos HTTP. | `"GET"` |
| **request_user_agent** | String | O cabeçalho de solicitação HTTP User-Agent. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | String | O cabeçalho de solicitação HTTP Referer (pode estar em branco). | `"https://chatgpt.com"` |
| **response_status** | Número inteiro | Código do status da resposta HTTP. | `200` |
| **response_content_type** | String | Cabeçalho de resposta HTTP Content-Type. | `"text/html; charset=utf-8"` |
| **time_to_first_byte** | Número inteiro | O tempo entre a criação de uma conexão com o servidor e o download do conteúdo de uma página da Web em **milissegundos**. Defina como zero se for desconhecido ou indisponível. | `42` |

#### Exemplo de linhas de log {#example}

O exemplo a seguir mostra três linhas de log:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Aviso importante (ortografia e tipos) {#disclaimer}

Os pipelines de ingestão e agregação são estritos em relação a **nomes de campo e tipos de dados**.

- Os nomes de campos devem corresponder a **exatamente** (maiúsculas/minúsculas e ortografia).
- Os Tipos de dados devem estar corretos, como se segue:
   - **carimbo de data e hora** deve ser uma string de caracteres com o formato **ISO 8601**. Os carimbos de data e hora semelhantes ao UNIX podem não funcionar.
   - **response_status** deve ser um número inteiro.
   - **time_to_first_byte** deve ser um número inteiro e usar milissegundos.
   - Strings devem ser strings JSON válidas.
- Campos JSON malformados ou ausentes/incorretos podem fazer com que os logs sejam ignorados ou não sejam analisados, resultando em dados ausentes nos relatórios.

### Localização de upload e cadência de processamento {#upload-location}

#### Regra de caminho {#path-rule}

Fazer upload de logs no caminho de pasta apropriado usando o formato: **`yyyy/mm/dd/`** (com barras).

Um exemplo de log de 1º de fevereiro de 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Regra de processamento {#processing-rule}

- Os logs carregados durante um determinado **dia UTC** são processados pelos pipelines **perto do fim desse dia UTC** (execução diária).
- Os logs enviados nas **pastas de dias anteriores** (preenchimento retroativo) são **detectados e processados** dentro de 24 horas.

## Cenários {#scenarios}

### Cenário 1: logs no Splunk / Elasticsearch — exportar e fazer upload para o S3 {#scenario-splunk}

**Meta**: recuperar logs de plataformas de observação existentes e entregá-los ao local do S3.

- Extraia os campos obrigatórios dos eventos de pesquisa do Splunk/Elastic.
- Transforme cada evento em um objeto JSON seguindo o esquema acima (linhas JSON).
- Faça upload do(s) arquivo(s) resultante(s) no bloco S3 designado e no caminho do **dia UTC atual**: `…/byocdn-other/yyyy/mm/dd/`
- Os logs serão processados automaticamente até o final do dia UTC.

### Cenário 2: Lambda / Azure Function — formatar e fazer upload para o S3 {#scenario-serverless}

**Meta**: usar a computação sem servidor para buscar/receber logs da CDN, normalizá-los e entregá-los ao local do S3.

- A função recupera logs da origem do cliente (armazenamento de log, fila, armazenamento de blob, etc.).
- A função mapeia campos para o esquema esperado e emite **Linhas JSON**.
- A função faz upload da saída para: `…/byocdn-other/yyyy/mm/dd/`
- Os logs serão processados automaticamente até o final do dia UTC.

## Lista de verificação rápida {#checklist}

- **Um objeto JSON por linha** (linhas JSON)
- **Ortografia exata do campo** conforme especificado
- Tipos de dados corretos
- **time_to_first_byte** em milissegundos (número inteiro)
- Fazer upload para a pasta UTC apropriada: **dd/mm/yyyy/** em **byocdn-other**
