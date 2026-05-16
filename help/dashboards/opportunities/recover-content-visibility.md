---
title: Recuperar visibilidade do conteúdo
description: Saiba como o LLM Optimizer identifica páginas em que o conteúdo crítico está oculto dos agentes de IA e como recuperar essa visibilidade usando otimização baseada em borda.
feature: Opportunities
autotag-review: '2026-05-15T17:56:37.098Z'
TQID: 'https://experienceleague.adobe.com/rHqJL4RrJr1ghsy4fhXe-JLDrWruNSZgVhXQeRN-iyA'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 928
ht-degree: 1%

---


# Recuperar visibilidade do conteúdo

Os agentes de IA só podem citar o conteúdo que podem acessar. Quando o conteúdo principal de suas páginas está oculto atrás da renderização do lado do cliente e de carregamentos dinâmicos (como descrições de produtos, classificações de usuário, receitas e comentários), os agentes de IA não o veem totalmente, deixando o conteúdo valioso invisível para os sistemas que poderiam citá-lo.

A oportunidade de Visibilidade do conteúdo de recuperação identifica páginas em seu site onde existe essa lacuna de visibilidade. Para cada página afetada, ela mostra exatamente qual conteúdo está faltando na visualização do agente de IA, destaca a lacuna e permite que você aplique correções sem alterações no CMS ou envolvimento do desenvolvedor.

Ele apresenta três métricas principais rapidamente:

- **URLs** — Número de páginas identificadas com uma lacuna de visibilidade do conteúdo.
- **Ganho Estimado de Conteúdo** — O multiplicador estimado de conteúdo que pode ser recuperado aplicando a otimização.
- **Visibilidade do conteúdo média** — o percentual médio do conteúdo visível atualmente para os agentes de IA nas páginas afetadas.

![Recuperar painel de Visibilidades do conteúdo](/help/dashboards/opportunities/assets/recover-content-visibility-overview.png)

Para obter uma visão geral em vídeo desta oportunidade, você pode assistir a [Recuperar Visibilidade do conteúdo](https://www.youtube.com/watch?v=BigPyJssFCw).

Esta oportunidade pode ser otimizada usando a [Otimizar na Edge](/help/dashboards/optimize-at-edge/overview.md). As otimizações são entregues exclusivamente a agentes de IA, sem impacto em visitantes humanos (entrega somente de bot). As otimizações são aplicadas na camada CDN sem a necessidade de alterações no CMS e podem ter efeito em minutos sem envolvimento do desenvolvedor, tornando-a uma implantação rápida e de baixo risco.

## Como funciona

O LLM Optimizer analisa suas páginas comparando o que os agentes de IA podem acessar com o que está realmente presente na página. As páginas que recebem alto tráfego agêntrico, mas têm baixa visibilidade do conteúdo, são exibidas na tabela **URLs com sugestões**, priorizadas por volume de tráfego agêntrico.

Para cada URL afetado, o LLM Optimizer fornece:

- **Análise de IA** — Uma descrição do conteúdo ausente e por que ele é importante para a citação do LLM, juntamente com uma lista de referências de conteúdo que podem ser recuperadas
- **Visibilidade do conteúdo** — A porcentagem do conteúdo visível atualmente para os agentes de IA nessa página
- **Taxa de Ganho de Conteúdo** — O multiplicador estimado do conteúdo recuperável se a otimização for aplicada
- **Visualização** — uma comparação lado a lado do HTML mostrando como a página será exibida agora vs. pós-otimização, para que você possa validar a alteração antes de implantar

A correção é aplicada usando [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) — o recurso de implantação baseado em borda da Adobe que fornece um instantâneo do HTML totalmente pré-renderizado e amigável para IA a agentes de usuário do LLM na camada de CDN, recuperando conteúdo oculto anteriormente sem tocar em seu CMS.

<!-- [URLs with suggestions](/help/dashboards/opportunities/assets/recover-content-visibility-urls.png)-->

## URLs com sugestões

A tabela **URLs com sugestões** lista todas as páginas afetadas e pode ser filtrada por classificação. Para cada URL é possível:

- **Expanda a linha** para exibir a Análise de IA, incluindo qual conteúdo está ausente e por que ele é importante.
- **Visualizar** a comparação lado a lado do HTML da página atual com a versão de pós-otimização.
- **Marcar como Corrigido** depois que o problema for resolvido.
- **Ignorar** sugestões que não são relevantes.

As sugestões são organizadas em três modos de exibição: **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Depois que uma sugestão é implantada, ela é movida para Sugestões Fixas com um status de **Otimizado** e uma ação **Exibir Em Tempo Real** para verificar se a otimização está ativa para tráfego de agente. Sugestões fixas também podem ser revertidas a qualquer momento.

![Sugestões corrigidas com status Otimizado](/help/dashboards/opportunities/assets/recover-content-visibility-fixed.png)

## Implantar a otimização

Depois de revisar as sugestões e selecionar as URLs a serem otimizadas, clique em **Implantar otimizações** para publicar a correção na borda da CDN. Uma caixa de diálogo de confirmação **Implantar no Edge** mostra as URLs selecionadas, seu tipo (Pré-renderização) e a sugestão que está sendo aplicada. Após a implantação, uma tela de confirmação confirma quais URLs foram otimizados com êxito.

>[!NOTE]
>
>A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

![Caixa de diálogo Implantar no Edge](/help/dashboards/opportunities/assets/recover-content-visibility-deploy.png)

## Experimente na demonstração

Veja a oportunidade de Visibilidade do conteúdo de recuperação em ação usando o ambiente de demonstração Frescopa.

[Ver Recuperar Visibilidade do conteúdo na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/prerender/75729489-756a-4c2b-9905-155b1715da5c)

## Perguntas frequentes

**Por que o conteúdo da minha página está oculto dos agentes de IA?**

A maioria dos sites modernos depende do JavaScript para carregar conteúdo dinamicamente após a solicitação de página inicial. Os agentes de IA normalmente não executam o JavaScript, de modo que o conteúdo renderizado no lado do cliente — listas de produtos, análises de usuários, links de artigos de blog e elementos semelhantes — nunca é visto pelo agente de IA, mesmo que seja totalmente visível para visitantes humanos.

**Essa otimização afetará meus visitantes humanos ou bots de SEO?**

Não. Otimizar no Edge direciona apenas agentes de usuário de IA. Os visitantes humanos e os bots de SEO recebem a página original exatamente como antes, sem alterações na experiência ou no desempenho.

**Preciso alterar minha CMS ou envolver desenvolvedores?**

Não. A otimização é aplicada na borda da CDN e não requer alterações de criação, implantações de código ou envolvimento de desenvolvedor. Depois de integrado ao Otimize at Edge, você pode implantar e reverter as alterações em minutos diretamente da interface do LLM Optimizer.

**O que acontece se o conteúdo da minha página for alterado após a implantação?**

Para a Visibilidade do conteúdo de recuperação, o LLM Optimizer usa configurações de TTL de cache baixo para que qualquer atualização de conteúdo no site acione uma atualização em minutos. Os agentes de IA sempre receberão a versão mais atualizada do seu conteúdo.

**Como começar a otimizar na Edge?**

Consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para obter o processo de integração completo, os guias de configuração de CDN e os pré-requisitos.
