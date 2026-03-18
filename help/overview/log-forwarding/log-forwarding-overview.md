---
title: Visão geral do encaminhamento de log BYOCDN
description: Saiba como encaminhar logs de CDN do seu provedor para o bucket do S3 da Adobe para coleta de dados de tráfego direto no LLM Optimizer.
feature: Agentic Traffic
source-git-commit: a1ba7684ccef9baf3452cc158fc0d6a12aa7adb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 3%

---


# Visão geral do encaminhamento de log BYOCDN {#cdn-log-forwarding}

O encaminhamento de logs para um CDN gerenciado pelo cliente (BYOCDN) é o processo de enviar os logs de acesso do CDN para o bucket do Amazon S3 da Adobe, para que o LLM Optimizer possa coletar e analisar dados de tráfego de agentes. Sem o encaminhamento de log CDN, o painel [Tráfego Agencial](/help/dashboards/agentic-traffic.md) não pode exibir métricas.

Os guias fornecidos abaixo seguem o mesmo fluxo de trabalho de duas fases:

1. **Integrar no LLM Optimizer** — registre sua CDN na página [Configuração da CDN](/help/dashboards/customer-configuration.md) para gerar as credenciais S3 e os detalhes de caminho necessários.
2. **Configurar sua CDN** — use esses detalhes para criar um trabalho de encaminhamento de log (ou carregar logs manualmente) no console do seu provedor de CDN.

## Provedores de CDN {#cdn-providers}

Siga o guia correspondente para seu provedor de CDN.

| Provedor de CDN | Guia |
|---|---|
| Akamai | [Exibir guia](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [Exibir guia](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront | [Exibir guia](/help/overview/log-forwarding/cloudfront.md) |
| Fastly | [Exibir guia](/help/overview/log-forwarding/fastly.md) |
| Imperva | [Exibir guia](/help/overview/log-forwarding/imperva.md) |
| Outro (CDN manual/não compatível) | [Exibir guia](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>Se seu provedor de CDN não estiver listado acima, use o guia **Outros (CDN manual/não compatível)** que abrange uploads manuais, scripts ad-hoc e qualquer CDN que não seja nativamente compatível.
