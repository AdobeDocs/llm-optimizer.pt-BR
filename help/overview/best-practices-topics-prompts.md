---
title: Práticas recomendadas para categorias, tópicos, prompts e outros
description: Otimize os insights do LLM configurando categorias, tópicos, prompts e outras marcas para rastrear, incluindo concorrentes para o monitoramento personalizado da marca e a análise estratégica de conteúdo.
feature: Best Practices, Customer Configuration
source-git-commit: a4dd9b1aece2936fb95a2e831ec8b41946bc5f46
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Práticas recomendadas para configurar categorias, tópicos, prompts e outros para rastrear

Esta seção descreve as práticas recomendadas para decidir como você deseja configurar suas categorias, tópicos, prompts e outros para rastrear. Além disso, inclui informações sobre a Industry Prompt Library, desenvolvida pela Adobe com extensa pesquisa com especialistas do setor.

Este é um primeiro passo vital. O que você decide agora determina como as informações são adaptadas ao seu contexto de negócios. Quaisquer alterações em categorias no futuro redefinirão os dados históricos.

O painel [[!UICONTROL Configuração do cliente]](/help/dashboards/customer-configuration.md) é onde você define como sua marca será monitorada e analisada na plataforma do otimizador de LLM. Consulte [[!UICONTROL Configuração do cliente]](/help/dashboards/customer-configuration.md) para obter informações sobre como usar o painel.

![Janela de configuração do cliente](/help/assets/best-practices/customer-configuration-best-practices.png)

No painel [!UICONTROL Configuração do cliente], você pode personalizar categorias (como unidades de negócios ou linhas de produtos), rastrear outras marcas e adicionar aliases de menção à marca para capturar todas as variações da sua marca em prompts. Essa configuração garante que a plataforma personalize insights para o contexto comercial, permitindo uma visibilidade precisa, tráfego e análise de oportunidades.

## Biblioteca de prompts do setor

Para ajudar a começar a usar prompts e tópicos, a Adobe criou uma Biblioteca de Prompts do Setor desenvolvida por meio de pesquisas abrangentes com especialistas do setor e análise do comportamento de pesquisa de IA em mais de 6.000 clientes. Essa biblioteca identifica os tópicos e prompts mais relevantes com base em tendências específicas do setor, objetivos de negócios validados e padrões de pesquisa de clientes reais.

Para usar a Biblioteca de prompts do setor:

1. Baixe o arquivo da Biblioteca de Prompts da LLM Optimizer navegando até o painel **Configuração do cliente**.
2. Revise os **Tópicos** e **Solicitações** sugeridos para o setor da sua marca na respectiva guia. Escolha as opções que forem mais relevantes.
3. Revise a **coluna Estágio de Jornada do cliente** para visualizar as opções de prompt no ciclo de vida do cliente (por exemplo, descoberta para conversão em retenção). Os prompts de estágio inicial/início do funnel têm alta prioridade, mas também consideram opções de estágio posterior para promover a retenção, habilitar o suporte ao cliente e assim por diante.
4. Modifique tópicos ou prompts, conforme necessário, para melhor suportar suas metas e objetivos, antes de fazer upload para a Adobe LLM Optimizer (por exemplo, adicione o nome da sua marca/produto, adicione a terminologia na marca). Os prompts podem ser adicionados manualmente ao LLMO ou carregados em massa usando o modelo *.csv* fornecido.

>[!TIP]
>
> Use uma combinação de prompts específicos do domínio recomendados pela LLM Optimizer durante a configuração inicial e a Biblioteca de prompts do setor para preparar sua estratégia de prompt.

### Prompt Library Research Foundation (Fundação de pesquisa da biblioteca de solicitações)

A Industry Prompt Library foi desenvolvida por meio de uma iniciativa de pesquisa abrangente que combina:

* **Inteligência do cliente:** análise do comportamento e das preferências de pesquisa de IA em mais de 6.000 clientes
* **Experiência do setor:** perspectivas de especialistas nos setores de Automóvel, Serviços Financeiros, Saúde, Telecom e Viagens.
* **Insights orientados por dados:** identificação de tópicos e padrões de consulta de alto impacto que impulsionam a participação e a conversão do cliente.

Principais tópicos pesquisados por clientes em todos os setores:

* **Automático:** Solução de problemas automáticos, Comparação de veículos e Financiamento/Leasing
* **Serviços Financeiros:** Pesquisando produtos financeiros
* **Assistência médica:** Buscando sintomas ou problemas de saúde, Comparando opções de tratamento, Compreender resultados de laboratório ou termos médicos
* **Telecom:** Comparando planos, termos de contrato e promoções, Verificando o serviço na área local
* **Viagem:** Preparação para uma viagem, Pesquisa e reserva de viagem

