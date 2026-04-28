---
title: Erros de tráfego de agente
description: Saiba como o LLM Optimizer detecta erros HTTP encontrados por agentes de IA que rastream do site e como corrigi-los para melhorar a acessibilidade do conteúdo e a visibilidade da IA.
feature: Opportunities
source-git-commit: 101a0582a5112c7fdf1871a938b773b7159a9d4c
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Erros de tráfego de agente

Os agentes de IA que rastream do site encontram os mesmos erros HTTP que os navegadores humanos, mas as consequências são diferentes. Quando um agente de IA atinge um erro 404, 403 ou 5xx, ele não pode acessar ou citar esse conteúdo, reduzindo diretamente a visibilidade da sua marca em respostas geradas por IA.

A oportunidade Erros de tráfego de agente monitora os registros CDN em busca de erros HTTP retornados aos agentes de IA e exibe os URLs afetados junto com seus volumes de ocorrência e sugestões de correção. Ele abrange três tipos de erro, cada um com sua própria oportunidade no painel:

- **404 Não encontrado** — Links quebrados que impedem os agentes de IA de acessar conteúdo que não existe mais na URL esperada.
- **403 Proibido** — Restrições de acesso que bloqueiam os rastreadores de IA do conteúdo que eles devem conseguir alcançar.
- **5xx Server Errors** — Instabilidade do lado do servidor que torna o conteúdo temporariamente ou persistentemente indisponível para os agentes de IA.

Cada tipo de erro pode aparecer como uma oportunidade separada no painel, dependendo dos erros detectados no site.

A oportunidade também exibe duas métricas principais para cada tipo de erro:

- **Total de URLs** — Número de URLs exclusivas que retornam erros para agentes de IA.
- **Total de ocorrências** — Número total de respostas de erro registradas em todas as solicitações do agente de IA.

![Painel de Erros de Tráfego de Agente mostrando métricas resumidas e detalhes do erro](/help/dashboards/opportunities/assets/agentic-traffic-errors-overview.png)

## Como funciona

A LLM Optimizer consulta seus registros de CDN por meio do Athena para identificar URLs que retornam códigos de status 404, 403 ou 5xx para agentes de usuário do agente de IA. Os agentes do usuário incluem ChatGPT, Claude, Perplexity e Gemini. Até 500 URLs por auditoria são analisados e classificados por volume de tráfego. A auditoria é executada semanalmente por padrão.

Os URLs são validados antes de serem exibidos para filtrar falsos positivos e dados obsoletos. O LLM Optimizer testa novamente cada URL para confirmar seu status atual e compara as respostas do agente de IA com as respostas do navegador humano para identificar problemas específicos do rastreador.

Para **404 erros**, as sugestões são alimentadas por IA. Dessa forma, o LLM Optimizer analisa a estrutura e o conteúdo do URL quebrado para recomendar URLs alternativos que preservem a intenção do usuário, juntamente com uma pontuação de confiança e uma explicação lógica da recomendação.

Para os erros **403 e 5xx**, as sugestões são baseadas em modelo, fornecendo orientação direcionada para cada tipo de erro.

## Tabela de detalhes do erro

A tabela de detalhes do erro lista todas as URLs afetadas, filtradas por **Agente do Usuário**, **Código do País** e **Categoria**. Para cada URL ele mostra:

- **URL** — A página afetada.
- **Total** — Número total de ocorrências de erro dos agentes de IA.
- A contagem de ocorrências semanais nas últimas semanas, para que você possa rastrear se o problema é persistente ou está melhorando.

![Tabela de detalhes do erro com filtros e colunas de ocorrências semanais](/help/dashboards/opportunities/assets/agentic-traffic-errors-table.png)

## Detalhes da sugestão

Clicar em qualquer sugestão abre um painel **Detalhes da Sugestão** mostrando:

- O URL afetado e a ação recomendada — por exemplo, &quot;Deve ser um URL válido ou redirecionar para um URL alternativo&quot;.
- Um gráfico **Estatísticas** mostrando o total de ocorrências por semana pelo agente de usuário do agente de IA, para que você possa entender o impacto no tráfego e se o problema é persistente ou está melhorando.
- **Compartilhar** e **Ignorar** ações para gerenciar a sugestão.

