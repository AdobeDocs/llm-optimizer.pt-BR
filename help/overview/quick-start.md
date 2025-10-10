---
title: Início rápido
description: Introdução ao Adobe LLM Optimizer - integre sua marca, desbloqueie os insights de visibilidade da IA e explore painéis para aumentar o desempenho da pesquisa.
source-git-commit: db42183c922e6156a890e4e56732f348c26e7e44
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Início rápido

Para começar a usar o otimizador do LLM, você precisa passar pelo processo de integração. Depois disso, você terá acesso total aos painéis e às funcionalidades completas do LLM Optimizer.

## Visão geral da integração

O processo de integração começa com a integração do seu domínio. O processo é diferente dependendo se você é um cliente da AEM Cloud ou não. Após concluir o processo, será necessário fornecer informações para o Encaminhamento de Logs da CDN e, finalmente, personalizar categorias, tópicos e prompts.

### Etapa 1: integrar seu domínio

### Clientes da AEM Cloud

Os Clientes da AEM Cloud (Cloud Service/Managed Services/ Edge Delivery Service) verão a opção de experimentar o LLM Optimizer através do cartão de Anúncio do Produto no [Experience Hub](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Os prompts adicionados recentemente não aparecerão na Presença da Marca até que o processamento seja concluído. Os clientes da AEM Cloud (Cloud Service, Managed Services/Edge Delivery Service) podem usar a versão de avaliação gratuita do LLM Optimizer. O uso de mais de 200 prompts requer um contrato de licença separado. O acesso é fornecido no &quot;estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido pela Adobe a qualquer momento. Entre em contato com o seu [representante de conta] para obter mais informações.

![Avaliação do LLM Optimizer](/help/overview/assets/llm-trial.png)

Depois de clicar no botão **Tentar LLM Optimizer**, você será redirecionado para [https://llmo.now](https://llmo.now). Em seguida, será necessário fazer logon via IMS. Depois de fazer logon, você iniciará o processo de integração fornecendo um domínio e o nome da marca.

![Domínio do LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>O domínio fornecido será usado por todos em sua organização e não poderá ser alterado.

Para acionar a Análise de presença da marca, será necessário fornecer categorias, tópicos e prompts.

![Análise de presença de marca](/help/overview/assets/bp-analysis.png)

Além disso, também é necessário configurar o encaminhamento de logs CDN para análise de tráfego. O LLM Optimizer exige dados e insights de presença da marca do tráfego de referência e de agente para identificar oportunidades e fornecer recomendações prescritivas para ajudar os clientes a aumentar a visibilidade da IA.

### Clientes da nuvem que não são da AEM

Após assinar o contrato, você será integrado por meio do comando slackbot com o domínio que deseja integrar no LLM Optimizer. Após concluir esta integração, você poderá fazer logon no LLM Optimizer via [https://llmo.now](https://llmo.now).

### Etapa 2: pré-preenchimento automático de insights

Depois que o domínio for integrado, o LLM Optimizer preencherá automaticamente o seguinte:

* **Categorias** - Amplas áreas de conteúdo relevantes para o seu domínio.
* **Tópicos** - Temas específicos vinculados a palavras-chave sem marca de alto volume associadas ao seu domínio.
* **Prompts** - Consultas (com e sem marca) para fornecer visibilidade da linha de base.

Isso garante que, mesmo antes de adicionar suas configurações e entradas personalizadas, você veja os insights iniciais sobre a visibilidade da sua marca.

### Etapa 3: Personalizar categorias, tópicos e prompts

Clique no [painel de configuração do cliente](/help/dashboards/customer-configuration.md) para começar a personalizar suas Categorias, Tópicos e Avisos.

![Painel de configuração do cliente](/help/dashboards/assets/customer-config.png)

Nesse painel, é possível:

* Adicione novas categorias que se alinhem às suas prioridades comerciais.
* Insira tópicos ou subtópicos personalizados que precisam ser rastreados.
* Crie seus prompts para monitorar a visibilidade em consultas específicas.
* Defina aliases de menção para que todas as menções sejam capturadas.
* Defina aliases de concorrentes para rastrear os concorrentes com precisão.

### Etapa 4: fornecer informações para encaminhamento de log CDN

Para desbloquear os insights de Tráfego de agente e Tráfego de referência, é necessário fornecer informações para o encaminhamento de log CDN. Consulte cada página específica para obter mais detalhes sobre como configurar o encaminhamento de log:

* [Tráfego de agente](/help/dashboards/agentic-traffic.md)
* [Tráfego de referência](/help/dashboards/referral-traffic.md#setup#cdn-setup)

### Etapa 5: Explorar painéis e agir

Depois de fornecer informações sobre o Encaminhamento de Logs CDN, você poderá:

* Exiba o painel [Presença da Marca](/help/dashboards/brand-presence.md), exiba sua pontuação de visibilidade e controle seu desempenho em relação aos seus concorrentes.
* Explore os painéis de [Tráfego de referência](/help/dashboards/agentic-traffic.md) e [Tráfego de referência](/help/dashboards/referral-traffic.md).
* Use as [Oportunidades](/help/dashboards/opportunities.md) para identificar melhorias técnicas e de conteúdo.
* Exporte dados e colabore com sua equipe ou convide seu colega de trabalho para usar o produto.

Para entender totalmente os recursos do otimizador de LLM, explore todos os [painéis](/help/dashboards/dashboards-overview.md) disponíveis.
