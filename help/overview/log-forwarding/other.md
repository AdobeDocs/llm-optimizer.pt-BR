---
title: Encaminhamento de logs - Outro (upload manual)
description: Saiba como fazer upload manual de logs CDN no bucket do S3 da Adobe para coleta de dados de tráfego agenciados no LLM Optimizer ao usar um provedor CDN não compatível.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---


# Encaminhamento de Log: Outro (Upload Manual) {#log-forwarding-other}

O método de provisionamento **Outro BYOCDN** é uma opção abrangente para clientes que desejam fornecer logs de CDN à LLM Optimizer quando:

- **Uploads manuais** são preferíveis - por exemplo, as equipes operacionais exportam logs e os carregam periodicamente.
- **Processos automatizados ad hoc** são usados - scripts únicos, exportações agendadas, trabalhos sem servidor.
- O cliente usa uma **CDN que não tem suporte nativo** pelas integrações de encaminhamento de log integradas.

Esse método imita o modelo de &quot;encaminhamento contínuo&quot;: os logs são produzidos e carregados no local S3 esperado e eventualmente são processados automaticamente pelos pipelines de assimilação.

## Etapa 1: integrar no LLM Optimizer {#step-1}

No [LLM Optimizer](https://llmo.now/):

1. Ir para **Configuração**.

   ![Botão Configuração](/help/overview/assets/log-forwarding/common/config-button.png)

1. Clique na guia **Configuração da CDN**.

   ![Guia Configuração de CDN](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Clique em **Introdução**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Ao lado de **Ativar insights de tráfego de IA**, clique em **Configurar**.

   ![Configurar](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecione **Outros**.

   ![Selecionar outro](/help/overview/assets/log-forwarding/other/other-select.png)

1. Clique em **Integrar**.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Etapa 2: Preparar e fazer upload de logs {#step-2}

### Formato de log necessário (Linhas JSON) {#log-format}

Os logs devem ser carregados como JSON delimitado por nova linha (**um objeto JSON por linha**). Cada linha de log deve incluir os seguintes campos **exatamente como escrito abaixo**.

#### Esquema campo a campo {#schema}

| Texto | Tipo | Descrição | Exemplo |
|---|---|---|---|
| **carimbo de data/hora** | String | O carimbo de data/hora da solicitação seguindo o formato **ISO 8601**. | `"2025-02-01T23:00:05Z"` |
| **host** | String | O domínio da Web que o cliente solicitou. | `"www.example.com"` |
| **url** | String | O **caminho** e os **parâmetros de consulta** são obrigatórios, enquanto o domínio **não** deve ser incluído. | `"/home?utm_source=google"` |
| **método_de_solicitação** | String | O método de solicitação HTTP, às vezes chamado de verbos HTTP. | `"GET"` |
| **request_user_agent** | String | O cabeçalho da solicitação do Agente do usuário HTTP. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | String | O cabeçalho da solicitação Referenciador de HTTP (pode estar vazio). | `"https://chatgpt.com"` |
| **status_de_resposta** | Número inteiro | O código do status da resposta HTTP. | `200` |
| **tipo_de_conteúdo_de_resposta** | String | O cabeçalho de resposta HTTP Content-Type. | `"text/html; charset=utf-8"` |
| **tempo_até_o_primeiro_byte** | Número inteiro | O tempo entre a criação de uma conexão com o servidor e o download do conteúdo de uma página da Web em **milissegundos**. Defina como zero se for desconhecido ou não estiver disponível. | `42` |

#### Exemplo de linhas de log {#example}

O exemplo a seguir mostra três linhas de log:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Isenção de responsabilidade crítica (ortografia e tipos) {#disclaimer}

Os pipelines de assimilação e agregação são estritos em relação a **nomes de campo e tipos de dados**.

- Os nomes de campos devem corresponder a **exatamente** (letra maiúscula e minúscula).
- Os Tipos de dados devem estar corretos, como se segue:
   - **carimbo de data/hora** deve ser uma cadeia de caracteres com o formato **ISO 8601**. Os carimbos de data e hora semelhantes ao UNIX podem não funcionar.
   - **response_status** deve ser um inteiro.
   - **time_to_first_byte** deve ser um inteiro e usar milissegundos.
   - As cadeias de caracteres devem ser cadeias JSON válidas.
- Campos JSON malformados ou ausentes/incorretos podem fazer com que os registros sejam ignorados ou não sejam analisados, resultando em dados ausentes nos relatórios.

### Localização de upload e cadência de processamento {#upload-location}

#### Regra de caminho {#path-rule}

Carregar logs no caminho de pasta apropriado usando o formato: **`yyyy/mm/dd/`** (com barras).

Um exemplo de log de 1º de fevereiro de 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Regra de processamento {#processing-rule}

- Os logs carregados durante um determinado **dia UTC** são processados pelos pipelines **perto do fim desse dia UTC** (execução diária).
- Os logs carregados nas **pastas de dias anteriores** (preenchimento retroativo) foram **detectados e processados** em 24 horas.

## Cenários {#scenarios}

### Cenário 1: Logs no Splunk / Elasticsearch — exportar e carregar para S3 {#scenario-splunk}

**Meta**: recuperar logs de plataformas de observação existentes e entregá-los ao local S3.

- Extraia os campos obrigatórios dos eventos de pesquisa do Splunk/Elastic.
- Transforme cada evento em um objeto JSON seguindo o esquema acima (linhas JSON).
- Carregue os arquivos resultantes no compartimento S3 designado e no caminho **dia UTC atual**: `…/byocdn-other/yyyy/mm/dd/`
- Os logs serão processados automaticamente até o final do dia UTC.

### Cenário 2: Lambda / Azure Function — formatar e enviar para S3 {#scenario-serverless}

**Meta**: usar a computação sem servidor para buscar/receber logs de CDN, normalizá-los e entregá-los ao local S3.

- A função recupera logs da origem do cliente (armazenamento de log, fila, armazenamento de blob etc.).
- A função mapeia campos para o esquema esperado e emite **Linhas JSON**.
- A função carrega a saída para: `…/byocdn-other/yyyy/mm/dd/`
- Os logs serão processados automaticamente até o final do dia UTC.

## Lista de verificação rápida {#checklist}

- **Um objeto JSON por linha** (linhas JSON)
- **Ortografia exata do campo** conforme especificado
- Tipos de dados corretos
- **time_to_first_byte** em milissegundos (número inteiro)
- Carregue para a pasta UTC apropriada: **aaaa/mm/dd/** em **byocdn-other**
