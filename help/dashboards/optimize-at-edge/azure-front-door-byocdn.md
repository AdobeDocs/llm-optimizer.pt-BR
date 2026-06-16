---
title: Otimizar no Edge - Azure Front Door (BYOCDN)
description: Saiba como configurar o Azure Front Door BYOCDN para otimizar no Edge no LLM Optimizer.
feature: Opportunities
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: 1d07ce1820e2688a130e410ee88ab329d628356a
workflow-type: tm+mt
source-wordcount: 768
ht-degree: 24%

---


# Porta frontal do Azure (BYOCDN)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após sua conclusão, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

O Azure Front Door não executa código personalizado na borda. O roteamento está configurado usando um **Conjunto de Regras** juntamente com um **grupo de origem** dedicado para Otimização do Edge. O failover é realizado pelas investigações de integridade do grupo de origem com base em prioridades do Azure Front Door.

**Pré-requisitos**

Antes de configurar as regras de roteamento do Azure Front Door, verifique se você tem:

* Acesso ao perfil do Azure Front Door.
* Uma chave da API do Edge Optimize obtida na interface do usuário do LLM Optimizer. Para obter as etapas, consulte [Recuperar suas chaves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para testar o roteamento de preparo, consulte [Chave de API de preparo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

## Etapa 1: criar um grupo de origem para o Edge Otimize

Seu perfil do Azure Front Door já tem um grupo de origem padrão que aponta para sua origem. Criar um grupo de origem **novo** para Otimização de Edge:

* **Nome** `edge-optimize-origin-group`
* **Origens (failover baseado em prioridade):**
   * **Prioridade 1** — `live.edgeoptimize.net` (Cabeçalho de host de origem: `live.edgeoptimize.net`)
   * **Prioridade 2** — seu ponto de extremidade de domínio (por exemplo, `www.example.com`). Isso é para failover: se o Edge Otimize não estiver íntegro, as solicitações serão roteadas para seu domínio, que entra novamente no Azure Front Door e é distribuído a partir de sua origem padrão.
* **Sondagens de integridade:** **Habilitadas**
   * Caminho: `/health/<your-domain>` (por exemplo, `/health/www.example.com`)
   * Protocolo: HTTPS
   * Intervalo: 225 segundos
* **Afinidade da sessão:** **Desabilitada**
* **Validação do nome da entidade do certificado:** **Habilitada**

![Edge Otimizar grupo de origem com duas origens baseadas em prioridade e investigações de integridade](/help/assets/optimize-at-edge/azure-front-door-origin-group.png)

>[!NOTE]
>
>O grupo de origem `edge-optimize-origin-group` mostra um aviso **&quot;Não associado&quot;** no portal. Isso é esperado — é referenciado por meio de uma substituição de rota do Conjunto de regras, não diretamente por uma rota.

## Etapa 2: configurar sua rota

Normalmente, uma rota padrão é criada com o perfil Azure Front Door. O Conjunto de regras (Etapa 3) substitui o grupo de origem para tráfego agêntico, portanto, nenhuma rota separada é necessária para o Edge Otimize.

## Etapa 3: criar o conjunto de regras

Vá para **Conjuntos de regras** > **Adicionar um conjunto de regras** e nomeie-o como `EORouting`. Adicione três regras nessa ordem.

![Conjunto de regras de roteamento mostrando as regras de remoção de cabeçalho e de roteamento de bot](/help/assets/optimize-at-edge/azure-front-door-ruleset-routing.png)

### Regra 1: StripIncomingEOHeaders01

Remove os cabeçalhos de otimização de Edge de entrada para evitar falsificação. Nenhuma condição — aplica-se a todas as solicitações. Parar avaliação: **Desativado**.

**Ações** — Excluir cabeçalho de solicitação para cada um de:

* `x-edgeoptimize-url`
* `x-edgeoptimize-config`
* `x-edgeoptimize-api-key`
* `x-edgeoptimize-fetcher-key`

### Regra 2: EOGPTBotRootGET03

Rastreia solicitações de bot em caminhos de página do HTML para o Edge Otimize. Parar avaliação: **Em**.

**Condições** (todas devem corresponder):

* Método de solicitação: **Igual** `GET`
* Caminho da solicitação: **RegEx** `(^$|^.*/$|(^|.*/)[^./]+$|^.*\.html$)` (corresponde à raiz do site, caminhos que terminam em `/`, caminhos de página sem extensão e caminhos de `.html`)
* User-Agent: **Contém qualquer um de** `chatgpt-user`, `gptbot`, `oai-searchbot`, `adobeedgeoptimize-ai`, `perplexitybot`, `perplexity-user`, `claudebot`, `claude-user`, `claude-searchbot`. Definir transformação de Cadeia de Caracteres para **Minúsculas**.
* `x-edgeoptimize-monitor`: **Não contém** `1`
* `x-edgeoptimize-request`: **Não contém qualquer um de** `failover`, `1`

**Ações**:

* Substituição do cabeçalho da solicitação `x-edgeoptimize-url` = `/{url_path}?{query_string}`
* Substituição do cabeçalho da solicitação `x-edgeoptimize-config` = `LLMCLIENT=TRUE;`
* Substituição do cabeçalho da solicitação `x-edgeoptimize-api-key` = `YOUR_API_KEY`
* Substituição do cabeçalho da solicitação `x-edgeoptimize-monitor` = `1`
* Substituição de configuração de rota: Grupo de origem → `edge-optimize-origin-group`, Protocolo de encaminhamento → Corresponder solicitação recebida, Armazenamento em cache → **Desabilitado**

### Regra 3: HealthProbeRewrite03

Substitui as solicitações de investigação de integridade do Azure Front Door para que elas atinjam sua origem como `/` em vez de `/health/<domain>`. Isso permite que o Edge do monitor Azure Front Door otimize a disponibilidade sem exigir um terminal de integridade dedicado na sua origem. Parar avaliação: **Em**.

![Regra de reescrita de investigação de integridade](/help/assets/optimize-at-edge/azure-front-door-ruleset-healthprobe.png)

**Condições** (todas devem corresponder):

* Caminho da URL de solicitação: **Começa com** `/health/`
* `x-fd-healthprobe`: **Contém** `1`

**Ações**:

* Regravação de URL — Padrão Source: `/health/`, Destino: `/`
* Substituição do cabeçalho de resposta `custom-origin-health` = `routed` (diagnóstico — pode ser removido após a verificação)
* Cabeçalho de solicitação anexado `user-agent` = ` AdobeEdgeOptimize/1.0` (adicione um espaço à esquerda — o Azure Front Door anexa o o valor como está)
* Substituição de configuração de rota: Grupo de origem → `default-origin-group`, Protocolo de encaminhamento → Corresponder solicitação recebida, Armazenamento em cache → **Desabilitado**

## Etapa 4: associar o conjunto de regras à rota

Abra a rota, role até a seção **Regras** na parte inferior e selecione o conjunto de regras `EORouting` na lista suspensa. Se você tiver conjuntos de regras existentes, use **Mover para o início** para posicionar `EORouting` em **#1**. As regras de Otimizar no Edge só interceptam tráfego agêntrico e as solicitações de loop-back de Otimizar do Edge — todo o tráfego restante passa sem ser afetado pelas outras regras. Salvar e aguardar propagação (aproximadamente 20 minutos).

## Permitir otimização no Edge por meio de regras de firewall (opcional)

{{waf-allowlist-setup}}

## Verificar a configuração

Após concluir a configuração, verifique se o tráfego de bots está sendo roteado para o Edge Optimize e se o tráfego humano permanece inalterado.

**1. Tráfego de bots de teste (deve ser otimizado)**

Simular uma solicitação de bot de IA usando um agente de usuário agêntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Teste o tráfego humano (NÃO deve ser afetado)**

Simule uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta **não** deve conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos aos de antes da habilitação da otimização na borda.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bots (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém uma ID de solicitação exclusiva | Ausente |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
