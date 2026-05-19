---
title: Controle de acesso
description: Saiba como usuários organizacionais e atribuídos ao produto diferem no Adobe LLM Optimizer, o que os usuários de somente leitura veem na interface do usuário e como os administradores atribuem acesso no Adobe Admin Console.
feature: Customer Configuration
autotag-review: '2026-05-15T17:26:43.837Z'
TQID: 'https://experienceleague.adobe.com/hJpQQpuHBRMdKT5oKA9z0Y8H3d3p6To-n2hWKrXgZsQ'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: b704f6a0-b2fb-4df0-9177-9753751004f5
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 618
ht-degree: 100%

---


# Controle de acesso

O Adobe LLM Optimizer oferece suporte ao controle de acesso básico, com base nas personas do usuário. Este recurso está disponível somente para **clientes pagantes** e é habilitado mediante solicitação. Não está disponível para clientes em período de avaliação.

>[!IMPORTANT]
>
>Para solicitar o acesso a esse recurso, os clientes pagantes devem entrar em contato com o gerente de conta da Adobe.

## Usuários atribuídos ao produto {#product-assigned-users}

Se estiver atribuído ao produto, você terá os mesmos recursos que um usuário organizacional padrão, além das seguintes permissões:

* Acesso de gravação na [Configuração do cliente](/help/dashboards/customer-configuration.md) para prompts, categorias, tópicos e configurações relacionadas.
* Implante otimizações com [Otimizar na borda](/help/dashboards/optimize-at-edge/overview.md) e gerencie sugestões.
* Gerencie as configurações do Google Search Console.
* Gerencie as configurações de Otimização na borda e da CDN.
* Integrar um novo site.

## Usuários organizacionais {#organizational-users}

Usuários organizacionais são usuários padrão que **não** estão atribuídos ao produto. Se você for um usuário organizacional, terá acesso **somente leitura** aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e às visualizações relacionadas. As restrições a seguir se aplicam.

### Configuração do cliente {#customer-configuration-restrictions}

* **Upload de prompts** está desativado.
* O gerenciamento e a edição de prompts, categorias, tópicos e região estão desativados.

  ![Restrições de configuração do cliente para usuários somente leitura](/help/dashboards/assets/access-control-customer-configuration.png)

### Configuração da CDN (configuração do cliente) {#cdn-configuration-restrictions}

* **Integrar CDN** está desabilitada (usuários somente leitura não podem adicionar um provedor de CDN).
* **Excluir CDN** está desabilitado (usuários somente leitura não podem remover uma configuração existente de CDN).
* O botão **Enviar** na caixa de diálogo de integração da CDN está desabilitado (usuários somente leitura não podem concluir a configuração da CDN).

  ![Restrições de configuração da CDN para usuários somente leitura](/help/dashboards/assets/access-control-cdn-configuration.png)

### Presença da marca — insights de dados {#brand-presence-restrictions}

* Botões **Excluir** ao lado dos tópicos estão ocultos (usuários somente leitura não podem remover tópicos do rastreamento).
* Botões **Excluir** ao lado das solicitações estão ocultos (usuários somente leitura não podem remover solicitações do rastreamento).

  ![Ações de Presença da marca ocultas para usuários somente leitura](/help/dashboards/assets/access-control-brand-presence.png)

### Oportunidades de Tráfego agêntico (oportunidades de página de erro) {#agentic-opportunities}

Para oportunidades como as páginas de erro 404, 403 e 503:

* **Implantar otimização** está oculto.
* Um alerta informativo explica que o acesso para implantação é necessário.

  ![Implantar otimização oculto nas oportunidades de tráfego agêntico](/help/dashboards/assets/access-control-agentic-deploy.png)

### Outras páginas de oportunidade {#other-opportunities}

O comportamento somente leitura também se aplica a tipos de oportunidade como:

* Sumário
* Resumo
* Legibilidade
* Pré-renderizar
* Cabeçalhos
* Perguntas frequentes
* Dados estruturados ausentes
* Oportunidade de correção genérica

Para estas páginas:

* **Implantar otimização** fica oculto quando o usuário não tem acesso de implantação.
* Um alerta em linha explica que o acesso para implantação é necessário. A mensagem é semelhante a: *Acesso de implantação necessário — Você não tem permissão para implantar otimizações ou gerenciar sugestões. Entre em contato com o administrador para solicitar acesso.*
* A barra inferior fixa com ações de implantação está oculta.

  ![Alerta em linha quando é necessário acesso à implantação](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Ações de implantação de Otimização na borda ocultas para usuários com acesso somente leitura](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Configuração de prompt do Google Search Console {#gsc-restrictions}

* Ações de gerenciar e conectar estão desabilitadas ou ocultas.
* A coluna de ações usada para adicionar prompts está oculta.

  ![Restrições de configuração do Google Search Console](/help/dashboards/assets/access-control-gsc.png)

### Integrar novo site {#onboarding-restrictions}

* Integrar novo site está desabilitado para usuários sem controle de acesso.

  ![Integrar novo site desabilitado](/help/dashboards/assets/access-control-onboarding.png)

## Atribuir o produto a um usuário ou grupo {#assign-product}

Um **administrador do sistema** da sua organização pode usar o [Adobe Admin Console](https://adminconsole.adobe.com/) para atribuir o Adobe LLM Optimizer a um usuário ou grupo.

1. Faça logon no [Adobe Admin Console](https://adminconsole.adobe.com/) com uma conta que tenha direito de administrador da organização.
1. Atribua o perfil de produto do Adobe LLM Optimizer (ou o direito de produto equivalente da organização) ao usuário ou grupo que deve receber recursos atribuídos ao produto.

Para obter instruções detalhadas, consulte [Gerenciar produtos no Admin Console](https://helpx.adobe.com/br/enterprise/using/manage-products.html) e[Gerenciar grupos de usuários](https://helpx.adobe.com/br/enterprise/using/user-groups.html).

>[!NOTE]
>
>Fluxos de tela no Adobe Admin Console podem sofrer alterações entre versões. Se as opções acima não corresponderem ao console, use os links de ajuda integrados no Adobe Admin Console ou entre em contato com a equipe de contas da Adobe.
