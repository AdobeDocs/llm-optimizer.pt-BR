---
title: Visão geral do encaminhamento de logs BYOCDN
description: Aprenda como encaminhar os logs da CDN do seu provedor para o bloco S3 da Adobe para coleção de dados de tráfego agêntico no LLM Optimizer.
feature: Agentic Traffic
autotag-review: '2026-05-15T17:53:26.846Z'
TQID: 'https://experienceleague.adobe.com/EPQ6GBjNXpIwYTuzj1xDKkIzuFLOWFPmu0lqSGUAX3I'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 100%

---


# Visão geral do encaminhamento de logs BYOCDN {#cdn-log-forwarding}

O encaminhamento de logs para uma CDN gerenciada pelo cliente (BYOCDN) é o processo de enviar os logs de acesso da sua CDN para o bloco do Amazon S3 da Adobe, para que o LLM Optimizer possa coletar e analisar os dados de tráfego agêntico. Sem o encaminhamento de logs da CDN, o painel de controle do [Tráfego agêntico](/help/dashboards/agentic-traffic.md) não pode exibir métricas.

Os guias fornecidos abaixo seguem o mesmo fluxo de trabalho de duas fases:

1. **Integração no LLM Optimizer**: registre a CDN na página [Configuração da CDN](/help/dashboards/customer-configuration.md) para gerar as credenciais S3 necessárias e os detalhes do caminho.
2. **Configurar a CDN**: use esses detalhes para criar um trabalho de encaminhamento de logs (ou carregue logs manualmente) no console do seu provedor de CDN. Para o CloudFront, você pode usar o console ou concluir a configuração de entrega somente com a **CLI da AWS**; consulte[CloudFront (CLI da AWS)](/help/overview/log-forwarding/cloudfront-cli.md).

## Provedores de CDN {#cdn-providers}

Siga o guia correspondente ao seu provedor de CDN.

| Provedor de CDN | Guia |
|---|---|
| Akamai | [Ver guia](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [Ver guia](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront (console) | [Ver guia](/help/overview/log-forwarding/cloudfront.md) |
| CloudFront (CLI da AWS) | [Ver guia](/help/overview/log-forwarding/cloudfront-cli.md) |
| Fastly | [Ver guia](/help/overview/log-forwarding/fastly.md) |
| Imperva | [Ver guia](/help/overview/log-forwarding/imperva.md) |
| Outro (CDN manual/sem suporte) | [Ver guia](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>Se o seu provedor de CDN não estiver listado acima, use o guia **Outro (CDN manual/sem suporte)** que abrange uploads manuais, scripts ad-hoc e qualquer CDN que não seja nativamente aceita.
