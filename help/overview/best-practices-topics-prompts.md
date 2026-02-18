---
title: Práticas recomendadas para categorias, tópicos, prompts e outros
description: Otimize os insights do LLM ao configurar categorias, tópicos, prompts e outras marcas para acompanhar, incluindo concorrentes, para o monitoramento personalizado da marca e a análise de conteúdo estratégica.
feature: Best Practices, Customer Configuration
source-git-commit: f6d33387337ca097747407099891cbc6b586b9bb
workflow-type: ht
source-wordcount: '1435'
ht-degree: 100%

---


# Práticas recomendadas para configurar categorias, tópicos, prompts e outros para acompanhar

Esta seção descreve as práticas recomendadas para decidir como configurar categorias, tópicos, prompts e outros para acompanhar. Além disso, inclui informações sobre a biblioteca de prompts do setor, desenvolvida pela Adobe através de extensa pesquisa junto a especialistas do setor.

Este é um primeiro passo importante. O que é decidido agora determina como as informações serão adaptadas ao seu contexto de negócios. Qualquer alteração futura nas categorias redefine os dados históricos.

O painel [[!UICONTROL Configuração do cliente]](/help/dashboards/customer-configuration.md) é onde ocorre a definição de como a marca será monitorada e analisada na plataforma LLM Optimizer. Consulte [[!UICONTROL Configuração do cliente]](/help/dashboards/customer-configuration.md) para obter informações sobre como usar o painel.

![Janela Configuração do cliente](/help/assets/best-practices/customer-configuration-best-practices.png)

No painel [!UICONTROL Configuração do cliente], é possível personalizar categorias (como unidades de negócios ou linhas de produtos), monitorar outras marcas e adicionar aliases de menção da marca para capturar todas as variações de sua marca nos prompts. Essa configuração garante que a plataforma personalize insights para o contexto empresarial, permitindo visibilidade, tráfego e análise de oportunidades precisos.

## Biblioteca de prompts do setor

Para ajudar na introdução a prompts e tópicos, a Adobe criou uma biblioteca de prompts do setor, desenvolvida por meio de pesquisas abrangentes com especialistas do setor e análise do comportamento em pesquisas com IA de mais de 6.000 clientes. Esta biblioteca identifica os tópicos e prompts mais relevantes com base em tendências específicas do setor, objetivos comerciais validados e padrões de pesquisa de clientes do mundo real.

Para usar a biblioteca de prompts do setor:

1. Navegue até o painel **Configuração do cliente**.
1. Selecione **Baixar biblioteca de prompts** para baixar o arquivo da biblioteca do LLM Optimizer.
   ![Download da biblioteca de prompts do setor](/help/assets/best-practices/customer-configuration-prompts-library.png)
1. Revise os **Tópicos** e **Prompts** sugeridos para o setor da marca na respectiva guia e escolha as opções mais relevantes.
1. Revise a **coluna Estágio da jornada do cliente** para visualizar as opções de prompt no ciclo de vida do cliente (por exemplo: descoberta para conversão e para retenção). Os prompts de estágio inicial/topo do funil têm alta prioridade, mas também considere opções de estágio posterior para promover a retenção, habilitar o suporte ao cliente e assim por diante.
1. Modifique os tópicos ou prompts conforme necessário, para obter o melhor suporte de suas metas e objetivos, antes de fazer upload deles para o Adobe LLM Optimizer (por exemplo: adicione o nome da marca/produto e terminologia consistente com a marca). Os prompts podem ser adicionados ao LLM Optimizer manualmente ou por meio de upload em massa, usando o modelo *.csv* fornecido.

>[!TIP]
>
> Use uma combinação de prompts específicos do domínio recomendados pelo LLM Optimizer durante a configuração inicial e a biblioteca de prompts do setor, para preparar a estratégia de prompts.

### Fundação da pesquisa da biblioteca de prompts

A biblioteca de prompts do setor foi desenvolvida por meio de uma iniciativa de pesquisa abrangente que combina:

