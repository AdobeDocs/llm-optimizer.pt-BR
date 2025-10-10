---
title: Configuração do cliente
description: Use a configuração do cliente para definir como sua marca será monitorada e analisada na plataforma do otimizador LLM.
source-git-commit: 653a6be856412faac8783fa9dc7b759a7c6e1f68
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---


# Configuração do cliente

A Configuração do cliente é onde você define como sua marca será monitorada e analisada na plataforma do otimizador LLM. Você pode personalizar categorias (como unidades de negócios ou linhas de produtos), rastrear concorrentes e adicionar aliases de menção à marca para capturar todas as variações da sua marca em prompts. Essa configuração garante que a plataforma personalize insights para o contexto comercial, permitindo uma visibilidade precisa, tráfego e análise de oportunidades.

![Painel de configuração do cliente](/help/dashboards/assets/customer-config.png)


## Práticas recomendadas para configurar categorias, tópicos e prompts

Esta seção descreve as práticas recomendadas para decidir como você deseja configurar suas categorias, tópicos, prompts e concorrentes.

Este é um primeiro passo vital. O que você decide agora determina como as informações são adaptadas ao seu contexto de negócios. Quaisquer alterações em categorias no futuro redefinirão os dados históricos.

### Práticas recomendadas para categorias

As categorias permitem organizar o conteúdo em unidades estratégicas de negócios ou agrupamentos lógicos. Eles são o bucket &quot;ao qual pertence&quot; e a estrutura organizacional de nível superior do seu conteúdo.

Ao decidir como configurar categorias, você precisa considerar suas metas e quem precisa agir de acordo com o que você está relatando.

>[!IMPORTANT]
>
> Verifique se as categorias estão configuradas corretamente desde o início, já que as alterações nas categorias redefinem os dados históricos. Isso significa que, se você alterá-los, perderá dados históricos anteriores à alteração.

Esta é uma visão geral dos tipos de abordagens que você pode realizar e quando você escolheria uma abordagem específica:

| Abordagem | Descrição | Benefício |
|---------|----------|---------|
| Unidade estratégica de negócios (SBU) | Use essa abordagem se sua organização for dividida por P&amp;L (por exemplo, Consumidor, Empresa, Serviços). | Você obtém relatórios limpos por linha de negócios e responsabilidade mais fácil. |
| Diretório de nível superior do site (URL_DIR) | Use se a arquitetura de informações do site espelhar a propriedade (/products/, /support/, /docs/, /news/). | Você obtém alinhamento com a forma como as equipes publicam e mantêm conteúdo. |
| Categoria do produto (ou serviço) | Use-o se você vender um catálogo (SKUs/serviços). | Você recebe respostas de exibições de variedade, análise de lacuna e &quot;qual categoria precisa de conteúdo&quot;. |

Como decidir como você configura categorias se baseia em uma pergunta: **Quem precisa agir no relatório?**

* Se você for um *líder de negócios*, escolha a abordagem **SBU**.
* Se você for um *proprietário da Web/conteúdo*, escolha a abordagem **URL_DIR**.
* Se você for um *gerente de merchandising/ofertas*, escolha a abordagem **Categoria de produto/serviço**.

>[!IMPORTANT]
>
> * Escolha uma abordagem e siga-a.
> * Você pode ter apenas **um** modelo de Categoria por conta/marca. Não misture **SBU** e **URL_DIR** ao mesmo tempo.

Exemplo:

| Tipo de site | Categoria | Exemplos de taxonomia de tópico |
|---------|----------|---------|
| Empresas com várias empresas | SBU | pequeno conjunto de intenção (Como fazer, Solução de problemas, Comparação, Preços, Política) |
| Site pesado de documentação/suporte | URL_DIR | Como fazer, Solução de problemas, Referência, Notas de versão |
| Catálogo de comércio eletrônico/serviços | Produto/Serviço | Comparação, análises, preços/disponibilidade, instruções, solução de problemas |

### Práticas recomendadas para tópicos

