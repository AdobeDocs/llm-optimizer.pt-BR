---
title: Configuração do cliente
description: Use a configuração do cliente para definir como a marca será monitorada e analisada na plataforma do LLM Optimizer.
feature: Customer Configuration
source-git-commit: 5d8b59ea4281c88bb42dc48096c07a3faaeb2e88
workflow-type: ht
source-wordcount: '836'
ht-degree: 100%

---


# Configuração do cliente {#customer-configuration}

O painel Configuração do cliente é uma ferramenta poderosa que fornece insights sobre a visibilidade da marca em LLMs. Ao configurar corretamente categorias, tópicos e prompts é possível garantir que a marca esteja bem posicionada para aparecer em respostas geradas pelo LLM. Essa configuração garante que a plataforma personalize insights para o contexto empresarial, permitindo visibilidade, tráfego e análise de oportunidades precisos.

![Painel Configuração do cliente](/help/dashboards/assets/customer-config.png)

Para configurar como o LLM Optimizer monitora e analisa a presença da marca em diferentes mercados e cenários competitivos, você tem acesso às seguintes guias:

* [Prompts](#prompts-brand)
* [Categorias](#categories)
* [Outras marcas](#other-brands)
* [Aliases da marca](#brand-aliases)
* [Configuração da CDN](#agentic-cdn)

>[!IMPORTANT]
>
> Para obter mais detalhes sobre como configurar categorias, tópicos e prompts, consulte a página [Práticas recomendadas para configurar categorias, tópicos e prompts](/help/overview/best-practices-topics-prompts.md).

## Prompts {#prompts-brand}

Nesta guia, é possível revisar, gerenciar e personalizar prompts. É possível fazer upload de um arquivo .csv de [Análise de presença da marca](/help/dashboards/brand-presence.md) e a lista será preenchida com prompts e tópicos dessa análise, ou [Baixar uma biblioteca de prompts](/help/overview/best-practices-topics-prompts.md) criada pela Adobe. Também é possível excluir, modificar e adicionar tópicos e seus prompts associados, conforme necessário.

Para importar um arquivo .csv de insights de dados, primeiro é necessário exportar um arquivo do painel Presença da marca. Consulte a seção [insights de dados](/help/dashboards/brand-presence.md#data-insights) para saber como fazer isso. Depois de obter o arquivo:

1. No painel, clique em **Fazer upload de CSV**.
2. Na janela Importar insights de dados, arraste e solte ou escolha manualmente o arquivo.
3. Clique em **Fazer upload dos dados**.

Também é possível criar um novo arquivo CSV baixando o modelo da janela **Importar insights de dados**. Após obter o modelo, abra-o e insira os tópicos com os prompts, categorias e regiões associados, cada um em uma nova linha.

Para saber como baixar e usar a Biblioteca de prompts do setor criada pela Adobe, consulte a seção Biblioteca de prompts do setor [nesta página](/help/overview/best-practices-topics-prompts.md)

Além disso, é possível adicionar tópicos/prompts à lista, independentemente de um arquivo CSV ou biblioteca de prompts. Para isso, no painel, é necessário:

1. Clicar em **Adicionar tópico**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Insira o nome do tópico.
4. Adicione o texto do prompt.
5. Selecione a região.
6. Clique em **Adicionar prompt** e o tópico com o prompt aparecerá na lista.

>[!NOTE]
>Os prompts recém-adicionados não aparecerão na presença da marca até que o processamento seja concluído.

Na lista, clique em cada tópico e os prompts associados serão exibidos. Para excluir o tópico e seus prompts associados, clique no ícone de excluir na lista.

## Categorias {#categories}

Na guia Categorias, é possível definir categorias de negócios ou linhas de produtos que você deseja monitorar e associá-las a regiões específicas. Em geral, a guia Categorias está relacionada a quase todas as outras personalizações nesta página, pois as categorias aparecerão no campo de categoria para as outras personalizações (rastreamentos de outros, aliases e assim por diante). Para adicionar uma nova categoria:

1. Clique em **Adicionar**.
2. Na nova janela de configuração, adicione o **Nome da categoria**.
3. Personalize a **Região associada** onde a categoria será monitorada.
4. Clique em **Salvar** e a nova categoria aparecerá na lista de categorias.

A adição de novas categorias não gerará automaticamente tópicos e prompts. Eles precisarão ser adicionados manualmente a partir da guia [Insights de dados](#data-insights).

Para excluir uma categoria, clique no ícone excluir na lista de categorias. Cuidado, porque **a exclusão de uma categoria também excluirá os itens associados**, como aliases de marca que estão vinculados a essa categoria específica.

## Outras marcas {#others-tracking}

Ao usar essa guia, é possível acompanhar como os outros são mencionados em relação à sua marca em diferentes categorias e regiões. Monitore a presença e o desempenho nos seus segmentos de mercado. Para personalizar o rastreamento:

1. Clique em **Adicionar**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Adicione o nome do outro.
4. Personalize o alias e os domínios do outro, se necessário.
5. Clique em **Salvar**.

Para excluir uma entrada na lista, clique no ícone de exclusão.

## Aliases da marca {#brand-aliases}

Ao usar aliases de marca, é possível configurar nomes alternativos e variações da marca a serem rastreados em diferentes categorias e regiões. Isso garante o monitoramento abrangente de todas as menções da marca. Para adicionar um alias de marca:

1. Clique em **Adicionar**.
2. Na nova janela de configuração, selecione a **Categoria**. As categorias criadas anteriormente aparecerão aqui.
3. Selecione a **Região** onde o alias será monitorado.
4. Adicione o alias da marca.
5. Clique em **Salvar** e o alias da marca aparecerá na lista.

Para excluir um alias de marca, clique no ícone de exclusão da lista de aliases.

## Configuração da CDN {#cdn-configuration}

Nessa guia, é possível configurar os fluxos da CDN para permitir que o Adobe LLM Optimizer analise os dados da CDN. Esses dados serão usados para alimentar painéis (como o tráfego agêntico), fornecendo insights sobre padrões de tráfego, métricas de desempenho e oportunidades de otimização. Para integrar o provedor da CDN, clique em **Integrar CDN**.

![CDN de configuração do cliente](/help/overview/assets/cc-cdn.png)

Na janela **Integrar provedor da CDN**:

1. Selecione o provedor da CDN.
2. Clique em **Integrar** para habilitar o encaminhamento de logs.

Caso selecione **Outro**, entre em contato com llmo-now@adobe.com para obter ajuda.
