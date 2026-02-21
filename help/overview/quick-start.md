---
title: Início rápido
description: 'Introdução ao Adobe LLM Optimizer: integre sua marca, desbloqueie os insights de visibilidade da IA e explore painéis para aumentar o desempenho da pesquisa.'
feature: Quickstart, Onboarding
source-git-commit: 82830e66d43ddd9741617cdf6daab63cd259554b
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 93%

---


# Início rápido

Para começar a usar o LLM Optimizer, é necessário concluir o processo de integração conforme detalhado nas etapas apresentadas abaixo. Após concluir o processo, você terá acesso total aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e a outras funcionalidades.

## Visão geral da integração

O processo de integração começa com a integração do seu domínio. O processo é diferente dependendo se você é cliente da AEM Cloud ou não. Após concluir o processo, será necessário fornecer informações para o Encaminhamento de logs da CDN e, por fim, personalizar categorias, tópicos e prompts. Cada parte do processo é detalhada abaixo, juntamente com dicas úteis sobre como começar a usar o LLM Optimizer o mais rápido possível.

### Permitir que o Adobe LLM Optimizer acesse páginas públicas

Para fornecer conteúdo preciso e recomendações técnicas, o Adobe LLM Optimizer precisa de acesso às suas páginas direcionadas ao público. Isso é feito por meio de um rastreador interno seguro (agente do usuário Spacecat/1.0).

Requisitos de configuração:

* Adicione o agente de usuário Spacecat/1.0 à lista de permissões no arquivo robots.txt do seu site ou nas regras de gerenciamento de tráfego de bots
* Verifique se as páginas não estão bloqueadas no nível de domínio ou da CDN. Páginas bloqueadas não podem ser indexadas, o que significa que tarefas de otimização e insights não podem ser gerados para elas.

Se a visibilidade do conteúdo parecer baixa no painel, verifique se o rastreador tem acesso aos seus domínios. O acesso restrito é uma causa comum de indexação incompleta.

## Etapa 1: integrar seu domínio

### Experimentar antes de comprar

Os clientes do AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) têm a opção de usar a oferta **Experimentar antes de comprar**. É uma versão de avaliação gratuita do LLM Optimizer com até 200 prompts gratuitos. O uso de mais de 200 prompts exige um contrato de licença separado. O acesso é fornecido no “estado em que se encontra” e “conforme disponível” e pode ser modificado, limitado ou removido pela Adobe a qualquer momento.

Alguns recursos do produto não estão disponíveis na versão gratuita:

* A versão de avaliação está limitada a um domínio. Você não poderá alterar o domínio fornecido após concluir a configuração.
* A capacidade de implantar otimizações está disponível em Acesso antecipado. Saiba mais em [Otimizar em Perguntas Frequentes da Edge](https://experienceleague.adobe.com/pt-br/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Consulte a seção abaixo para obter detalhes sobre como ativar a versão de avaliação gratuita e integrar seu domínio.

### Clientes da AEM Cloud

Se você é cliente da AEM Cloud, tem a opção de experimentar o LLM Optimizer usando o cartão de anúncio do produto no [Experience Hub](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/experience-hub/experience-hub).

>[!NOTE]
>Os prompts adicionados recentemente não aparecerão no [Painel de presença da marca](/help/dashboards/brand-presence.md) até que o processamento seja concluído. Os clientes da AEM Cloud podem usar a versão de avaliação gratuita do LLM Optimizer. O uso de mais de 200 prompts exige um contrato de licença separado. O acesso é fornecido no “estado em que se encontra” e “conforme disponível” e pode ser modificado, limitado ou removido pela Adobe a qualquer momento. Entre em contato com o seu representante de conta para obter mais informações.

![Versão de avaliação do LLM Optimizer](/help/overview/assets/llm-trial.png)

Depois de clicar no botão **Testar o LLM Optimizer**, haverá um redirecionamento para [https://llmo.now](https://llmo.now). Em seguida, será necessário fazer logon via IMS. Depois de fazer logon, você deve iniciar o processo de integração fornecendo um domínio e o nome da marca.

![Domínio do LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>O domínio fornecido será usado por todos da sua organização e não poderá ser alterado.

Um pequeno conjunto de categorias, tópicos e prompts é gerado durante a fase de integração. A análise de presença da marca nesses prompts estará disponível logo após a integração do site.

<!--![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)-->

Além disso, você também precisa configurar o [encaminhamento de logs da CDN](#step-4) para análise de tráfego. O LLM Optimizer exige dados de presença da marca e insights do tráfego agêntico e de referência para identificar oportunidades e fornecer recomendações prescritivas a fim de aumentar a visibilidade da IA.

### Clientes que não usam a AEM Cloud

Após a finalização do contrato comercial, você será integrado ao domínio que deseja integrar no LLM Optimizer. Assim que a integração for concluída, você poderá fazer logon no LLM Optimizer por meio de [https://llmo.now](https://llmo.now).

## Etapa 2: personalizar categorias, tópicos e prompts

Após a integração do site, você poderá visualizar a análise de presença da marca com base no pequeno conjunto de prompts gerados automaticamente durante a fase de integração. Agora é possível personalizar as categorias, os tópicos e os prompts da sua marca. Esta configuração é criada no [painel de configuração do cliente](/help/dashboards/customer-configuration.md).

![Painel de configuração do cliente](/help/overview/assets/prompt-creation.png)

Nesse painel, é possível:

* Adicionar **novas categorias** alinhadas às suas prioridades comerciais. As categorias podem ser áreas de conteúdo amplas e relevantes para o seu domínio.
* Inserir **tópicos personalizados** ou subtópicos que você deseja rastrear. Os tópicos podem ser temas específicos vinculados a palavras-chave não relacionadas à marca e de alto volume associadas ao seu domínio.
* Criar **seus prompts** para monitorar a visibilidade em consultas específicas. Os prompts são consultas (com e sem marca) que fornecem uma visibilidade da linha de base. Apenas um número limitado de prompts será gerado automaticamente com base nas categorias e tópicos que você forneceu.
* Definir **aliases** de menção para garantir que todas as menções de uma marca sejam capturadas e contabilizadas.
* Definir **outros aliases** para rastrear outras marcas com precisão.

>[!NOTE]
>Os prompts exatos que você solicita aos LLMs não estão disponíveis publicamente, pois não são divulgados pelos LLMs.

>[!NOTE]
>
> Para obter mais detalhes sobre como configurar categorias, tópicos e prompts, consulte a página [Práticas recomendadas para configurar categorias, tópicos e prompts](/help/overview/best-practices-topics-prompts.md).

## Etapa 3: insights de presença da marca

Após a integração do domínio, você verá informações iniciais na visualização Presença da marca, com base nos prompts gerados automaticamente durante a integração. Depois de personalizar suas próprias categorias, tópicos e prompts, o LLM Optimizer acionará automaticamente a análise de presença da marca nos prompts fornecidos e os resultados estarão disponíveis em 24 horas.

## Etapa 4: fornecer informações para encaminhamento de logs da CDN {#step-4}

Para obter insights sobre tráfego agêntico e tráfego de referência, você precisa fornecer informações para o encaminhamento de logs da CDN. Elas podem ser adicionadas a partir do [painel de configuração do cliente](/help/dashboards/customer-configuration.md#cdn-configuration), acessado pela guia **Configuração de CDN** e por clicar em **Integrar CDN**.

![CDN de configuração do cliente](/help/overview/assets/cc-cdn.png)

Como alternativa, se nenhum provedor de CDN tiver sido adicionado anteriormente (conforme descrito acima), será solicitado que você adicione o encaminhamento de logs de CDN ao acessar os painéis de tráfego agêntico e de referência pela primeira vez. Para obter mais detalhes, consulte:

* [Tráfego agêntico](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfego de referência](/help/dashboards/referral-traffic.md#setup#setup)

## Etapa 5: explorar painéis e agir

Depois de fornecer informações sobre o encaminhamento de logs da CDN, você poderá:

* Visualizar o painel de [Presença da marca](/help/dashboards/brand-presence.md), ver sua pontuação de visibilidade e acompanhar seu desempenho em relação a outras marcas.
* Explorar os painéis de [Tráfego agêntico](/help/dashboards/agentic-traffic.md) e [Tráfego de referência](/help/dashboards/referral-traffic.md), se o encaminhamento de logs da CDN tiver sido configurado.
* Usar [oportunidades](/help/dashboards/opportunities.md) para identificar melhorias técnicas e de conteúdo.
* Exportar dados e colaborar com sua equipe ou convidar um colega de trabalho para usar o produto.

Por fim, para entender totalmente os recursos do LLM Optimizer, você deve explorar todos os [painéis](/help/dashboards/dashboards-overview.md) disponíveis.
