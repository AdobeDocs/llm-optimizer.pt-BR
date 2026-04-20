---
title: Controle de acesso
description: Saiba como os usuários atribuídos ao produto e organizacionais diferem no Adobe LLM Optimizer, o que os usuários somente leitura veem na interface do usuário e como os administradores atribuem acesso no Adobe Admin Console.
feature: Customer Configuration
source-git-commit: 3b792a8ca7efd4b6d6764d2e83f9b0c103a56558
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 4%

---


# Controle de acesso

O Adobe LLM Optimizer oferece suporte ao controle de acesso básico, com base nas personas do usuário. Este recurso está disponível somente para **clientes pagantes** e está habilitado mediante solicitação. Ele não está disponível para clientes de avaliação.

>[!IMPORTANT]
>
>Para solicitar o acesso a esse recurso, os clientes pagantes devem entrar em contato com o gerente de conta da Adobe.

## Usuários atribuídos ao produto {#product-assigned-users}

Se estiver atribuído ao produto, você terá os mesmos recursos que um usuário organizacional padrão, além das seguintes permissões:

* Acesso de gravação na [Configuração do cliente](/help/dashboards/customer-configuration.md) para prompts, categorias, tópicos e configurações relacionadas.
* Implante o [Otimizar nas otimizações do Edge](/help/dashboards/optimize-at-edge/overview.md) e gerencie sugestões.
* Gerencie as configurações do Google Search Console.
* Gerenciar Otimizar nas configurações de Edge e CDN.
* Integrar um novo site.

## Usuários organizacionais {#organizational-users}

Usuários organizacionais são usuários padrão que **não** estão atribuídos ao produto. Se você for um usuário organizacional, terá acesso de **somente leitura** aos [painéis do LLM Optimizer](/help/dashboards/dashboards-overview.md) e aos modos de exibição relacionados. As restrições a seguir se aplicam.

### Configuração do cliente {#customer-configuration-restrictions}

* **Prompts de Carregamento** está desabilitado.
* O gerenciamento e a edição de prompts, categorias, tópicos e região estão desativados.

  ![Restrições de configuração do cliente para usuários somente leitura](/help/dashboards/assets/access-control-customer-configuration.png)

### Configuração da CDN (Configuração do cliente) {#cdn-configuration-restrictions}

* **A CDN integrada** está desabilitada (usuários somente leitura não podem adicionar um provedor CDN).
* **Excluir CDN** está desabilitado (usuários somente leitura não podem remover uma configuração existente de CDN).
* O botão **Enviar** na caixa de diálogo de integração do CDN está desabilitado (usuários somente leitura não podem concluir a configuração do CDN).

  ![Restrições de configuração da CDN para usuários somente leitura](/help/dashboards/assets/access-control-cdn-configuration.png)

### Presença da marca — insights de dados {#brand-presence-restrictions}

* Os botões **Excluir** ao lado dos tópicos estão ocultos (usuários somente leitura não podem remover tópicos do rastreamento).
* Os botões **Excluir** ao lado das solicitações estão ocultos (usuários somente leitura não podem remover solicitações do rastreamento).

  ![Ações de Presença da marca ocultas para usuários somente leitura](/help/dashboards/assets/access-control-brand-presence.png)

### Oportunidades de Tráfego de agente (oportunidades de página de erro) {#agentic-opportunities}

Para oportunidades como as páginas de erro 404, 403 e 503:

* **A Otimização de Implantação** está oculta.
* Um alerta informativo explica que o acesso para implantação é necessário.

  ![Implantar Otimização oculta em oportunidades de Tráfego Agencial](/help/dashboards/assets/access-control-agentic-deploy.png)

### Outras páginas de oportunidade {#other-opportunities}

O comportamento somente leitura também se aplica a tipos de oportunidade como:

* Índice
* Resumo
* Legibilidade
* Pré-renderizar
* Cabeçalhos
* Perguntas frequentes
* Dados estruturados ausentes
* Oportunidade de patch genérica

Para estas páginas:

* **A Otimização de Implantação** fica oculta quando o usuário não tem acesso de implantação.
* Um alerta em linha explica que o acesso para implantação é necessário. A mensagem é semelhante a: *Acesso de Implantação Necessário — Você não tem permissão para implantar otimizações ou gerenciar sugestões. Entre em contato com o administrador para solicitar acesso.*
* A barra inferior fixa com ações de implantação está oculta.

  ![Alerta embutido quando é necessário acesso de implantação](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Otimizar ações de implantação do Edge ocultas para usuários somente leitura](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Configuração do prompt do Google Search Console {#gsc-restrictions}

* As ações Gerenciar e Conectar estão desabilitadas ou ocultas.
* A coluna de ações usada para adicionar prompts está oculta.

  ![Restrições de configuração do Google Search Console](/help/dashboards/assets/access-control-gsc.png)

### Integrar um novo site {#onboarding-restrictions}

* A integração de um novo site está desabilitada para usuários sem controle de acesso.

  ![Integrar novo site desabilitado](/help/dashboards/assets/access-control-onboarding.png)

## Atribuir o produto a um usuário ou grupo {#assign-product}

Um **administrador do sistema** da sua organização pode usar o [Adobe Admin Console](https://adminconsole.adobe.com/) para atribuir o Adobe LLM Optimizer a um usuário ou grupo.

1. Entre no [Adobe Admin Console](https://adminconsole.adobe.com/) com uma conta que tenha direitos administrativos para sua organização.
1. Atribua o perfil de produto da Adobe LLM Optimizer (ou o direito de produto equivalente da sua organização) ao usuário ou grupo que deve receber recursos atribuídos ao produto.

Para obter etapas detalhadas, consulte [Gerenciamento de produtos no Admin Console](https://helpx.adobe.com/br/enterprise/using/manage-products.html) e [Gerenciamento de grupos de usuários](https://helpx.adobe.com/br/enterprise/using/user-groups.html).

>[!NOTE]
>
>Os fluxos de tela no Adobe Admin Console podem mudar entre versões. Se as opções acima não corresponderem ao seu console, use os links de ajuda do produto no Adobe Admin Console ou entre em contato com a equipe de conta da Adobe.
