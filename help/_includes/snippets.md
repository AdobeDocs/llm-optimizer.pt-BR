---
source-git-commit: b13f91d144d4899198891c4dcd841de8cfbb2355
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---
# Trechos

## Verificar o status do roteamento no LLM Optimizer {#verify-routing-status-in-ui}

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração de CDN**.

![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Permitindo a otimização no Edge por meio de regras de firewall (opcional) {#waf-allowlist-setup}

Se o CDN usar um WAF ou Gerenciador de bot:

* Inclua na lista de permissões o agente de usuário `*AdobeEdgeOptimize/1.0*` no WAF ou no Gerenciador de bot para que o serviço Otimizar na Edge possa buscar o conteúdo de origem.
* Se o firewall exigir verificação adicional além do agente do usuário, gere um segredo (por exemplo, `openssl rand -hex 32`) e:
   * Adicione `x-edgeoptimize-fetcher-key` com o segredo em suas regras de roteamento junto com os outros cabeçalhos `x-edgeoptimize-*`.
   * Adicione uma regra do WAF ou do Gerenciador de bot para permitir solicitações em que `x-edgeoptimize-fetcher-key` corresponde ao mesmo segredo.
* Otimizar no Edge encaminha esse cabeçalho como está — você é o proprietário do ciclo de vida completo da chave.

## Retornar à visão geral {#return-to-overview}

Para saber mais sobre como Otimizar na Edge, incluindo oportunidades disponíveis, fluxos de trabalho de otimização automática e perguntas frequentes, volte para a [visão geral de Otimizar na Edge](/help/dashboards/optimize-at-edge/overview.md).
