---
title: Adicionar perguntas frequentes relevantes
description: Saiba como o LLM Optimizer identifica páginas de alto tráfego que não têm conteúdo estruturado de perguntas e respostas para agentes de IA e como revisar e implantar perguntas frequentes geradas por IA com o recurso Otimizar no Edge.
feature: Opportunities
source-git-commit: 7f0729839d761ca57236da935c8c7638dd92f32a
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Adicionar perguntas frequentes relevantes

A oportunidade Adicionar perguntas frequentes relevantes identifica páginas de alto tráfego que não têm conteúdo de perguntas e respostas estruturado do qual os agentes de IA geralmente dependem ao gerar respostas. Ela apresenta conteúdo relevante de **perguntas frequentes alinhadas à intenção**, com base no material da sua página atual. Isso ajuda os agentes a fazer a correspondência mais direta das perguntas dos usuários ao seu conteúdo.

Para cada URL afetado, você pode revisar as sugestões de perguntas frequentes geradas pela IA e implantá-las com [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md) para que o tráfego de agente receba um contexto de perguntas e respostas mais claro, sem a necessidade de alterações no Sistema de gerenciamento de conteúdo (CMS).

## Como ele corrige o problema

As correções são aplicadas usando [Otimizar em Edge](/help/dashboards/optimize-at-edge/overview.md), que:

- Disponibiliza um instantâneo pré-renderizado do HTML para agentes de IA.
- Enriquece a página com conteúdo de Perguntas frequentes no HTML que eles recuperam.
- Funciona na camada CDN (sem alterações no CMS).
- É somente IA — sem impacto para visitantes humanos ou bots de SEO.
- Implanta em minutos e é **totalmente reversível** da interface do LLM Optimizer.

## Como funciona

O LLM Optimizer identifica páginas de alto tráfego nas quais o conteúdo de perguntas e respostas está ausente ou fino, com base no conjunto de prompts da sua marca. As URLs afetadas aparecem na tabela **URLs com sugestões** na guia **Sugestões Atuais**, onde você pode expandir uma linha para inspecionar cada recomendação.

![URLs com sugestões sobre Sugestões Atuais, linha expandida com prompts de perguntas frequentes e respostas geradas por IA](/help/dashboards/opportunities/assets/add-relevant-faqs-expand.png)

A tabela **URLs com sugestões** lista páginas em que as perguntas frequentes ajudariam na descoberta orientada por IA. As sugestões estão organizadas em **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Para cada URL é possível:

- **Expanda a linha** para exibir o conteúdo de perguntas frequentes proposto para essa página.
- **Visualize** a comparação anterior e posterior para tráfego de agente.
- **Marque como Corrigido** se você abordou a oportunidade fora da LLM Optimizer.
- **Ignorar** sugestões que não são relevantes.

Cada entrada expandida lista as **perguntas frequentes**, as **respostas sugeridas geradas pela IA**, o breve **raciocínio** e as **fontes** vinculadas à página. A tabela também mostra quantas perguntas frequentes são sugeridas por URL e **tráfego de agente (4 semanas)** para ajudá-lo a priorizar.

Clique em **Visualizar** em uma linha para abrir a visualização da otimização. Ele compara como a sua página procura tráfego de agente agora com a exibição de pós-otimização (por exemplo, o novo bloco **Perguntas frequentes**).

![Visualizar otimizações comparando a exibição do agente de pós-otimização atual com as perguntas frequentes](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-01.png)

Selecione as sugestões de perguntas frequentes que você deseja entregar usando as caixas de seleção de linha. O rodapé mostra quantos estão selecionados e fornece **Marcar como Fixo**, **Ignorar Sugestões** e **Implantar otimizações**.

![Sugestões de Perguntas Frequentes Selecionadas sobre Sugestões Atuais com Otimizações de Implantação](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-02.png)

### Implantar a otimização

Quando estiver pronto para publicar na borda, clique em **Implantar otimizações**. Uma caixa de diálogo **Implantar no Edge** lista as URLs, as perguntas e as respostas que você está prestes a enviar. Revise a lista e escolha **Implantar** ou **Cancelar**.

![Caixa de diálogo Implantar no Edge](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-03.png)

Após uma implantação bem-sucedida, a **Implantação concluída** confirma quantas otimizações ficaram ativas. Feche a caixa de diálogo e abra **Sugestões Corrigidas** para verificar o status.

![Confirmação de conclusão da implantação](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-04.png)

>[!NOTE]
>
>A implantação de otimizações exige a conclusão do processo de integração Otimizar na Edge. Se ainda não tiver integrado, clique em **Implantar otimizações** para direcioná-lo para o processo de integração. Para obter detalhes completos sobre como Otimizar no Edge funciona, provedores de CDN compatíveis e o processo de integração, consulte a página [Otimizar no Edge](/help/dashboards/optimize-at-edge/overview.md).

### Sugestões Fixas e Visualização em Tempo Real

Em **Sugestões Corrigidas**, as URLs implantadas mostram **Otimizado** na coluna de status. Expanda uma linha para revisar o conteúdo de perguntas frequentes ao vivo, use **Detalhes** para análise ou clique em **Exibir em tempo real** para abrir uma exibição somente leitura do **conteúdo da página atual**, conforme fornecido para verificação (incluindo a seção **Perguntas frequentes** inserida).

![Sugestões Corrigidas com Status Otimizado, Exibição em Tempo Real e Reversão](/help/dashboards/opportunities/assets/add-relevant-faqs-fixed.png)

A janela **Exibir em tempo real** mostra a estrutura da página e a cópia das Perguntas frequentes apresentadas nessa verificação.

![Exibir ao Vivo — conteúdo da página atual, incluindo perguntas frequentes](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-05.png)

## Reversão

Se você mudar de ideia, poderá reverter qualquer otimização implantada. No modo de exibição **Sugestões Fixas**, você pode selecionar as linhas otimizadas que deseja reverter e clicar em **Reversão** no cabeçalho.

A caixa de diálogo **Reversão** lista as sugestões que serão revertidas, com um breve aviso de que as otimizações implantadas serão revertidas. Confirme a lista e clique em **Reversão** ou **Cancelar**.

![Caixa de diálogo de reversão listando sugestões para reverter](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-07.png)

Quando a operação for concluída, um resumo **Revertido com Êxito** será exibido; feche-o para retornar ao painel.

![Reversão concluída — Reversão realizada com êxito](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-08.png)

## Experimente na demonstração

Explore o fluxo de trabalho Adicionar perguntas frequentes relevantes na [demonstração do Frescopa](https://play.llmo.now/org/demo-org).