Os tópicos ajudam você a entender a intenção do usuário - mostram o que o usuário deseja. Elas permitem agrupar prompts com intenções de usuário semelhantes. Pense nisso como um agrupamento de prompts relevantes juntos.

>[!IMPORTANT]
>
>Os tópicos são universais em **todas** categorias, o que significa que eles permanecem consistentes independentemente da categoria à qual estão atribuídos. Eles representam grupos de perguntas ou prompts que compartilham um propósito comum.

Ao decidir sobre tópicos, você deseja criar uma lista simples e curta (máximo de 6 a 12). Por exemplo:

* Produtos/Serviços
* Como fazer (configuração/uso)
* Solução de problemas (erros/problemas)
* Comparação (X vs Y; &quot;melhor ... para ...&quot;)
* Revisões e classificações
* Preços e disponibilidade
* Política e garantia
* Contato de suporte
* Corporativo / Notícias (se você realmente precisa deles)

Ao criar a lista, considere o seguinte:

* Um editor pode entender o tópico em 5 segundos a partir do texto do prompt? Caso contrário, renomeie/simplifique.
* Uma equipe diferente será responsável pela correção de tópicos diferentes? Em caso afirmativo, você escolheu tópicos úteis.

Algumas dicas úteis adicionais:

* Use o conhecimento da sua empresa ou site para definir tópicos que se alinhem às metas estratégicas da sua marca
* Considere como sua marca se compara aos concorrentes em tópicos específicos.

>[!IMPORTANT]
>
> * Mantenha os tópicos com base na intenção, não organizacional.
> * Não adicione categorias/filtros para marca/não marca/geográfico, pois você pode filtrar especificamente na guia **Marcas**.
> * Os tópicos estão distribuídos em várias categorias. Você pode **não** ter tópicos diferentes por categoria.
> * Um único prompt pode existir em vários tópicos ou categorias.

### Práticas recomendadas para prompts

Os prompts identificam as perguntas ou consultas específicas que os clientes estão fazendo, o que pode afetar seus negócios. Elas são as perguntas ou consultas reais que os usuários informam nos LLMs.

Certifique-se de revisar e atualizar os prompts regularmente para garantir que eles se alinhem às necessidades do cliente e às metas de negócios.

>[!TIP]
>
>* Você pode usar ferramentas como o LLM Optimizer e o Google Search Console com filtros de regex para identificar estruturas de perguntas comuns (por exemplo, &quot;como&quot;, &quot;o que&quot;, &quot;quando&quot;, &quot;onde&quot;).
>* Para descobrir quais prompts são relevantes para seu site/marca, você pode usar dados de pesquisa no site, perguntas frequentes nas páginas de resultados do mecanismo de pesquisa ou até mesmo perguntar aos chatbots do LLM diretamente quais perguntas os clientes podem fazer sobre sua marca.

### Práticas recomendadas para os concorrentes

Os concorrentes permitem que você monitore a visibilidade e faça menções nas respostas do LLM a prompts e tópicos importantes para sua empresa.

A guia [!UICONTROL **Rastreamento de Concorrente**] permite que você adicione concorrentes e rastreie sua visibilidade para prompts e tópicos específicos.

Com o rastreamento de concorrentes, você pode ver com que frequência os concorrentes são mencionados junto com sua marca em diferentes regiões e categorias e comparar sua visibilidade com a sua.

>[!TIP]
>
>Analise regularmente as menções e citações de concorrentes para identificar áreas em que sua marca pode melhorar.

## Painel Configuração do cliente

O Painel de configuração do cliente é uma ferramenta poderosa que fornece insights sobre a visibilidade da sua marca em LLMs. Ao configurar corretamente categorias, tópicos, prompts e concorrentes, você pode garantir que sua marca esteja bem posicionada para aparecer em respostas geradas pelo LLM. A análise regular de insights como Compartilhamento de voz, visibilidade de conteúdo e oportunidades ajudará você a adaptar sua estratégia e a ficar à frente dos concorrentes.

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

