---
title: Início rápido
description: Introdução ao Adobe LLM Optimizer - integre sua marca, desbloqueie os insights de visibilidade da IA e explore painéis para aumentar o desempenho da pesquisa.
feature: Quickstart, Onboarding
source-git-commit: c6e37395362262eb5fe8366473e76086e36d77e9
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# Início rápido

Para começar a usar o otimizador do LLM, é necessário concluir o processo de integração conforme detalhado nas etapas abaixo. Após concluir o processo, você terá acesso total aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e a outras funcionalidades.

## Visão geral da integração

O processo de integração começa com a integração do seu domínio. O processo é diferente dependendo se você é cliente da AEM Cloud ou não. Após concluir o processo, será necessário fornecer informações para o Encaminhamento de Logs da CDN e, finalmente, personalizar categorias, tópicos e prompts. Cada parte do processo é detalhada abaixo, juntamente com dicas úteis sobre como começar a usar o LLM Optimizer o mais rápido possível.

## Etapa 1: integrar seu domínio

### Experimente antes de comprar

Os clientes do AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) têm a opção de usar a oferta **Experimentar antes de comprar**. É uma versão de avaliação gratuita do LLM Optimizer com até 200 prompts gratuitos. O uso de mais de 200 prompts requer um contrato de licença separado. O acesso é fornecido no &quot;estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido pela Adobe a qualquer momento.

Alguns recursos do produto não estão disponíveis na versão gratuita:

* A avaliação está limitada a um domínio. Você não poderá alterar o domínio fornecido após concluir a configuração.
* O suporte para implantar otimizações não estará disponível.

Consulte a seção abaixo para obter detalhes sobre como ativar a versão de avaliação gratuita e integrar seu domínio.

### Clientes da AEM Cloud

Se você for um cliente da AEM Cloud, tem a opção de experimentar o LLM Optimizer usando o cartão de Anúncio do Produto no [Experience Hub](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Os prompts adicionados recentemente não aparecerão no [Painel de Presença da Marca](/help/dashboards/brand-presence.md) até que o processamento seja concluído. Os clientes da AEM Cloud podem usar a versão de avaliação gratuita do LLM Optimizer. O uso de mais de 200 prompts requer um contrato de licença separado. O acesso é fornecido no &quot;estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido pela Adobe a qualquer momento. Entre em contato com o seu representante de conta para obter mais informações.

![Avaliação do LLM Optimizer](/help/overview/assets/llm-trial.png)

Depois de clicar no botão **Tentar LLM Optimizer**, você será redirecionado para [https://llmo.now](https://llmo.now). Em seguida, será necessário fazer logon via IMS. Depois de fazer logon, você iniciará o processo de integração fornecendo um domínio e o nome da marca.

![Domínio do LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>O domínio fornecido será usado por todos da organização e não poderá ser alterado.

Para acionar a Análise de presença da marca, será necessário fornecer categorias, tópicos e prompts.

![Análise de presença de marca](/help/overview/assets/bp-analysis.png)

Além disso, também é necessário configurar o [encaminhamento de logs da CDN](#step-4) para análise de tráfego. O LLM Optimizer exige dados e insights de presença da marca do tráfego de referência e de agente para identificar oportunidades e fornecer recomendações prescritivas a fim de aumentar a visibilidade da IA.

### Clientes da nuvem que não são da AEM

Depois que o contrato comercial for finalizado, você será integrado ao domínio que deseja integrar no LLM Optimizer. Após concluir esta integração, você poderá fazer logon no LLM Optimizer via [https://llmo.now](https://llmo.now).

### Etapa 2: Personalizar categorias, tópicos e prompts

Para acionar a análise de Presença da marca e preencher o painel com insights sobre a visibilidade da marca, é necessário personalizar Categorias, Tópicos e Avisos. Esta configuração foi criada no [painel de configuração do cliente](/help/dashboards/customer-configuration.md).

![Painel de configuração do cliente](/help/overview/assets/prompt-creation.png)

Nesse painel, é possível:

* Adicione **novas categorias** alinhadas às suas prioridades comerciais. As categorias podem ser amplas áreas de conteúdo relevantes para o seu domínio.
* Insira **tópicos personalizados** ou subtópicos que você deseja rastrear. Tópicos podem ser temas específicos vinculados a palavras-chave sem marca de alto volume associadas ao seu domínio.
* Crie **seus prompts** para monitorar a visibilidade em consultas específicas. Os prompts são consultas (com e sem marca) que fornecem uma visibilidade da linha de base. Somente um número limitado de prompts será gerado automaticamente com base nas categorias e tópicos fornecidos.
* Defina a menção **aliases** para garantir que todas as menções de uma marca sejam capturadas e contabilizadas.
* Defina **outros aliases** para rastrear outras marcas com precisão.

>[!NOTE]
>Os prompts exatos que você solicita aos LLMs não estão disponíveis publicamente, pois não são divulgados pelos LLMs.

>[!NOTE]
>
> Para obter mais detalhes sobre como configurar suas categorias, tópicos, prompts, consulte a página [Práticas recomendadas para configurar categorias, tópicos, prompts](/help/overview/best-practices-topics-prompts.md).

### Etapa 3: pré-preenchimento automático de insights

Depois que o domínio for integrado e você tiver fornecido categorias e tópicos, a LLM Optimizer acionará automaticamente a análise de Presença da marca.

### Etapa 4: fornecer informações para encaminhamento de log CDN {#step-4}

Para desbloquear os insights de Tráfego de agente e Tráfego de referência, é necessário fornecer informações para o encaminhamento de log CDN. Ele pode ser adicionado a partir do [painel de configuração do cliente](/help/dashboards/customer-configuration.md#cdn-configuration) navegando até a guia **Configuração de CDN** e clicando em **CDN integrada**.

![CDN de Configuração de Cliente](/help/overview/assets/cc-cdn.png)

Como alternativa, se nenhum provedor de CDN tiver sido adicionado anteriormente (conforme descrito acima), você será solicitado a adicionar o encaminhamento de log de CDN ao acessar os painéis de Controle de tráfego de Referência e de Agente pela primeira vez. Para obter mais detalhes, consulte:

* [Tráfego de agente](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfego de referência](/help/dashboards/referral-traffic.md#setup#setup)

### Etapa 5: Explorar painéis e agir

Depois de fornecer informações sobre o Encaminhamento de Logs CDN, você poderá:

* Exiba o painel [Presença da Marca](/help/dashboards/brand-presence.md) e exiba sua pontuação de visibilidade e controle seu desempenho em relação a outras marcas.
* Explore os painéis de [Tráfego de Referência](/help/dashboards/agentic-traffic.md) e [Tráfego de Referência](/help/dashboards/referral-traffic.md) se o encaminhamento de log de CDN tiver sido configurado.
* Use as [Oportunidades](/help/dashboards/opportunities.md) para identificar melhorias técnicas e de conteúdo.
* Exporte dados e colabore com sua equipe ou convide seu colega de trabalho para usar o produto.

Por fim, para entender totalmente os recursos do LLM Optimizer, você deve explorar todos os [painéis](/help/dashboards/dashboards-overview.md) disponíveis.
