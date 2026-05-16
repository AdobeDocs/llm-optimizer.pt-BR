---
title: Adicionar Resumos de Transcrição de Multimídia
description: Saiba como o LLM Optimizer identifica páginas em que as informações principais são incorporadas em vídeo sem texto legível por máquina e como revisar e implantar resumos de transcrição gerados por IA com o recurso Otimizar no Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:28:28.569Z'
TQID: 'https://experienceleague.adobe.com/LiXMsMq6D08ciXR85aQBNDpmR5Csiv-5b9kv3lfTpDc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 775
ht-degree: 0%

---


# Adicionar Resumos de Transcrição de Multimídia

>[!NOTE]
>
> **Acesso antecipado** — Os Resumos da Transcrição de Multimídia de Adição estão disponíveis em Acesso Antecipado. A disponibilidade, a qualificação e partes do fluxo de trabalho podem mudar à medida que o recurso amadurece. Entre em contato com a equipe de conta da Adobe em caso de dúvidas sobre o acesso.

A oportunidade Adicionar resumos de transcrição de multimídia identifica páginas em que informações importantes estão em vídeo ou outras mídias, sem transcrições ou resumos de texto curtos que os agentes de IA podem ler. Ele apresenta **resumos de transcrição gerados por IA** com base na mídia e no contexto da página ao redor. Ele ajuda a recuperar informações importantes da marca que, de outra forma, seriam perdidas, tornando o conteúdo multimídia compreensível para os agentes de IA.

Para cada URL afetado, você pode revisar os detalhes propostos do **Patch de Conteúdo**, da **Implementação** (por exemplo, o seletor de CSS de destino e a operação) e da **Justificativa**. Em seguida, implante com [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para que o tráfego de agente receba o HTML enriquecido sem a necessidade de alterações no Sistema de Gerenciamento de Conteúdo (CMS).

## Como ele corrige o problema

As correções são aplicadas usando [Otimizar em Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Disponibiliza um instantâneo pré-renderizado do HTML para agentes de IA.
- Enriquece a página com o texto de resumo da transcrição no HTML que eles recuperam (por exemplo, próximo ao vídeo em linha relevante).
- Funciona na camada CDN (sem alterações no CMS).
- É somente IA — sem impacto para visitantes humanos ou bots de SEO.
- Implanta em minutos e é **totalmente reversível** da interface do LLM Optimizer.

## Como funciona

O LLM Optimizer sinaliza páginas de alto tráfego onde o texto legível por máquina está ausente para mídia incorporada, com base na sua configuração e estrutura de página. As URLs afetadas aparecem na tabela **URLs com sugestões** na guia **Sugestões Atuais**, onde você pode expandir uma linha para inspecionar cada **Patch de Conteúdo**, como ele será aplicado e por que ele é recomendado.

Para cada página, você tem:

**Resumo de multimídia** - Resumos estruturados derivados do conteúdo de vídeo.
**Visualizar** - Antes e depois da comparação de páginas.

![URLs com sugestões sobre Sugestões Atuais, linha expandida com Patch de Conteúdo, Detalhes de implementação e Fundamentação](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-expand.png)

A tabela **URLs com sugestões** lista páginas em que a transcrição ou o texto de resumo ajudaria na descoberta de agente. As sugestões estão organizadas em **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Para cada URL é possível:

- **Expanda a linha** para exibir o texto **Patch de Conteúdo**, os detalhes de **Implementação** (incluindo a operação DOM planejada e o seletor de CSS) e a **Razão** para a alteração.
- **Visualize** a comparação anterior e posterior para tráfego de agente.
- **Marque como Corrigido** se você abordou a oportunidade fora da LLM Optimizer.
- **Ignorar** sugestões que não são relevantes.

É possível editar o texto de correção na linha quando suportado (controle de lápis) e, em seguida, usar as caixas de seleção de linha para selecionar o que implantar. O rodapé mostra quantos estão selecionados e fornece **Marcar como Fixo**, **Ignorar Sugestões** e **Implantar otimizações**.

### Implantar a otimização

Quando estiver pronto para publicar na borda, clique em **Implantar otimizações**. Uma caixa de diálogo **Implantar no Edge** lista as URLs, os seletores e as operações que você está prestes a executar. Revise a lista e escolha **Implantar** ou **Cancelar**.

![Implantar na caixa de diálogo do Edge para patches de conteúdo de resumo de transcrição multimídia](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-dialog.png)

Após uma implantação bem-sucedida, a **Implantação concluída** confirma quantas otimizações ficaram ativas. Feche a caixa de diálogo e abra **Sugestões Corrigidas** para verificar o status.

![Confirmação de conclusão da implantação](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-confirm.png)

>[!NOTE]
>
> A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugestões Fixas e Visualização em Tempo Real

Em **Sugestões Corrigidas**, as URLs implantadas mostram **Otimizado** na coluna de status. Expanda uma linha para revisar os detalhes de **Patch de Conteúdo**, **Implementação** e **Razão** em tempo real. Além disso, você pode usar os **Detalhes** para análise ou o **Exibir em tempo real**, onde disponível, para confirmar o tráfego de agente que recebe.

![Sugestões corrigidas com status Otimizado, Patch de Conteúdo expandido e Reversão](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-fixed.png)

Para reverter em massa, marque as linhas otimizadas usando as caixas de seleção e use **Reverter** no cabeçalho.

![Sugestões Corrigidas com linhas selecionadas antes da Reversão](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-select-in-fixed.png)

## Reversão

Se você mudar de ideia, poderá reverter uma otimização implantada. Em **Sugestões Corrigidas**, selecione as linhas a serem revertidas e clique em **Reversão**.

A caixa de diálogo **Reversão** lista as sugestões que serão revertidas e avisa que as otimizações implantadas serão removidas do caminho ativo para tráfego de agente. Confirme e clique em **Reversão** ou **Cancelar**.

![Caixa de diálogo de reversão listando sugestões para reverter](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-dialog.png)

Quando a operação for concluída, um resumo **Revertido com Êxito** será exibido; feche-o para retornar ao painel.

![Reversão concluída — Reversão realizada com êxito](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-confirm.png)

## Experimente na demonstração

Explore o fluxo de trabalho Adicionar resumos de transcrição de multimídia na [Demonstração do Frescopa](https://play.llmo.now/org/demo-org).
