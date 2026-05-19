---
title: Erros de tráfego agêntico
description: Saiba como o LLM Optimizer detecta erros HTTP encontrados por agentes de IA ao rastrear o site e como corrigi-los para melhorar a acessibilidade do conteúdo e a visibilidade da IA.
feature: Opportunities
autotag-review: '2026-05-15T17:32:31.900Z'
TQID: 'https://experienceleague.adobe.com/9Gbva-14SNt8A0G0B2Qu26OOp34L5NaM0z6lCv4yrTg'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1045
ht-degree: 100%

---


# Erros de tráfego agêntico

Os agentes de IA que rastreiam o site encontram os mesmos erros HTTP que os navegadores humanos, mas as consequências são diferentes. Quando um agente de IA atinge um erro 404, 403 ou 5xx, ele não pode acessar ou citar esse conteúdo, reduzindo diretamente a visibilidade da marca em respostas geradas por IA.

A oportunidade “Erros de tráfego agêntico” monitora os logs da CDN em busca de erros HTTP retornados a agentes de IA e exibe os URLs afetados junto com seus volumes de ocorrência e sugestões de correção. Ele abrange três tipos de erro, cada um com sua própria oportunidade no painel:

- **404 Não encontrado** — Links quebrados que impedem os agentes de IA de acessar conteúdo que não existe mais no URL esperado.
- **403 Proibido** — Restrições de acesso que bloqueiam rastreadores de IA de conteúdos aos quais deveriam conseguir acessar.
- **5xx Server Errors** — Instabilidade do lado do servidor que torna o conteúdo temporariamente ou persistentemente indisponível para os agentes de IA.

Cada tipo de erro pode aparecer como uma oportunidade separada no painel, dependendo dos erros detectados no site.

A oportunidade também exibe duas métricas principais para cada tipo de erro:

- **Total de URLs** — Número de URLs exclusivos que retornam erros para agentes de IA.
- **Total de ocorrências** — Número total de respostas de erro registradas em todas as solicitações do agente de IA.

![Painel de erros de tráfego agêntico mostrando métricas resumidas e detalhes do erro](/help/dashboards/opportunities/assets/agentic-traffic-errors-overview.png)

## Como funciona

O LLM Optimizer consulta os logs da sua CDN via Athena para identificar URLs que retornam códigos de status 404, 403 ou 5xx para agentes de usuário do agente de IA. Os agentes do usuário incluem ChatGPT, Claude, Perplexity e Gemini. Até 500 URLs por auditoria são analisados e classificados por volume de tráfego. A auditoria é executada semanalmente por padrão.

Os URLs são validados antes de serem exibidos para filtrar falsos positivos e dados obsoletos. O LLM Optimizer testa novamente cada URL para confirmar seu status atual e compara as respostas do agente de IA com as respostas do navegador humano para identificar problemas específicos do rastreador.

Para **404 erros**, as sugestões são viabilizadas por IA. Dessa forma, o LLM Optimizer analisa a estrutura e o conteúdo do URL quebrado para recomendar URLs alternativos que preservem a intenção do usuário, juntamente com uma pontuação de confiança e uma explicação lógica da recomendação.

Para os erros **403 e 5xx**, as sugestões são baseadas em modelo, fornecendo orientação direcionada para cada tipo de erro.

## Tabela de detalhes do erro

A tabela de detalhes do erro lista todas os URLs afetados, filtrados por **Agente do usuário**, **Código do país** e **Categoria**. Para cada URL ele mostra:

- **URL** — A página afetada.
- **Total** — Número total de ocorrências de erro dos agentes de IA.
- A contagem de ocorrências semanais nas últimas semanas, para que você possa rastrear se o problema é persistente ou está melhorando.

![Tabela de detalhes do erro com filtros e colunas de ocorrências semanais](/help/dashboards/opportunities/assets/agentic-traffic-errors-table.png)

## Detalhes da sugestão

Clicar em qualquer sugestão abre o painel **Detalhes da sugestão** mostrando:

- O URL afetado e a ação recomendada — por exemplo, &quot;Deve ser um URL válido ou redirecionar para um URL alternativo&quot;.
- Um gráfico **Estatísticas** mostrando o total de ocorrências por semana pelo agente de usuário do agente de IA, para que você possa entender o impacto no tráfego e se o problema é persistente ou está melhorando.
- **Compartilhar** e **Ignorar** ações para gerenciar a sugestão.

![Painel Detalhes da sugestão para erro 404 com gráfico de estatísticas](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion.png)

Em alguns casos do tipo **5xx** (e similares), o painel pode indicar quando não há URLs alternativos disponíveis no mesmo domínio e explicar como as recomendações seguem as regras de domínio e de lista. Por exemplo, sugerir o URL do domínio principal para preservar o valor de SEO quando não for possível oferecer uma combinação mais próxima.

![Painel Detalhes da sugestão para um erro de servidor com mensagens explicativas](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion-503.png)

## Como corrigir

A correção depende do tipo de erro:

**Erros 404** — A sugestão inclui um ou mais URLs alternativos recomendados por IA, com base na estrutura e no conteúdo do URL corrompido, além de uma pontuação de confiança e uma fundamentação. Implemente um redirecionamento do lado do servidor do URL corrompido para a alternativa sugerida para restaurar o acesso ao agente de IA e preservar a capacidade de descoberta do conteúdo.

**Erros 403** — Revise as permissões de acesso para garantir que rastreadores de IA não sejam bloqueados de conteúdos aos quais deveriam ter acesso. Especificamente:
- Revisar permissões de acesso — rastreador de IA bloqueado.
- Verifique se as configurações de segurança não bloqueiam rastreadores legítimos.

**Erros 5xx** — Investigue problemas do lado do servidor que afetam as páginas sinalizadas. Especificamente:
- Investigue a estabilidade do servidor para páginas de alto tráfego.
- Verifique se há erros recorrentes nos logs do aplicativo.
- Monitore a integridade e a capacidade da infraestrutura.

## Experimente na demonstração

Veja a oportunidade Erros de tráfego agêntico em ação usando o ambiente de demonstração Frescopa.

- [Exibir erros 404 na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-4xxs)
- [Exibir erros 5xx na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-5xxs)

## Perguntas frequentes

**Por que os erros HTTP são importantes para a visibilidade da IA?**

Em sistemas de recuperação aumentada, os rastreadores de IA descobrem links e tentam buscar conteúdo da página para inclusão em suas respostas. Se uma página estiver faltando, retornar um erro ou estiver inacessível, seu conteúdo não poderá ser recuperado nem citado. A correção desses erros técnicos melhora diretamente a probabilidade de o conteúdo ser indexado e citado com êxito pelos sistemas de IA.

**Qual é a diferença entre um erro 404 e um 403?**

Um erro 404 significa que a página não existe no URL solicitado — ela foi excluída ou movida sem um redirecionamento. Um erro 403 significa que a página existe, mas o acesso está sendo negado, para todos os rastreadores ou especificamente para agentes de IA. Ambos impedem que os agentes de IA acessem seu conteúdo, mas a correção é diferente para cada um.

**Por que um erro 403 afetaria apenas agentes de IA e não visitantes humanos?**

Algumas configurações de segurança ou de controles de acesso podem bloquear os agentes de usuário do agente de IA contra conteúdos que os visitantes humanos podem acessar normalmente. O LLM Optimizer sinaliza especificamente esses casos comparando as respostas para agentes de IA com as respostas para navegadores usados por pessoas.

**Como os falsos positivos são filtrados?**

O LLM Optimizer testa novamente as URLs para confirmar o status atual delas antes de apresentá-las como sugestões e compara as respostas para agentes de IA com as respostas para navegadores usados por pessoas para identificar problemas específicos de rastreadores. URLs que não retornam mais erros não são mostrados.

**Com que frequência a análise é atualizada?**

Auditorias são executadas semanalmente por padrão, extraindo dados de erro de logs da CDN da semana anterior. A tabela de detalhes do erro mostra contagens de ocorrências semanais para que você possa rastrear tendências ao longo do tempo.

**Quais agentes de IA são monitorados?**

O LLM Optimizer monitora as respostas de erro de todos os padrões de agentes de usuário de agentes de IA detectados, incluindo: rastreadores do ChatGPT, Claude, Perplexity e Gemini.