Tendências do cliente em relação à pesquisa de IA e ao comportamento de prompt nas ferramentas do LLM:

* Os clientes preferem fazer perguntas e não usar palavras-chave ao usar as ferramentas de pesquisa do LLM.
* Eles usam principalmente ferramentas de pesquisa LLM para pesquisa e descoberta em fase inicial.
* Os clientes tendem a mencionar uma marca ou nome de produto específico em seus prompts.

## Práticas recomendadas para categorias

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

![Adicionando categorias no LLM Optimizer](/help/assets/best-practices/add-category.png)

>[!IMPORTANT]
>
> * Escolha uma abordagem e siga-a.
> * Você pode ter apenas **um** modelo de Categoria por conta/marca. Não misture **SBU** e **URL_DIR** ao mesmo tempo.
<!--Can you mix Product/Service with these?-->

Exemplo:

| Tipo de site | Categoria | Exemplos de taxonomia de tópico |
|---------|----------|---------|
| Empresas com várias empresas | SBU | Pequeno conjunto de intenção (procedimentos, solução de problemas, comparação, preços, política) |
| Site pesado de documentação/suporte | URL_DIR | Como fazer, Solução de problemas, Referência, Notas de versão |
| Catálogo de comércio eletrônico/serviços | Produto/Serviço | Comparação, análises, preços/disponibilidade, instruções, solução de problemas |

## Práticas recomendadas para tópicos

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
* Corporativo/Notícias (se você realmente precisar disso)

![Adicionando tópicos no LLM Optimizer](/help/assets/best-practices/add-topic.png)

Ao criar a lista, considere o seguinte:

* Um editor pode entender o tópico em 5 segundos a partir do texto do prompt? Caso contrário, renomeie/simplifique.
* Uma equipe diferente será responsável pela correção de tópicos diferentes? Em caso afirmativo, você escolheu tópicos úteis.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Algumas dicas úteis adicionais:

* Use o conhecimento da sua empresa ou site para definir tópicos que se alinhem às metas estratégicas da sua marca
* Considere a comparação de sua marca com outras marcas em tópicos específicos.

>[!IMPORTANT]
>
> * Mantenha os tópicos com base na intenção, não organizacional.
> * Não adicione categorias/filtros para marca/não marca/geográfico, pois você pode filtrar especificamente na guia **[!UICONTROL Marcas]**.
> * Os tópicos estão distribuídos em várias categorias. Você **não pode** definir tópicos exclusivos para cada categoria.
> * Um único prompt **pode** existe em vários tópicos ou categorias.

## Práticas recomendadas para prompts

Os prompts identificam as perguntas ou consultas específicas que os clientes estão fazendo, o que pode afetar seus negócios. Elas são as perguntas ou consultas reais que os usuários informam nos LLMs.

Certifique-se de revisar e atualizar os prompts regularmente para garantir que eles se alinhem às necessidades do cliente e às metas de negócios.

Práticas recomendadas para prompts:

* Agrupe prompts semelhantes com base no que as pessoas estão perguntando.
* Concentre-se nos prompts que são mais importantes para seus clientes.
* Verifique se a sua marca tem uma boa chance de ser mencionada em determinados prompts.

>[!TIP]
>
>* Você pode usar ferramentas como o Adobe LLM Optimizer e o Google Search Console com filtros de regex para identificar estruturas de perguntas comuns (por exemplo, &quot;como&quot;, &quot;o que&quot;, &quot;quando&quot;, &quot;onde&quot;) e descobrir quais prompts as pessoas estão usando para visitar seu site.
>* Para descobrir quais prompts são relevantes para seu site/marca, você pode usar dados de pesquisa no site, perguntas frequentes nas páginas de resultados do mecanismo de pesquisa ou até mesmo perguntar aos chatbots do LLM diretamente quais perguntas os clientes podem fazer sobre sua marca.

## Práticas recomendadas para rastrear outras marcas

O rastreamento de Outros permite monitorar a visibilidade e menções em respostas LLM para prompts e tópicos importantes para sua empresa.

A guia [!UICONTROL **Others Tracking**] permite adicionar outros, incluindo concorrentes, para rastrear sua visibilidade de prompts e tópicos específicos.

Com outros rastreadores, você pode ver com que frequência outras marcas são mencionadas ao lado da sua marca em diferentes regiões e categorias e comparar sua visibilidade com a sua.

>[!TIP]
>
>Analise regularmente menções e citações de concorrentes ou de outros para identificar áreas em que sua marca pode melhorar.

## Saiba mais

* O [painel de Configuração do Cliente](/help/dashboards/customer-configuration.md) é onde você configura suas categorias, tópicos, prompts e outros controles.
* [Práticas recomendadas da LLM Optimizer](/help/tutorials/best-practices.md) descreve as práticas recomendadas para a otimização de LLM

