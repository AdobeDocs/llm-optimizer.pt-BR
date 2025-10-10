---
title: Configuração do cliente
description: Use a configuração do cliente para definir como sua marca será monitorada e analisada na plataforma do otimizador LLM.
source-git-commit: 7d01b35cb2153e020f0b64e493aad263fb9bb09f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Configuração do cliente

A Configuração do cliente é onde você define como sua marca será monitorada e analisada na plataforma do otimizador LLM. Você pode personalizar categorias (como unidades de negócios ou linhas de produtos), rastrear concorrentes e adicionar aliases de menção à marca para capturar todas as variações da sua marca em prompts. Essa configuração garante que a plataforma personalize insights para o contexto comercial, permitindo uma visibilidade precisa, tráfego e análise de oportunidades.

![Painel de configuração do cliente](/help/dashboards/assets/customer-config.png)

Para configurar como o LLM Optimizer monitora e analisa a presença da sua marca em diferentes mercados e cenários competitivos, você tem acesso às seguintes guias:

* [Categorias](#categories)
* [Rastreamento do concorrente](#competitor-tracking)
* [Aliases da marca](#brand-aliases)
* [Insights de dados](#data-insights)
* [CDN agente](#agentic-cdn)

## Categorias {#categories}

Na guia Categorias, é possível definir categorias comerciais ou linhas de produtos que você deseja rastrear e associá-las a regiões específicas. Em geral, a guia Categorias está relacionada a todas as outras personalizações nesta página, pois as categorias aparecerão no campo de categoria para as outras personalizações (rastreamento de concorrente, aliases e assim por diante). Para adicionar uma nova categoria:

1. Clique no botão **Adicionar**.
2. Na nova janela de configuração, adicione o **Nome da Categoria**.
3. Personalize a **Região Associada** onde a categoria será monitorada.
4. Clique em **Salvar** e a nova categoria aparecerá na lista de categorias.

A adição de novas categorias não gerará automaticamente tópicos e prompts; eles precisarão ser adicionados manualmente na guia [Data Insights](#data-insights).

Para excluir uma categoria, clique no ícone excluir na lista de categorias. Cuidado, porque **a exclusão de uma categoria também excluirá os itens associados**, como concorrentes que você pode ter configurado ou aliases de marca vinculados a essa categoria específica.

## Rastreamento do concorrente {#competitor-tracking}

Ao usar o rastreamento de concorrentes, você pode acompanhar como seus concorrentes são mencionados em relação à sua marca em diferentes categorias e regiões. Monitore a presença e o desempenho nos segmentos de mercado. Para personalizar o rastreamento do concorrente:

1. Para adicionar um novo concorrente, clique no botão **Adicionar**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Adicione o nome do concorrente.
4. Personalize o Alias e os Domínios do concorrente, se necessário.
5. Clique em **Salvar** e o novo concorrente aparecerá na lista de concorrentes.

Para excluir um concorrente, clique no ícone excluir da lista de concorrentes.

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

## CDN agente {#agentic-cdn}

Não disponível (estará disponível para lançamento?).

