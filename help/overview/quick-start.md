---
title: Início rápido
description: Introdução ao Adobe LLM Optimizer - integre sua marca, desbloqueie os insights de visibilidade da IA e explore painéis para aumentar o desempenho da pesquisa.
feature: Quickstart, Onboarding
source-git-commit: 24183fbe2577bb9402f8b6aaaf1e46c75403383d
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---


# Início rápido

Para começar a usar o otimizador do LLM, é necessário concluir o processo de integração conforme detalhado nas etapas abaixo. Após concluir o processo, você terá acesso total aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e a outras funcionalidades.

## Visão geral da integração

O processo de integração começa com a integração do seu domínio. O processo é diferente dependendo se você é cliente da AEM Cloud ou não. Após concluir o processo, será necessário fornecer informações para o Encaminhamento de Logs da CDN e, finalmente, personalizar categorias, tópicos e prompts. Cada parte do processo é detalhada abaixo, juntamente com dicas úteis sobre como começar a usar o LLM Optimizer o mais rápido possível.

### Permitir que o Adobe LLM Optimizer acesse páginas públicas

Para fornecer conteúdo preciso e recomendações técnicas, o Adobe LLM Optimizer requer acesso às suas páginas direcionadas ao público. Isso é feito por meio de um rastreador interno seguro (agente do usuário Spacecat/1.0).

Requisitos de configuração:

* Adicione o agente de usuário Spacecat/1.0 ao Incluo na lista de permissões robots.txt do site ou nas regras de gerenciamento de tráfego de bot
* Certifique-se de que as páginas não estejam bloqueadas no nível de domínio ou CDN. Páginas bloqueadas não podem ser indexadas, o que significa que tarefas de otimização e insights não podem ser gerados para elas.

Se a visibilidade do conteúdo parecer baixa no painel, verifique se o rastreador tem acesso aos seus domínios. O acesso restrito é uma causa comum de indexação incompleta.

## Etapa 1: integrar seu domínio

### Experimente antes de comprar

Os clientes do AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) têm a opção de usar a oferta **Experimentar antes de comprar**. É uma versão de avaliação gratuita do LLM Optimizer com até 200 prompts gratuitos. O uso de mais de 200 prompts requer um contrato de licença separado. O acesso é fornecido no &quot;estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido pela Adobe a qualquer momento.

Alguns recursos do produto não estão disponíveis na versão gratuita:

* A avaliação está limitada a um domínio. Você não poderá alterar o domínio fornecido após concluir a configuração.
* O suporte para implantar otimizações não estará disponível.

Consulte a seção abaixo para obter detalhes sobre como ativar a versão de avaliação gratuita e integrar seu domínio.

### Clientes da AEM Cloud

Se você for um cliente da AEM Cloud, tem a opção de experimentar o LLM Optimizer usando o cartão de Anúncio do Produto no [Experience Hub](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Prompts adicionados recentemente não aparecerão no [Painel de Presenças da marca](/help/dashboards/brand-presence.md) até que o processamento seja concluído. Os clientes da AEM Cloud podem usar a versão de avaliação gratuita do LLM Optimizer. O uso de mais de 200 prompts requer um contrato de licença separado. O acesso é fornecido no &quot;estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido pela Adobe a qualquer momento. Entre em contato com o seu representante de conta para obter mais informações.

![Avaliação do LLM Optimizer](/help/overview/assets/llm-trial.png)

Depois de clicar no botão **Tentar LLM Optimizer**, você será redirecionado para [https://llmo.now](https://llmo.now). Em seguida, será necessário fazer logon via IMS. Depois de fazer logon, você iniciará o processo de integração fornecendo um domínio e o nome da marca.

![Domínio do LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>O domínio fornecido será usado por todos da organização e não poderá ser alterado.

Um pequeno conjunto de categorias, tópicos e prompts será gerado durante a fase de integração. A análise de Presença da marca nessas solicitações estará disponível logo após a integração do site.

<!--![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)-->

Além disso, também é necessário configurar o [encaminhamento de logs da CDN](#step-4) para análise de tráfego. O LLM Optimizer exige dados e insights de Presença da marca do agente e do tráfego de referência para identificar oportunidades e fornecer recomendações prescritivas a fim de aumentar a visibilidade da IA.

### Clientes da nuvem que não são da AEM

Depois que o contrato comercial for finalizado, você será integrado ao domínio que deseja integrar no LLM Optimizer. Após concluir esta integração, você poderá fazer logon no LLM Optimizer via [https://llmo.now](https://llmo.now).

### Etapa 2: Personalizar categorias, tópicos e prompts

Depois que o site for integrado, você poderá exibir a Análise de Presença da marca com base no pequeno conjunto de prompts que foram gerados automaticamente durante a fase de integração. Agora é possível personalizar as categorias, os tópicos e os prompts da sua marca. Esta configuração foi criada no [painel de configuração do cliente](/help/dashboards/customer-configuration.md).

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

### Etapa 3: Presença da marca Insights

Após a integração do seu domínio, você verá os insights iniciais na exibição do Presença da marca com base nos prompts que foram gerados automaticamente durante a integração. Depois de personalizar suas próprias categorias, tópicos e prompts, o LLM Optimizer acionará automaticamente a análise de Presença da marca nos prompts fornecidos e os resultados estarão disponíveis em 24 horas.

### Etapa 4: fornecer informações para encaminhamento de log CDN {#step-4}

Para desbloquear insights de tráfego e Tráfegos de referência do Agentic, é necessário fornecer informações para o encaminhamento de logs CDN. Ele pode ser adicionado a partir do [painel de configuração do cliente](/help/dashboards/customer-configuration.md#cdn-configuration) navegando até a guia **Configuração de CDN** e clicando em **CDN integrada**.

![CDN de Configuração de Cliente](/help/overview/assets/cc-cdn.png)

Como alternativa, se nenhum provedor de CDN tiver sido adicionado anteriormente (conforme descrito acima), você será solicitado a adicionar o encaminhamento de log de CDN ao acessar os painéis de Agentes e Tráfegos de referência pela primeira vez. Para obter mais detalhes, consulte:

* [Tráfego de agentes](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfego por indicação](/help/dashboards/referral-traffic.md#setup#setup)

### Etapa 5: Explorar painéis e agir

Depois de fornecer informações sobre o Encaminhamento de Logs CDN, você poderá:

* Exiba o painel da [Presença da marca](/help/dashboards/brand-presence.md), exiba sua pontuação de visibilidade e acompanhe seu desempenho em relação a outras marcas.
* Explore os painéis [Agente](/help/dashboards/agentic-traffic.md) e [Tráfego de referência](/help/dashboards/referral-traffic.md), se o encaminhamento de log de CDN tiver sido configurado.
* Use as [Oportunidades](/help/dashboards/opportunities.md) para identificar melhorias técnicas e de conteúdo.
* Exporte dados e colabore com sua equipe ou convide seu colega de trabalho para usar o produto.

Por fim, para entender totalmente os recursos do LLM Optimizer, você deve explorar todos os [painéis](/help/dashboards/dashboards-overview.md) disponíveis.
