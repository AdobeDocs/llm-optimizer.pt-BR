---
title: Configuração do cliente
description: Use a configuração do cliente para definir como sua marca será monitorada e analisada na plataforma do otimizador LLM.
feature: Customer Configuration
source-git-commit: c6e37395362262eb5fe8366473e76086e36d77e9
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---


# Configuração do cliente {#customer-configuration}

O Painel de configuração do cliente é uma ferramenta poderosa que fornece insights sobre a visibilidade da sua marca em LLMs. Ao configurar corretamente categorias, tópicos, prompts, você pode garantir que sua marca esteja bem posicionada para aparecer em respostas geradas pelo LLM. Essa configuração garante que a plataforma personalize insights para o contexto comercial, permitindo uma visibilidade precisa, tráfego e análise de oportunidades.

![Painel de configuração do cliente](/help/dashboards/assets/customer-config.png)

Para configurar como o LLM Optimizer monitora e analisa a presença da sua marca em diferentes mercados e cenários competitivos, você tem acesso às seguintes guias:

* [Categorias](#categories)
* [Rastreamento de outros](#others-tracking)
* [Aliases da marca](#brand-aliases)
* [Insights de dados](#data-insights)
* [Configuração de CDN](#agentic-cdn)

>[!IMPORTANT]
>
> Para obter mais detalhes sobre como configurar suas categorias, tópicos, prompts, consulte a página [Práticas recomendadas para configurar categorias, tópicos, prompts](/help/overview/best-practices-topics-prompts.md).

## Categorias {#categories}

Na guia Categorias, é possível definir categorias comerciais ou linhas de produtos que você deseja rastrear e associá-las a regiões específicas. Em geral, a guia Categorias está relacionada a quase todas as outras personalizações nesta página, pois as categorias aparecerão no campo de categoria para as outras personalizações (outros rastreamentos, aliases e assim por diante). Para adicionar uma nova categoria:

1. Clique no botão **Adicionar**.
2. Na nova janela de configuração, adicione o **Nome da Categoria**.
3. Personalize a **Região Associada** onde a categoria será monitorada.
4. Clique em **Salvar** e a nova categoria aparecerá na lista de categorias.

A adição de novas categorias não gerará automaticamente tópicos e prompts; eles precisarão ser adicionados manualmente na guia [Data Insights](#data-insights).

Para excluir uma categoria, clique no ícone excluir na lista de categorias. Cuidado, porque **a exclusão de uma categoria também excluirá os itens associados**, como aliases de marca, que estão vinculados a essa categoria específica.

## Rastreamento de outros {#others-tracking}

Ao usar essa guia, você pode acompanhar como os outros são mencionados em relação à sua marca em diferentes categorias e regiões. Monitore a presença e o desempenho nos segmentos de mercado. Para personalizar o rastreamento:

1. Clique no botão **Adicionar**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Adicione o nome do outro.
4. Personalize os outros Alias e Domínios, se necessário.
5. Clique em **Salvar**.

Para excluir uma entrada na lista , clique no ícone delete.

## Aliases da marca {#brand-aliases}

Ao usar aliases de marca, você pode configurar nomes alternativos e variações de sua marca que devem ser rastreados em diferentes categorias e regiões. Isso garante um monitoramento abrangente de todas as menções à marca. Para adicionar um alias de marca:

1. Clique no botão **Adicionar**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Selecione a **Região** onde o alias será monitorado.
4. Adicione o alias da marca.
5. Clique em **Salvar** e o alias da marca aparecerá na lista.

Para excluir um alias de marca, clique no ícone excluir na lista de alias.

## Insights de dados {#data-insights}

Nesta guia, é possível revisar, gerenciar e personalizar prompts. Você pode carregar um [insights de dados de presença da marca](/help/dashboards/brand-presence.md#data-insights) .csv e a lista será preenchida com prompts e tópicos dessa análise. Você também pode excluir, modificar e adicionar tópicos e seus prompts associados, conforme necessário.

Para importar um arquivo de insights de dados .csv, primeiro é necessário exportar um arquivo do painel Presença da marca. Consulte a seção [insights de dados](/help/dashboards/brand-presence.md#data-insights) para saber como fazer isso. Depois de ter o arquivo:

1. No painel, clique em **Carregar CSV**.
2. Na janela Importar insights de dados, arraste e solte ou escolha manualmente o arquivo.
3. Clique em **Carregar dados**.

Você também pode criar um novo arquivo CSV baixando o modelo da janela **Importar Insights de Dados**. Depois de ter o modelo, abra-o e insira seus tópicos junto com seus prompts associados, categorias e regiões, cada um em uma nova linha.

Além disso, você também pode adicionar tópicos/prompts à lista independentemente de um arquivo CSV. Para isso, no painel, é necessário:

1. Clique no botão **Adicionar tópico**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Informe o nome do tópico.
4. Adicione o texto do prompt.
5. Selecione a região.
6. Clique em **Adicionar prompt** e o tópico com o prompt aparecerá na lista.

>[!NOTE]
>Os prompts adicionados recentemente não aparecerão na Presença da Marca até que o processamento seja concluído.

Na lista, você pode clicar em cada tópico e os prompts associados serão exibidos. Para excluir o tópico e seus prompts associados, clique no ícone excluir da lista.

## Configuração de CDN {#cdn-configuration}

Nessa guia, é possível configurar os fluxos de CDN para permitir que o Adobe LLM Optimizer analise os dados de CDN. Esses dados serão usados para alimentar painéis (como Tráfego de referência e de agente), fornecendo insights sobre padrões de tráfego, métricas de desempenho e oportunidades de otimização. Para integrar seu provedor de CDN, clique em **Integrar CDN**.

![CDN de Configuração de Cliente](/help/overview/assets/cc-cdn.png)

Na janela **Onboard CDN Provider**:

1. Selecione seu provedor de CDN.
2. Clique em **Integrar** para habilitar o encaminhamento de log.

Se você selecionar **Outros**, precisará entrar em contato com llmo-now@adobe.com para obter assistência.