![Painel Detalhes da Sugestão para um 404 com gráfico de estatísticas](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion.png)

Para alguns casos de **5xx** (e semelhantes), o painel pode observar quando não houver URLs alternativas de mesmo domínio disponíveis e explicar como as recomendações seguem o domínio e as regras da lista. Por exemplo, sugerir o URL do domínio base para preservar o valor SEO quando uma correspondência mais próxima não puder ser oferecida.

![Painel Detalhes da Sugestão para um erro de servidor com mensagens explicativas](/help/dashboards/opportunities/assets/agentic-traffic-errors-suggestion-503.png)

## Como corrigir

A correção depende do tipo de erro:

**404 erros** — A sugestão inclui uma ou mais URLs alternativas recomendadas pela IA, com base na estrutura e no conteúdo da URL corrompida, além de uma pontuação de confiança e uma fundamentação. Implemente um redirecionamento do lado do servidor do URL corrompido para a alternativa sugerida para restaurar o acesso ao agente de IA e preservar a capacidade de descoberta do conteúdo.

**403 erros** — Revise as permissões de acesso para garantir que os rastreadores de IA não estejam bloqueados no conteúdo que eles deveriam poder acessar. Especificamente:
- Revisar permissões de acesso — rastreador de IA bloqueado.
- Verifique se as configurações de segurança não bloqueiam rastreadores legítimos.

**5xx errors** — Investigue problemas do lado do servidor que afetam as páginas sinalizadas. Especificamente:
- Investigue a estabilidade do servidor para páginas de alto tráfego.
- Verifique nos logs do aplicativo se há erros recorrentes.
- Monitore a integridade e a capacidade da infraestrutura.

## Experimente na demonstração

Veja a oportunidade Erros de tráfego de agente em ação usando o ambiente de demonstração Frescopa.

- [Exibir erros 404 na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-4xxs)
- [Exibir erros 5xx na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/agentic-traffic-5xxs)

## Perguntas frequentes

**Por que os erros HTTP são importantes para a visibilidade da IA?**

Em sistemas de recuperação aumentada, os rastreadores de IA descobrem links e tentam buscar conteúdo da página para inclusão em suas respostas. Se uma página estiver ausente, retornar um erro ou estiver inacessível, seu conteúdo não poderá ser recuperado ou citado. A correção desses erros técnicos melhora diretamente a probabilidade de o conteúdo ser indexado e citado com êxito pelos sistemas de IA.

**Qual é a diferença entre um erro 404 e um 403?**

Um erro 404 significa que a página não existe no URL solicitado — ela foi excluída ou movida sem um redirecionamento. Um erro 403 significa que a página existe, mas o acesso está sendo negado, para todos os rastreadores ou especificamente para agentes de IA. Ambos impedem que os agentes de IA acessem seu conteúdo, mas a correção é diferente para cada um.

**Por que um erro 403 pode afetar apenas os agentes de IA e não os visitantes humanos?**

Algumas configurações de segurança ou de controle de acesso podem bloquear os agentes de usuário do agente de IA contra conteúdos que os visitantes humanos podem acessar normalmente. O LLM Optimizer sinaliza especificamente esses casos comparando as respostas do agente de IA com as respostas humanas do navegador.

**Como os falsos positivos são filtrados?**

O LLM Optimizer testa novamente os URLs para confirmar seu status atual antes de exibi-los como sugestões e compara as respostas do agente de IA com as respostas humanas do navegador para identificar problemas específicos do rastreador. Os URLs que não retornam mais erros não são mostrados.

**Com que frequência a análise é atualizada?**

A auditoria é executada semanalmente por padrão, extraindo dados de erro dos logs CDN da semana anterior. A tabela de detalhes do erro mostra contagens de ocorrências semanais para que você possa rastrear tendências ao longo do tempo.

**Quais agentes de IA são monitorados?**

O LLM Optimizer monitora as respostas de erro de todos os padrões de agente de usuário de IA detectados, incluindo: rastreadores ChatGPT, Claude, Perplexity e Gemini.
