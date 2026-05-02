---
title: Adicionar resumos amigáveis ao LLM
description: Saiba como o LLM Optimizer identifica páginas de alto tráfego que não têm resumos concisos e pontos-chave para agentes de IA e como analisá-las e implantá-las com a opção Otimizar no Edge.
feature: Opportunities
source-git-commit: 7f0729839d761ca57236da935c8c7638dd92f32a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---


# Adicionar resumos amigáveis ao LLM

A oportunidade Adicionar resumos intuitivos identifica páginas de alto tráfego que não têm resumos estruturados concisos, o que dificulta que os agentes de IA entendam rapidamente as principais informações na página. Ele apresenta resumos claros e pontos-chave com base no conteúdo existente da página. Isso ajuda os agentes a interpretar e capturar reivindicações de marca importantes com mais eficiência e aumenta a probabilidade de seu conteúdo ser incluído com precisão nas respostas de IA.

Para cada URL afetado, você pode revisar as sugestões geradas pela IA e implantá-las com [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para que o tráfego de agente fique mais claro e possa ser digitalizado sem a necessidade de alterações no CMS (Content Management System).

## Como ele corrige o problema

As correções são aplicadas usando [Otimizar em Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Disponibiliza um instantâneo pré-renderizado do HTML para agentes de IA.
- Enriquece a página com resumos e/ou pontos-chave na HTML que eles recuperam.
- Funciona na camada CDN (sem alterações no CMS).
- É somente IA — sem impacto para visitantes humanos ou bots de SEO.
- Implanta em minutos e é **totalmente reversível** da interface do LLM Optimizer.

## Como funciona

O LLM Optimizer identifica páginas de alto tráfego em que os **resumos** e os **pontos-chave**, no nível de página ou seção, ajudariam na compreensão da IA. As URLs afetadas aparecem na tabela **URLs com sugestões** na guia **Sugestões Atuais**, onde você pode expandir uma linha para inspecionar cada recomendação.

![URLs com sugestões sobre Sugestões Atuais, linha expandida com sugestões de resumo de página e seção](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

A tabela **URLs com sugestões** lista páginas em que os resumos ajudariam na descoberta de agentes. As sugestões estão organizadas em **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Para cada URL é possível:

- **Expanda a linha** para exibir a análise e o texto de resumo proposto (e pontos-chave quando incluídos).
- **Visualize** a comparação anterior e posterior para tráfego de agente.
- **Marque como Corrigido** se você abordou a oportunidade fora da LLM Optimizer.
- **Ignorar** sugestões que não são relevantes.

Cada entrada expandida mostra instruções de resumo no nível da página e da seção, **cópia gerada por IA**, controles de edição e contexto vinculados à página ativa.

Clique em **Visualizar** na coluna **Ações** para abrir a visualização de otimização. Ele compara como a sua página procura tráfego de agente agora com o modo de exibição pós-otimização (por exemplo, inseriu conteúdo de **resumo** e **ponto-chave** alinhado aos posicionamentos sugeridos). Você pode abrir ou fechar essa visualização a qualquer momento antes de implantar.

Quando estiver pronto para publicar, marque o resumo e os itens de linha de ponto principal usando as caixas de seleção. O rodapé mostra quantos estão selecionados e fornece **Marcar como Fixo**, **Ignorar Sugestões** e **Implantar otimizações**.

![Sugestões atuais com itens de linha de resumo selecionados e Implantar otimizações no rodapé](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

### Implantar a otimização

Quando estiver pronto para publicar na borda, clique em **Implantar otimizações**. Uma caixa de diálogo **Implantar no Edge** lista as URLs selecionadas e os detalhes de otimização. Revise a lista e escolha **Implantar** ou **Cancelar**.

![Caixa de diálogo Implantar no Edge](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

Após uma implantação bem-sucedida, a **Implantação concluída** confirma quantas otimizações entraram em funcionamento e observa que os agentes de IA podem levar tempo para indexar a atualização. Feche a caixa de diálogo e abra **Sugestões Corrigidas** para verificar o status.

![Confirmação de conclusão da implantação](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugestões Fixas e Visualização em Tempo Real

Em **Sugestões Corrigidas**, as URLs implantadas mostram **Otimizado** na coluna de status. Expanda uma linha para analisar a cópia resumida e as instruções implantadas.

![Guia Sugestões Corrigidas com status Otimizado, resumos implantados expandidos, Exibição em Tempo Real e Detalhes](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

Clique em **Exibir em tempo real** na linha para abrir uma exibição somente leitura do **conteúdo da página atual** conforme fornecido para verificação (incluindo blocos de **resumo** e **ponto de chave** inseridos, onde aplicados). Use **Detalhes** para análise. Quando for necessário reverter alterações de borda em massa, marque as linhas otimizadas usando as caixas de seleção e use **Reversão** no cabeçalho.

![Sugestões Corrigidas com caixas de seleção para seleção em massa antes da Reversão](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Reversão

Se você mudar de ideia, poderá reverter qualquer otimização implantada. Na exibição **Sugestões Corrigidas**, selecione as linhas otimizadas que deseja reverter e clique em **Reversão** no cabeçalho.

A caixa de diálogo **Reversão** lista as sugestões que serão revertidas, com um breve aviso de que as otimizações implantadas serão revertidas. Confirme a lista e clique em **Reversão** ou **Cancelar**.

![Caixa de diálogo de reversão listando sugestões para reverter](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

Quando a operação for concluída, um resumo **Revertido com Êxito** será exibido; feche-o para retornar ao painel.

![Reversão concluída — Reversão realizada com êxito](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## Experimente na demonstração

Explore o fluxo de trabalho Adicionar Resumos amigáveis para LLM na [Demonstração do Frescopa](https://play.llmo.now/org/demo-org).
