---
title: Tráfego bloqueado por robots.txt
description: Saiba como o LLM Optimizer detecta quando seu arquivo robots.txt está bloqueando o acesso de agentes de IA ao seu conteúdo e como corrigi-lo.
feature: Opportunities
source-git-commit: fa8b994aa55869cf7f2607e792acc4e8abc213e7
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 1%

---


# Tráfego bloqueado por robots.txt

Seu arquivo `robots.txt` controla quais rastreadores podem acessar seu site. Quando os agentes de IA são seletivamente bloqueados de um conteúdo que, de outra forma, seria acessível aos rastreadores gerais, eles não podem indexar ou citar esse conteúdo, reduzindo diretamente a visibilidade da sua marca em respostas geradas por IA.

A oportunidade Tráfego bloqueado por robots.txt analisa seu arquivo `robots.txt` em relação às páginas principais e identifica regras que estão impedindo os agentes de IA de acessar o conteúdo que eles devem conseguir. Ele exibe os resultados no nível de linha `robots.txt` individual para que você possa revisar e atualizar diretivas específicas em vez de auditar todo o arquivo manualmente.

Ele apresenta duas métricas principais rapidamente:

- **Total de URLs** — Número de URLs afetadas pelas regras de bloqueio em seu `robots.txt`.
- **Agentes bloqueados** — Número de agentes de IA sendo impedidos de acessar essas URLs.

![Tráfego bloqueado pelo painel robots.txt](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-overview.png)

## Como funciona

A LLM Optimizer busca o arquivo `robots.txt` e verifica as páginas principais em relação a seis agentes de usuário principais do agente de IA:

- ClaudeBot
- GPTBot
- OAI-SearchBot
- Usuário do OAI
- PerplexityBot
- Perplexidade-Usuário

Uma URL só é sinalizada quando é **permitida para o agente de usuário curinga (`*`), mas não para um agente de IA específico**. O bloqueio geral — em que todos os rastreadores são igualmente restritos — não é relatado. A auditoria visa especificamente a exclusão seletiva do agente de IA, que representa a conclusão mais acionável para a GEO.

>[!NOTE]
>Essa oportunidade não usa IA para desenvolver ou fornecer sugestões. As descobertas são baseadas inteiramente na análise direta de seu arquivo `robots.txt`.

Os resultados são exibidos em duas guias: **robots.txt** e **Detalhes de Tráfego Bloqueado pelo Agente**.

## robots.txt

Esta guia exibe o arquivo `robots.txt` completo com diretivas de bloqueio realçadas em vermelho. Cada linha destacada representa uma regra que está bloqueando seletivamente um ou mais agentes de IA de acessar um URL que, de outra forma, estaria acessível publicamente.

Exibição ![robots.txt com diretivas de bloqueio realçadas](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-robotstxt.png)

Clicar em uma diretiva destacada mostra mais informações sobre seu impacto e a correção sugerida.

## Detalhes do tráfego bloqueado por agente

Esta guia fornece um detalhamento do tráfego bloqueado organizado pelo agente de IA. Para cada agente bloqueado, ele mostra:

- **Descrição do Problema** — Uma explicação de qual agente está sendo bloqueado e por que ele é importante.
- **Solução** — Orientação para abrir o arquivo `robots.txt` e revisar o número de linha específico listado ao lado de cada URL afetada.
- Uma tabela de URLs afetadas com a **Linha**, **Classificação** e **URL** para cada página bloqueada.

Cada agente (por exemplo, OAI-User, GPTBot, OAI-SearchBot) tem sua própria subguia para que você possa endereçar blocos por agente.

## Como corrigir

Para resolver uma descoberta de agente bloqueado, abra o arquivo `robots.txt` e localize o número da linha mostrado ao lado de cada URL afetada na guia Detalhes do Tráfego Bloqueado pelo Agente. Atualize ou remova a diretiva de não permissão para o agente de IA relevante para permitir acesso ao URL afetado.

Por exemplo, para desbloquear GPTBot de uma página específica, remova ou atualize a diretiva:

```
User-agent: GPTBot
Disallow: /blog/cold-brewing-101
```

Assim que o arquivo `robots.txt` for atualizado e republicado, o LLM Optimizer detectará a alteração na próxima execução de auditoria e marcará a sugestão como resolvida.

## Experimente na demonstração

Veja a oportunidade Tráfego bloqueado por robots.txt em ação usando o ambiente de demonstração Frescopa.

[Exibir o tráfego bloqueado por robots.txt na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/blocked-urls-llm-agents)

## Perguntas frequentes

**Por que o bloqueio de agentes de IA é importante para a GEO?**

A Otimização do mecanismo gerador exige que os rastreadores de IA possam acessar e indexar o conteúdo do site. O bloqueio dos agentes de IA impede diretamente que suas páginas apareçam em respostas geradas por IA, reduzindo citações, menções de marca e a visibilidade geral da IA. Mesmo uma única página de alto tráfego bloqueada pode representar uma perda significativa de exposição da marca orientada por IA.

**Qual é a diferença entre o bloqueio geral e o bloqueio seletivo?**

O bloqueio de coberturas significa que todos os rastreadores, incluindo rastreadores gerais da Web, são restritos de uma página. O bloqueio seletivo significa que rastreadores gerais podem acessar a página, mas agentes de IA específicos não podem. Essa oportunidade sinaliza apenas o bloqueio seletivo porque representa uma exclusão intencional ou acidental dos agentes de IA do conteúdo que, de outra forma, seria público, o que é a conclusão mais acionável.

**Quais agentes de IA o LLM Optimizer verifica?**

O LLM Optimizer verifica ClaudeBot, GPTBot, OAI-SearchBot, OAI-User, PerplexityBot e Perplexity-User.

**E se eu intencionalmente desejar bloquear determinados agentes de IA?**

Você pode revisar cada diretiva sinalizada e escolher manter o bloco intencionalmente. As sugestões descartadas são preservadas nas execuções de auditoria e não serão exibidas novamente, a menos que o arquivo `robots.txt` seja alterado e a regra reapareça.

**Como o LLM Optimizer rastreia as alterações no meu arquivo robots.txt ao longo do tempo?**

O LLM Optimizer usa hash para rastrear o conteúdo do `robots.txt` em execuções. Se uma regra de bloqueio resolvida anteriormente reaparecer — por exemplo, após uma atualização de `robots.txt` — ela será exibida novamente como uma nova sugestão.

**Como as páginas principais são determinadas?**

As páginas são provenientes de uma combinação de suas páginas de SEO de tráfego mais alto, URLs principais visitados pelo agente de IA de logs CDN e URLs personalizados especificados na configuração do site.
