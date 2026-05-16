---
title: Simplificar conteúdo complexo
description: Saiba como o LLM Optimizer identifica páginas de alto tráfego com cópia densa que é difícil de ser interpretada pelos agentes de IA e como revisar e implantar texto simplificado com o recurso Otimizar no Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:58:39.879Z'
TQID: 'https://experienceleague.adobe.com/wO3ZY-fEgOi7cD4dq0kCltk-YJSD431bkA6-9PW42Lo'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 785
ht-degree: 0%

---


# Simplificar conteúdo complexo

A oportunidade Simplificar conteúdo complexo identifica páginas de alto tráfego em que há texto denso ou complexo que dificulta a interpretação das informações principais pelos agentes de IA. Ele apresenta versões mais claras e fáceis de digitalizar da cópia existente, preservando o significado original. Isso ajuda os agentes a analisar, resumir e extrair informações importantes de forma mais confiável.

Para cada URL afetada, você pode revisar sugestões de **Texto Aprimorado**, compará-las com **Visualização** e implantá-las com [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para que o tráfego de agente receba HTML mais nítido sem a necessidade de alterações no sistema de Gerenciamento de Conteúdo (CMS).

## Como ele corrige o problema

As correções são aplicadas usando [Otimizar em Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Disponibiliza um instantâneo pré-renderizado do HTML para agentes de IA.
- Atualiza a página visível para agente de forma que passagens complexas sejam substituídas ou aumentadas com **Texto aprimorado** alinhado à página ativa.
- Funciona na camada CDN (sem alterações no CMS).
- É somente IA — sem impacto para visitantes humanos ou bots de SEO.
- Implanta em minutos e é **totalmente reversível** da interface do LLM Optimizer.

## Como funciona

O LLM Optimizer identifica páginas que recebem tráfego agêntico alto e nas quais as pontuações de conteúdo estão abaixo dos limites de legibilidade, e sugere regravações da cópia. Para cada página que você tem:

**Texto aprimorado** - conteúdo simplificado com base no que já está na página.
**Visualizar** - uma comparação anterior e posterior para tráfego de agente.

As URLs afetadas aparecem na tabela **URLs com sugestões** na guia **Sugestões Atuais**, onde você pode expandir uma linha para inspecionar cada recomendação.

![URLs com sugestões sobre Sugestões Atuais, linha expandida com Texto Aprimorado e Visualização](/help/dashboards/opportunities/assets/simplify-complex-content-expand.png)

A tabela **URLs com sugestões** lista páginas em que um conteúdo simplificado ajudaria na compreensão do agente. As sugestões estão organizadas em **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Para cada URL é possível:

- **Expanda a linha** para exibir **Texto Aprimorado** sugestões para essa página.
- **Visualize** a comparação anterior e posterior para tráfego de agente.
- **Marque como Corrigido** se você abordou a oportunidade fora da LLM Optimizer.
- **Ignorar** sugestões que não são relevantes.

**Exibições** incluem **Sugestões Atuais**, **Sugestões Fixas** (status **Otimizado** quando implantado) e **Sugestões Ignoradas**. Você pode verificar a implantação ativa usando a **Exibir em tempo real** em **Sugestões Corrigidas** e reverter a qualquer momento.

Selecione as URLs ou os itens de linha com **Texto Aprimorado** que você deseja enviar usando as caixas de seleção e use **Marcar como Corrigido**, **Ignorar Sugestões** ou **Implantar otimizações** no cabeçalho do **Plano de oportunidade**. A interface de demonstração também mostra uma contagem de seleção e ações relacionadas com a lista.

![Plano de oportunidade, Sugestões atuais, linha expandida e otimizações de implantação no cabeçalho do plano](/help/dashboards/opportunities/assets/simplify-complex-content-select.png)

### Implantar a otimização

Quando estiver pronto para publicar na borda, clique em **Implantar otimizações**. Uma caixa de diálogo **Implantar no Edge** lista as URLs selecionadas e os detalhes de otimização. Revise a lista e escolha **Implantar** ou **Cancelar**.

![Caixa de diálogo Implantar no Edge](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-dialog.png)

Após uma implantação bem-sucedida, a **Implantação concluída** confirma quantas otimizações entraram em funcionamento e observa que os agentes de IA podem levar tempo para indexar a atualização. Feche a caixa de diálogo e abra **Sugestões Corrigidas** para verificar o status.

![Confirmação de conclusão da implantação](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-confirm.png)

>[!NOTE]
>
>A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugestões Fixas e Visualização em Tempo Real

Em **Sugestões Corrigidas**, as URLs implantadas mostram **Otimizado** na coluna de status. Expanda uma linha para revisar o **Texto Aprimorado** e as instruções implantadas.

![Guia Sugestões Corrigidas com status Otimizado, cópia simplificada expandida, Exibir em Tempo Real e Detalhes](/help/dashboards/opportunities/assets/simplify-complex-content-fixed.png)

Clique em **Exibir em tempo real** na linha para abrir uma exibição somente leitura do **conteúdo da página atual**, conforme fornecido para verificação (incluindo as passagens simplificadas quando aplicadas). Use **Detalhes** para análise.

![Exibir ao vivo — conteúdo da página atual incluindo texto simplificado para agentes](/help/dashboards/opportunities/assets/simplify-complex-content-view-live.png)

Quando for necessário reverter alterações de borda em massa, marque as linhas otimizadas usando as caixas de seleção e use **Reversão** no cabeçalho.

![Sugestões corrigidas com a linha implantada expandida, o status Otimizado e a reversão no cabeçalho](/help/dashboards/opportunities/assets/simplify-complex-content-rollback.png)

## Reversão

Se você mudar de ideia, poderá reverter qualquer otimização implantada. Na exibição **Sugestões Corrigidas**, selecione as linhas otimizadas que deseja reverter e clique em **Reversão** no cabeçalho.

A caixa de diálogo **Reversão** lista as sugestões que serão revertidas, com um breve aviso de que as otimizações implantadas serão revertidas. Confirme a lista e clique em **Reversão** ou **Cancelar**.

![Caixa de diálogo de reversão listando sugestões para reverter](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-dialog.png)

Quando a operação for concluída, um resumo **Revertido com Êxito** será exibido; feche-o para retornar ao painel.

![Reversão concluída — Reversão realizada com êxito](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-confirm.png)

## Experimente na demonstração

Explore o fluxo de trabalho Simplificar conteúdo complexo na [Demonstração do Frescopa](https://play.llmo.now/org/demo-org).
