---
title: Adicionar sumário
description: Saiba como o LLM Optimizer identifica páginas de alto tráfego que não têm uma estrutura de navegação clara para agentes de IA e como revisar e implantar um índice com a opção Otimizar no Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:29:21.334Z'
TQID: 'https://experienceleague.adobe.com/A-Oxmmn-Cb4l9-iVx1TAKxvBTEOxRIAnRe1w1PqF6OI'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 655
ht-degree: 0%

---


# Adicionar sumário

>[!NOTE]
>
> **Acesso antecipado** — Este recurso está disponível em Acesso antecipado. A disponibilidade, a qualificação e partes do fluxo de trabalho podem mudar à medida que o recurso amadurece. Entre em contato com a equipe de conta da Adobe em caso de dúvidas sobre o acesso.

A oportunidade Adicionar índice identifica páginas de alto tráfego que não têm um **índice** claro e um guia estrutural, o que dificulta aos agentes de IA analisar a página e mapear consultas de usuário para as seções certas. Ele introduz um Sumário estruturado com **cabeçalhos vinculados por âncora** que refletem as seções principais da página. Essa estrutura ajuda os agentes a extrair, mapear e citar passagens relevantes de forma mais confiável.

Para cada URL afetada, você pode revisar as entradas sugeridas do Sumário e, em seguida, implantá-las com [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para que o tráfego de agente receba um contexto de navegação mais claro sem a necessidade de alterações no Sistema de Gerenciamento de Conteúdo (CMS).

## Como ele corrige o problema

As correções são aplicadas usando [Otimizar em Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Disponibiliza um instantâneo pré-renderizado do HTML para agentes de IA.
- Adiciona um sumário à página.
- Funciona na camada CDN (sem alterações no CMS).
- É somente IA — sem impacto para visitantes humanos ou bots de SEO.
- Implanta em minutos e é **totalmente reversível** da interface do LLM Optimizer.

## Como funciona

O LLM Optimizer identifica páginas de alto tráfego nas quais um **Sumário** melhoraria a forma como os agentes de IA navegam pelos cabeçalhos e seções. Para cada página, as sugestões são baseadas nos cabeçalhos já existentes na página, de modo que o Índice reflita a estrutura da página.

As URLs afetadas aparecem na tabela **URLs com sugestões** na guia **Sugestões Atuais**.

Em **Sugestões Atuais**, para cada URL é possível:

- **Expanda a linha** para inspecionar o Sumário proposto (analisado a partir de títulos da página e apresentado como entradas vinculadas à âncora).
- **Visualizar** uma antes e depois da comparação.
- **Marque como Corrigido** se você abordou a oportunidade fora da LLM Optimizer.
- **Ignorar** sugestões que não são relevantes.

As sugestões estão organizadas em **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**, de acordo com outras oportunidades do Otimizar no Edge.

### Implantar a otimização

Quando estiver pronto para publicar na borda, selecione as sugestões de índice que deseja implantar. O rodapé resume quantos itens estão selecionados e geralmente oferece **Marcar como Corrigido**, **Ignorar Sugestões** e **Implantar otimizações**.

Clique em **Implantar otimizações**. Uma caixa de diálogo **Implantar no Edge** lista as URLs selecionadas e os detalhes de otimização. Revise a lista e escolha **Implantar** ou **Cancelar**.

Após uma implantação bem-sucedida, a **Implantação concluída** confirma quantas otimizações ficaram ativas. Feche a caixa de diálogo e abra **Sugestões Corrigidas** para verificar o status.

>[!NOTE]
>
>A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugestões Fixas e Visualização em Tempo Real

Em **Sugestões Corrigidas**, as URLs implantadas mostram **Otimizado** na coluna de status. Expanda uma linha para revisar o Sumário implantado, use os **Detalhes** para as análises, quando disponíveis, ou clique em **Exibir Em Tempo Real** para abrir uma exibição somente leitura de **conteúdo da página atual**, conforme fornecido para verificação (incluindo o **Sumário** inserido).

Quando for necessário reverter alterações de borda em massa, marque as linhas otimizadas usando as caixas de seleção e use **Reversão** no cabeçalho.

## Reversão

Se você mudar de ideia, poderá reverter uma otimização implantada. Na exibição **Sugestões Corrigidas**, selecione as linhas otimizadas que deseja reverter e clique em **Reversão** no cabeçalho.

A caixa de diálogo **Reversão** lista as sugestões que serão revertidas, com um breve aviso de que as otimizações implantadas serão revertidas. Confirme a lista e clique em **Reversão** ou **Cancelar**.

Quando a operação for concluída, um resumo **Revertido com Êxito** será exibido; feche-o para retornar ao painel.
