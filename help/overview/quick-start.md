---
title: Início rápido
description: Saiba como integrar o nome da marca e o domínio, ativar a avaliação no Experience Hub ou no Experience Cloud e concluir a configuração do Adobe LLM Optimizer.
feature: Quickstart, Onboarding
source-git-commit: dcbeb1c61dd9dcefd83908f65f8303d36c0fb78e
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 47%

---


# Início rápido

Para começar a usar o LLM Optimizer, é necessário concluir o processo de integração. Após a integração, você poderá personalizar categorias, tópicos, prompts e configurar o encaminhamento de logs para obter insights mais precisos e acesso total aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e outras funcionalidades.

## Visão geral da integração

O processo de integração começa com a integração do domínio e do nome da marca. Cada parte da jornada de integração é detalhada abaixo, juntamente com dicas úteis sobre como começar a usar o LLM Optimizer o mais rápido possível.

### Permitir que o Adobe LLM Optimizer acesse páginas públicas

Para fornecer conteúdo preciso e recomendações técnicas, o Adobe LLM Optimizer precisa de acesso às suas páginas direcionadas ao público. Isso é feito por meio de um rastreador interno seguro (agente do usuário Spacecat/1.0).

Requisitos de configuração:

* Adicione o agente de usuário Spacecat/1.0 ao Incluo na lista de permissões nas regras de gerenciamento de tráfego de bot ou robots.txt do site.
* Certifique-se de que as páginas não estejam bloqueadas no nível de domínio ou CDN. Páginas bloqueadas não podem ser indexadas, o que significa que tarefas de otimização e insights não podem ser gerados para elas.

Se a visibilidade do conteúdo parecer baixa no painel, verifique se o rastreador tem acesso aos seus domínios. O acesso restrito é uma causa comum de indexação incompleta.

## Etapa 1: integre o nome da sua marca e domínio {#step-1-onboard-your-domain}

Para começar a usar o LLM Optimizer, primeiro ative sua versão de avaliação (se elegível) e integre o nome da marca e o domínio.

### Ativar sua versão de avaliação

O fluxo de ativação é diferente dependendo do produto Adobe.

#### Clientes da AEM Cloud

Para ativar sua avaliação, como cliente da AEM Cloud, você pode:

* Navegue até [Experience Hub](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) e use o cartão Anúncio do Produto para ativar o LLM Optimizer. Após selecionar **Tentar LLM Optimizer**, você será redirecionado para [https://llmo.now](https://llmo.now). Faça logon por meio do IMS e insira um domínio e um nome de marca para iniciar o processo de integração.
* Ou vá diretamente para [https://llmo.now](https://llmo.now) e entre.

![Versão de avaliação do LLM Optimizer](/help/overview/assets/llm-trial.png)

#### Clientes do Adobe Analytics

Se você for cliente do Adobe Analytics, verá um banner na página inicial do Experience Cloud.

![Página inicial do Experience Cloud com o banner Iniciar avaliação do Adobe LLM Optimizer](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

Você pode ativar sua versão de avaliação de uma das seguintes maneiras:

* Selecione **Iniciar sua avaliação do Adobe LLM Optimizer** no banner.
* Vá diretamente para [https://llmo.now](https://llmo.now) e entre.

Quando a versão de avaliação estiver ativa, continue com a integração do nome da marca e do domínio.

>[!NOTE]
>
> * **Avaliação gratuita:** os clientes da AEM Cloud e da Adobe Analytics podem usar a versão de avaliação gratuita do LLM Optimizer.
> * **Os clientes que ativarem a avaliação em ou após 1º de abril de 2026** poderão usar até 100 prompts, um domínio e implantar otimizações em até 10 URLs para um único tipo de oportunidade.
> * **Os clientes que ativaram a avaliação antes de 1º de abril de 2026** continuam a ter acesso a até 200 prompts de acordo com seus termos existentes.
>
>O uso além dos limites incluídos requer um contrato de licença separado. O acesso é fornecido &quot;no estado em que se encontra&quot; e &quot;conforme disponível&quot; e pode ser modificado, limitado ou removido a qualquer momento. Entre em contato com seu representante de conta para obter mais informações.

#### Integre o nome da sua marca e domínio

Integre o nome da marca e o domínio para começar a usar o LLM Optimizer.

1. Insira o nome da sua marca e o domínio associado.

   * Esse deve ser o domínio principal onde você deseja analisar e otimizar o conteúdo.

1. Integração concluída.

   * Depois de enviado, o LLM Optimizer começa a analisar seu domínio e gerar insights.

![Domínio do LLM Optimizer](/help/overview/assets/domain.png)

>[!NOTE]
>Os prompts adicionados recentemente não aparecerão no [Painel de presença da marca](/help/dashboards/brand-presence.md) até que o processamento seja concluído.

>[!NOTE]
>O domínio fornecido será usado por todos da sua organização e não poderá ser alterado.

Um pequeno conjunto de categorias, tópicos e prompts é gerado durante a fase de integração. A análise de presença da marca nesses prompts estará disponível logo após a integração do site.

A capacidade de implantar otimizações na borda também está disponível. Saiba mais em [Otimizar na Edge — Perguntas frequentes](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Além disso, configure o [encaminhamento de logs da CDN](#step-4) para análise de tráfego. O LLM Optimizer exige dados e insights de Presença da marca do agente e do tráfego de referência para identificar oportunidades e fornecer recomendações prescritivas que aumentem a visibilidade da IA.

### Clientes que não usam a AEM Cloud

Depois que sua organização finalizar o contrato comercial, você será integrado à LLM Optimizer com o domínio selecionado por sua organização. Quando a integração terminar, entre em [https://llmo.now](https://llmo.now).

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

Para desbloquear os insights de Tráfego e Tráfegos de referência do Agente, adicione informações de encaminhamento de log CDN no [painel de configuração do cliente](/help/dashboards/customer-configuration.md#cdn-configuration). Abra a guia **Configuração de CDN** e selecione **CDN integrada**.

![CDN de configuração do cliente](/help/overview/assets/cc-cdn.png)

Como alternativa, se nenhum provedor de CDN tiver sido adicionado anteriormente (conforme descrito acima), será solicitado que você adicione o encaminhamento de logs de CDN ao acessar os painéis de tráfego agêntico e de referência pela primeira vez. Para obter mais detalhes, consulte:

* [Tráfego agêntico](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Tráfego de referência](/help/dashboards/referral-traffic.md#setup)

>[!NOTE]
>Para obter detalhes sobre o encaminhamento de logs ao usar uma CDN gerenciada pelo cliente (BYOCDN), consulte [Visão geral do encaminhamento de logs BYOCDN](/help/overview/log-forwarding/log-forwarding-overview.md)

## Etapa 5: explorar painéis e agir

Depois de fornecer informações sobre o encaminhamento de logs da CDN, você poderá:

* Visualizar o painel de [Presença da marca](/help/dashboards/brand-presence.md), ver sua pontuação de visibilidade e acompanhar seu desempenho em relação a outras marcas.
* Explore os painéis [Agente](/help/dashboards/agentic-traffic.md) e [Tráfego de referência](/help/dashboards/referral-traffic.md), se o encaminhamento de log de CDN tiver sido configurado.
* Usar [oportunidades](/help/dashboards/opportunities.md) para identificar melhorias técnicas e de conteúdo.
* Exportar dados e colaborar com sua equipe ou convidar um colega de trabalho para usar o produto.

Por fim, para entender totalmente os recursos do LLM Optimizer, você deve explorar todos os [painéis](/help/dashboards/dashboards-overview.md) disponíveis.