* **Customer intelligence:** análise do comportamento e das preferências na pesquisa com IA de mais de 6.000 clientes
* **Experiência no setor:** perspectivas de especialistas nos setores automotivo, serviços financeiros, saúde, telecomunicações e turismo.
* **Insights orientados por dados:** identificação de tópicos e padrões de consulta de alto impacto que impulsionam o engajamento e a conversão do cliente.

Principais tópicos pesquisados por clientes nos setores:

* **Automotivo:** solução de problemas automotivos, comparação de veículos e financiamento/leasing
* **Serviços financeiros:** pesquisa de produtos financeiros
* **Saúde:** busca de sintomas ou problemas de saúde, comparação de opções de tratamento, compreensão de resultados de laboratório ou termos médicos
* **Telecomunicações:** comparação de planos, termos contratuais e promoções, verificar o serviço no local
* **Turismo:** preparação para viagem, pesquisa e reserva de viagens

Tendências do cliente em pesquisas com IA e comportamento de prompt nas ferramentas LLM:

* Os clientes preferem fazer perguntas e não usar as palavras-chave ao utilizar as ferramentas de pesquisa LLM.
* Eles usam as ferramentas de pesquisa LLM principalmente para pesquisa e descoberta em estágio inicial.
* Os clientes tendem a mencionar uma marca ou nome de produto específico em seus prompts.

## Práticas recomendadas para categorias

As categorias permitem organizar o conteúdo em unidades estratégicas de negócios ou agrupamentos lógicos. Elas são o bloco “onde o item pertence” e a estrutura organizacional de nível superior do conteúdo.

Ao decidir como configurar categorias, é necessário considerar suas metas e quem precisa agir de acordo com o que está relatando.

>[!IMPORTANT]
>
> Verifique se as categorias estão configuradas corretamente desde o início, já que alterações nas categorias redefinem os dados históricos. Isso significa que, se alterá-las, perderá dados históricos anteriores à alteração.

Esta é uma visão geral dos tipos de abordagens possíveis de realizar e quando escolher uma abordagem específica:

| Abordagem | Descrição | Benefício |
|---------|----------|---------|
| Unidade estratégica de negócios (SBU) | Use essa abordagem se a organização for dividida por unidade de negócio (por exemplo: Consumidor, Empresas, Serviços). | Você obterá relatórios claros para cada linha de negócios e facilitará a prestação de contas. |
| Diretório de nível superior do site (URL_DIR) | Use se a arquitetura de informações do site refletir a propriedade (/products/, /support/, /docs/, /news/). | Isso fornecerá alinhamento com a forma como as equipes publicam e mantêm conteúdo. |
| Categoria do produto (ou serviço) | Use-a caso venda um catálogo (SKUs/serviços). | Você receberá visualizações de portfólio, análise de lacuna e respostas para a pergunta “qual categoria precisa de conteúdo?”. |

A decisão sobre como configurar categorias se baseia em uma pergunta: **Quem precisa agir no relatório?**

* Se você for *líder de negócios*, escolha a abordagem **SBU**.
* Se você for *proprietário(a) de conteúdo/da web*, escolha a abordagem **URL_DIR**.
* Se você for *gerente de merchandising/ofertas*, escolha a abordagem **Categoria do produto/serviço**.

![Adição de categorias no LLM Optimizer](/help/assets/best-practices/add-category.png)

>[!IMPORTANT]
>
> * Escolha uma abordagem e siga-a.
> * É possível ter apenas **um** modelo de categoria por conta/marca. Não misture **SBU** e **URL_DIR** ao mesmo tempo.
<!--Can you mix Product/Service with these?-->

Exemplo:

| Tipo de site | Categoria | Exemplos de taxonomia de tópico |
|---------|----------|---------|
| Corporações com vários negócios | SBU | Pequeno conjunto de intenções (tutorial, solução de problemas, comparação, preços, política) |
| Site com foco em documentação/suporte | URL_DIR | Tutorial, solução de problemas, referência, notas de versão |
| Catálogo de comércio eletrônico/serviços | Produto/serviço | Comparação, análises, preços/disponibilidade, tutorial, solução de problemas |

## Práticas recomendadas para tópicos

