---
title: Tráfego bloqueado pelo robots.txt
description: Aprenda como o LLM Optimizer detecta quando o arquivo robots.txt está bloqueando o acesso de agentes de IA ao seu conteúdo e como corrigir isso.
feature: Opportunities
autotag-review: '2026-05-15T18:00:25.453Z'
TQID: 'https://experienceleague.adobe.com/9LGbxeIbWYZp-MN5Zww6g-dQ6BZT0IWzlA7XB-2Xlho'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 817
ht-degree: 100%

---


# Tráfego bloqueado pelo robots.txt

Seu arquivo `robots.txt` controla quais rastreadores podem acessar seu site. Quando os agentes de IA são bloqueados seletivamente em conteúdos que, de outra forma, seriam acessíveis a rastreadores em geral, esses agentes não podem indexar ou citar esse conteúdo diretamente, reduzindo a visibilidade da sua marca nas respostas geradas por IA.

A oportunidade “Tráfego bloqueado por robots.txt” analisa seu arquivo `robots.txt` em relação às suas páginas principais e identifica regras que estão impedindo os agentes de IA de acessar conteúdo que deveriam ser capazes de acessar. Ela exibe as descobertas no nível da linha individual `robots.txt` para que você possa revisar e atualizar diretivas específicas em vez de auditar o arquivo inteiro manualmente.

Ela apresenta rapidamente duas métricas principais:

- **Total de URLs** — Número de URLs afetados por regras de bloqueio em seu `robots.txt`.
- **Agentes bloqueados** — Número de agentes de IA impedidos de acessar esses URLs.

![Tráfego bloqueado pelo painel do robots.txt](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-overview.png)

## Como funciona

O LLM Optimizer busca seu arquivo `robots.txt` e verifica suas páginas principais em relação a seis dos principais agentes de usuário de IA:

- ClaudeBot
- GPTBot
- OAI-SearchBot
- OAI-User
- PerplexityBot
- Perplexity-User

Um URL só é sinalizado quando é **permitido para o agente de usuário curinga (`*`), mas impedido para um agente de IA específico**. O bloqueio geral — em que todos os rastreadores são igualmente restringidos — não é relatado. A auditoria tem como alvo especificamente a exclusão seletiva de agentes de IA, que representa a descoberta mais acionável para GEO.

>[!NOTE]
>Esta oportunidade não utiliza IA para desenvolver ou fornecer sugestões. Os resultados são baseados inteiramente na análise direta do seu arquivo `robots.txt`.

Os resultados são exibidos em duas guias:**robots.txt** e **Detalhes do tráfego bloqueado por agente**.

## robots.txt

Esta aba exibe seu arquivo `robots.txt` completo com as diretivas de bloqueio destacadas em vermelho. Cada linha destacada representa uma regra que bloqueia seletivamente um ou mais agentes de IA de acessar um URL que, de outra forma, seria publicamente acessível.

![Exibição do arquivo robots.txt com as diretivas de bloqueio destacadas](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-robotstxt.png)

Clicar em uma diretiva destacada exibe mais informações sobre seu impacto e a correção sugerida.

## Detalhes do tráfego bloqueado por agente

Esta aba fornece um detalhamento do tráfego bloqueado, organizado por agente de IA. Para cada agente bloqueado, é exibido:

- **Descrição do problema** — Uma explicação de qual agente está sendo bloqueado e por que isso é importante.
- **Resolução** — Orientações para abrir o arquivo `robots.txt` e revisar o número da linha específica listada ao lado de cada URL afetado.
- Uma tabela de URLs afetados com a **Linha**, **Classificação** e **URL** para cada página bloqueada.

Cada agente (por exemplo, OAI-User, GPTBot, OAI-SearchBot) possui sua própria subguia para que você possa tratar os bloqueios por agente.

## Como corrigir

Para resolver um problema de bloqueio de agente, abra o arquivo `robots.txt` e localize o número da linha exibido ao lado de cada URL afetado na guia Detalhes de tráfego bloqueado por agente. Atualize ou remova a diretiva de bloqueio para o agente de IA relevante a fim de permitir o acesso ao URL afetado.

Por exemplo, para desbloquear o GPTBot em uma página específica, remova ou atualize a diretiva:

```
User-agent: GPTBot
Disallow: /blog/cold-brewing-101
```

Assim que o seu arquivo `robots.txt` for atualizado e republicado, o LLM Optimizer detectará a alteração na próxima execução de auditoria e marcará a sugestão como resolvida.

## Experimente na demonstração

Visualize a oportunidade Tráfego bloqueado por robots.txt em ação usando o ambiente de demonstração do Frescopa.

[Visualizar Tráfego bloqueado por robots.txt na demonstração do Frescopa](https://play.llmo.now/org/demo-org/opportunities/blocked-urls-llm-agents)

## Perguntas frequentes

**Por que bloquear agentes de IA é importante para GEO?**

A Generative Engine Optimization (GEO) exige que os rastreadores de IA possam acessar e indexar o conteúdo do seu site. Bloquear agentes de IA diretamente impede que suas páginas apareçam em respostas geradas por IA, reduzindo citações, menções à marca e a visibilidade geral da IA. Mesmo o bloqueio de uma única página de alto tráfego pode representar uma perda significativa de exposição da marca impulsionada por IA.

**Qual a diferença entre bloqueio total e bloqueio seletivo?**

O bloqueio total significa que todos os rastreadores — incluindo os rastreadores da web em geral — estão impedidos de acessar uma página. O bloqueio seletivo significa que os rastreadores em geral podem acessar a página, mas agentes de IA específicos não podem. Essa oportunidade apenas sinaliza o bloqueio seletivo porque representa uma exclusão intencional ou acidental de agentes de IA de conteúdo que, de outra forma, seria público, o que constitui a descoberta mais acionável.

**Quais agentes de IA o LLM Optimizer verifica?**

O LLM Optimizer realiza verificações em relação ao ClaudeBot, GPTBot, OAI-SearchBot, OAI-User, PerplexityBot e Perplexity-User.

**E se eu quiser bloquear intencionalmente certos agentes de IA?**

Você pode revisar cada diretiva sinalizada e optar por manter o bloqueio intencionalmente. As sugestões rejeitadas são preservadas entre as execuções de auditoria e não serão reapresentadas a menos que o arquivo `robots.txt` seja alterado e a regra reapareça.

**Como o LLM Optimizer acompanha as alterações no meu robots.txt ao longo do tempo?**

O LLM Optimizer usa hashing para rastrear seu conteúdo `robots.txt` entre as execuções. Se uma regra de bloqueio previamente resolvida reaparecer — por exemplo, após uma atualização `robots.txt` — ela será reapresentada como uma nova sugestão.

**Como são determinadas as páginas principais?**

As páginas são obtidas a partir de uma combinação das suas páginas de SEO com maior tráfego, URLs mais visitados pelo agente de IA nos logs da CDN e quaisquer URLs personalizados especificados na configuração do site.
