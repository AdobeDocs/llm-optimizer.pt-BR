---
title: Enriquecimento da página de detalhes do produto
description: Saiba como o LLM Optimizer identifica páginas de produtos em que os dados de catálogo estão ocultos dos agentes de IA e como recuperar essa visibilidade usando otimização baseada em borda e insights de catálogo de produtos viabilizados pelo Adobe Commerce.
feature: Opportunities
source-git-commit: c0e4c82a5eedd864d654557173dd1dcfa5b78362
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---


# Enriquecer páginas de detalhes do produto

Os agentes de IA só podem recomendar produtos que eles entendam completamente. Na maioria das lojas de comércio, as páginas de produtos são projetadas para compradores humanos. Dessa forma, esses produtos dependem de guias renderizadas pela JavaScript, painéis expansíveis, assistentes de compras, modais interativos e links para as variantes de produtos de superfície, especificações e recursos. Os agentes de IA não analisam as profundezas da Página de detalhes do produto, o que significa que esses dados avançados do produto nunca são vistos pelos rastreadores do LLM que impulsionam a descoberta orientada por IA, mesmo quando são totalmente visíveis para visitantes humanos.

A oportunidade Enriquecer páginas de detalhes do produto identifica páginas de produto no catálogo do Adobe Commerce, onde existe essa lacuna de visibilidade. Com a tecnologia do Catálogo do Adobe Commerce, ele compara o que os agentes de IA podem acessar na loja com os dados completos do produto disponíveis no catálogo e exibe todos os atributos, variantes e a profundidade das características do seu produto que estão ausentes na visualização do agente de IA.

Ele apresenta as seguintes métricas principais rapidamente:

- **Páginas de produto** — A lista de todas as páginas de detalhes do produto identificadas com uma lacuna de visibilidade de dados de catálogo.
- **Tráfego de Agente** — O total de visitas e interações em um site iniciadas e orientadas por agentes de IA autônomos (como assistentes ou bots alimentados por LLM) que atuam em nome dos usuários para descobrir, recuperar ou se envolver com conteúdo.

![Enriquecer Painel das Páginas de Detalhes do Produto](/help/dashboards/opportunities/assets/enrich-product-detail-pages-overview.png)

Esta oportunidade pode ser otimizada usando a [Otimizar na Edge](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge). As otimizações são fornecidas exclusivamente para agentes de IA sem impacto para visitantes humanos (entrega somente de bot), aplicadas na camada CDN sem a necessidade de alterações no CMS ou catálogo, e podem ter efeito em minutos sem envolvimento do desenvolvedor, tornando-o um caminho de implantação rápido e de baixo risco para catálogos de produtos grandes.

## Como funciona

O Adobe Commerce Catalog Agent lê todos os dados do catálogo de produtos, incluindo: variantes, relacionamentos mais profundos de produtos, atributos, facetas, metadados de categoria e todas as características do produto. Em seguida, compara os dados com o que está realmente acessível aos agentes de IA no PDP da loja correspondente. As páginas em que os dados do catálogo estão ocultos dos rastreadores de IA são exibidas na tabela **URLs com sugestões**, priorizadas por volume de tráfego de agente.

Para cada página de produto afetada, o LLM Optimizer fornece:

- **Visualização da análise de IA** — uma lista completa de quais informações de catálogo estão ausentes na exibição do agente de IA e por que elas são importantes para a descoberta de produtos orientada por LLM, incluindo uma lista de pontos de dados recuperáveis, como variantes de produtos, opções de tamanho, especificações de material e detalhes de compatibilidade, entre outros.

A correção é aplicada usando [Otimizar no Edge](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge) — o recurso de implantação em borda da Adobe que fornece um instantâneo do HTML totalmente pré-renderizado e amigável para IA a agentes de usuário do LLM na camada de CDN. Isso recupera todos os dados de catálogo ocultos anteriormente (incluindo variantes de produtos, especificações técnicas e detalhes de recursos) sem tocar no catálogo do Commerce ou na interface visível humana da loja.

![URLs com tabela de sugestões](/help/dashboards/opportunities/assets/enrich-product-detail-pages-suggestions.png)

## URLs com sugestões

A tabela **URLs com sugestões** lista todas as páginas de produtos identificadas que se beneficiam de uma otimização. Para cada URL de produto, é possível:

- **Visualizar** para exibir a Análise de IA, incluindo quais informações de catálogo estão ausentes e por que elas são importantes para a descoberta orientada por IA
- **Marcar como Corrigido** depois que a otimização tiver sido implantada e validada
- **Ignorar** sugestões que não são relevantes para sua estratégia de merchandising

As sugestões são organizadas em três modos de exibição: **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Depois que uma sugestão é implantada, ela é movida para Sugestões Fixas com um status de **Otimizado** e uma ação **Exibir Ativo** para verificar se o enriquecimento está ativo para tráfego de agente. As sugestões fixas podem ser revertidas a qualquer momento.

## Implantar a otimização

Depois de revisar as sugestões e selecionar as páginas de produto a serem otimizadas, clique em **Implantar otimizações** para publicar o enriquecimento na borda da CDN. Uma caixa de diálogo de confirmação **Implantar no Edge** mostra as URLs do produto selecionado, o tipo de otimização e o enriquecimento sendo aplicado. Após a implantação, uma tela de confirmação confirma quais páginas de produto foram otimizadas com êxito.

A otimização é entregue exclusivamente aos agentes de usuário de IA por meio da camada de borda CDN. Visitantes humanos continuam a ver sua experiência de loja existente exatamente como antes, sem alterações no design PDP, desempenho da página ou experiência da marca.

>[!NOTE]
>
>A implantação de otimizações requer (1) a conexão do LLM Optimizer ao Adobe Commerce e (2) a conclusão do processo de integração Otimizar na Edge.

Se a sua instância do Commerce ainda não estiver conectada ao LLM Optimizer, você será direcionado para a configuração da conexão antes que os enriquecimentos possam ser aplicados.

Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge).

![Caixa de diálogo Implantar no Edge](/help/dashboards/opportunities/assets/enrich-product-detail-pages-deploy.png)

## Experimente na demonstração

Veja a oportunidade Enriquecer páginas de detalhes do produto em ação usando o ambiente de demonstração Frescopa.

[Visualizar as páginas de detalhes do produto enriquecido na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Perguntas frequentes

**Por que meus dados de catálogo de produtos estão ocultos dos agentes de IA?**

As vitrines da Commerce são criadas para compradores humanos. As características do produto, as variantes, as opções de tamanho, os detalhes do material e outras especificações técnicas geralmente são exibidos por meio de interações orientadas pelo JavaScript, como guias, painéis recolhíveis, modais pop-up, links e assistentes de compras. Os agentes de IA não analisam as profundezas da Página de detalhes do produto, de modo que todos esses dados são invisíveis para os rastreadores do LLM, mesmo quando estão totalmente presentes no catálogo de produtos. O resultado é que os agentes de IA fazem recomendações de produtos com base em uma fração das informações reais do produto disponíveis.

**Quais tipos de dados de produto essa otimização recupera?**

O Agente de catálogo recupera todas as informações de produto disponíveis no catálogo do Adobe Commerce que não estão acessíveis na loja para agentes de IA. Isso inclui caracteres de produtos, relações, variantes (tamanhos, cores, configurações), especificações técnicas e atributos, detalhes de compatibilidade, metadados de categoria e valores de facetas.

**Essa otimização afetará meus visitantes humanos, bots de SEO ou desempenho de vitrine?**

Não. Otimizar no Edge direciona apenas agentes de usuário de IA. Os visitantes humanos e os bots de SEO recebem a página original do produto exatamente como antes, sem alterações na experiência, no desempenho do carregamento da página ou no design da loja.

**Preciso alterar meu catálogo do Commerce, o CMS ou envolver desenvolvedores?**

Não. A otimização é aplicada na camada de borda CDN e não requer alterações no catálogo do Adobe Commerce, nenhuma implantação de código e nenhum envolvimento do desenvolvedor. Depois de integrado ao Otimize at Edge, você pode implantar e reverter enriquecimentos em minutos diretamente da interface do LLM Optimizer.

**O que acontece se meus dados de produto forem alterados após a implantação?**

Para a oportunidade Enriquecer páginas de detalhes do produto, o LLM Optimizer usa configurações TTL de baixo cache para que qualquer atualização de produto no catálogo do Commerce acione uma atualização em minutos. Os agentes de IA sempre receberão os dados mais atualizados do produto disponíveis.