Os tópicos ajudam a compreender a intenção do usuário. Eles mostram o que o usuário deseja. Eles permitem agrupar prompts com intenções do usuário semelhantes. Pense nisso como um conjunto de prompts relevantes.

>[!IMPORTANT]
>
>Os tópicos são universais em **todas** as categorias, o que significa que eles permanecem consistentes independentemente da categoria à qual estão atribuídos. Eles representam grupos de perguntas ou prompts que compartilham uma intenção em comum.

Ao decidir sobre os tópicos, crie uma lista simples e curta (máximo de 6 a 12). Por exemplo:

* Produtos/serviços
* Guia (configuração/uso)
* Solução de problemas e erros
* Comparação (X vs. Y; “melhor ... para ...”)
* Revisões e classificações
* Preços e disponibilidade
* Política e garantia
* Contato com o suporte
* Corporativo/notícias (se realmente precisar disso)

![Adição de tópicos no LLM Optimizer](/help/assets/best-practices/add-topic.png)

Ao criar a lista, considere o seguinte:

* Um editor pode entender o tópico em 5 segundos a partir do texto do prompt? Caso contrário, renomeie e simplifique.
* Uma equipe diferente será responsável pela correção de tópicos diferentes? Em caso afirmativo, você escolheu tópicos úteis.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algumas dicas úteis adicionais:

* Use o conhecimento da sua empresa ou site para definir tópicos que se alinhem às metas estratégicas da marca
* Considere como sua marca se compara a outras marcas em tópicos específicos.

>[!IMPORTANT]
>
> * Mantenha os tópicos baseados na intenção e não na organização.
> * Não adicione categorias e filtros para “marcas”, “sem marca” “regiões”, pois há filtros específicos para isso na guia **[!UICONTROL Marcas]**.
> * Os tópicos estão distribuídos em várias categorias. **Não é possível** definir tópicos únicos para cada categoria.
> * Um único prompt **pode** existir em vários tópicos ou categorias.

## Práticas recomendadas para prompts

Os prompts identificam as perguntas ou consultas específicas que clientes estão fazendo, o que pode afetar seus negócios. Estes são as perguntas ou consultas reais que os usuários inserem nos LLMs.

Certifique-se de revisar e atualizar os prompts regularmente para garantir que eles se alinhem às necessidades do cliente e às metas de negócios.

Práticas recomendadas para prompts:

* Agrupe prompts semelhantes com base no que as pessoas estão perguntando.
* Concentre-se nos prompts que são mais importantes para os clientes.
* Verifique se a marca tem uma boa chance de ser mencionada em determinados prompts.

>[!TIP]
>
>* É possível usar ferramentas como o Adobe LLM Optimizer e o Google Search Console com filtros de regex para identificar estruturas de perguntas comuns (por exemplo: “como”, “o que”, “quando”, “onde”) e descobrir quais prompts as pessoas estão usando para visitar o site.
>* Para descobrir quais prompts são relevantes para o site ou marca, é possível usar dados de pesquisa no site, perguntas frequentes nas páginas de resultados do mecanismo de pesquisa ou até mesmo perguntar aos chatbots do LLM diretamente quais perguntas os clientes podem fazer sobre a marca.

## Práticas recomendadas para monitorar outras marcas

A guia “Monitorar outros” permite monitorar a visibilidade e as menções em respostas do LLM, de prompts e tópicos importantes para os negócios.

A guia [!UICONTROL **Monitorar outros**] permite adicionar outros, incluindo concorrentes, para monitorar sua visibilidade em prompts e tópicos específicos.

Com a guia “Monitorar outros”, é possível ver com que frequência outras marcas são mencionadas junto à sua marca em diferentes regiões e categorias e comparar a visibilidade delas com a sua.

>[!TIP]
>
>Analise regularmente menções e citações de concorrentes ou de outros para identificar áreas em que sua marca pode melhorar.

## Saiba mais

* O [painel Configuração do cliente](/help/dashboards/customer-configuration.md) é o local para configurar categorias, tópicos, prompts e o monitoramento de outros.
* As [Práticas recomendadas do LLM Optimizer](/help/tutorials/best-practices.md) descrevem as práticas recomendadas para otimização de LLM

