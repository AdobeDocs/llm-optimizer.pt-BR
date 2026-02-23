---
title: Configuração do cliente
description: Use a configuração do cliente para definir como a marca será monitorada e analisada na plataforma do LLM Optimizer.
feature: Customer Configuration
source-git-commit: 3fab5f21311a741e51e7a31cd3a26de79fcbff95
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 40%

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
* [Google Search Console](#google-console)

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

Para excluir um alias de marca, clique no ícone **Excluir** da lista de alias.

## Configuração da CDN {#cdn-configuration}

Nessa guia, é possível configurar os fluxos da CDN para permitir que o Adobe LLM Optimizer analise os dados da CDN. Esses dados serão usados para alimentar painéis (como o tráfego agêntico), fornecendo insights sobre padrões de tráfego, métricas de desempenho e oportunidades de otimização. Para integrar o provedor da CDN, clique em **Integrar CDN**.

![CDN de configuração do cliente](/help/overview/assets/cc-cdn.png)

Na janela **Integrar provedor da CDN**:

1. Selecione o provedor da CDN.
2. Clique em **Integrar** para habilitar o encaminhamento de logs.

Caso selecione **Outro**, entre em contato com llmo-now@adobe.com para obter ajuda.

## Google Search Console {#google-console}

O Adobe LLM Optimizer permite integrar sua conta do Google Search Console para trazer consultas de pesquisa reais diretamente para a interface. Ao descobrir consultas reais do Google Search Console, você pode criar conjuntos de prompts baseados no comportamento de pesquisa real e nos padrões de descoberta de alta intenção. Isso ajuda a priorizar solicitações com base na demanda comprovada e alinha os esforços de otimização do LLM à forma como os usuários fazem a pesquisa no momento. Além disso, você permanece no controle total, pois as consultas nunca são adicionadas automaticamente e devem ser explicitamente selecionadas antes de se tornarem prompts ativos.

### Como funciona {#how-it-works}

O principal a ser lembrado sobre a integração entre o LLM Optimizer e o Google Search Console é o seguinte: em vez de adivinhar manualmente o que os clientes podem pedir a um assistente de IA, observamos o que eles **já estão procurando** e transformamos essas consultas reais em prompts naturais e conversacionais. Esse processo de mudança de consultas de pesquisa para prompts de IA é exemplificado no diagrama abaixo.

![Fluxo do processo](/help/dashboards/assets/diagram-flow.png)

De modo geral, o processo tem cinco etapas:

#### Etapa 1 — Coletar os dados de pesquisa reais {#gsc-one}

O processo começa com as palavras-chave que seu público-alvo está realmente usando quando encontra seu site por meio do Google. Esse conjunto de dados brutos (geralmente milhares de consultas exclusivas) é a base de tudo o que se segue.

#### Etapa 2 — analisar o significado e o filtro para a segurança {#gsc-two}

Cada consulta é analisada por seu significado semântico (sobre o que o usuário realmente está perguntando) e filtrada por um filtro de segurança que remove conteúdo inadequado ou fora da marca. Isso garante que somente palavras-chave limpas e relevantes avancem.

#### Etapa 3 — Agrupar em categorias e tópicos {#gsc-three}

As consultas relacionadas são automaticamente agrupadas em **categorias** (temas empresariais amplos) e **tópicos** (subtópicos focalizados em cada categoria). O sistema prioriza categorias que já estão configuradas na configuração do LLM Optimizer. Além disso, ele também pode exibir novas categorias reveladas pelos dados de pesquisa, mas que ainda não estão sendo monitoradas. O diagrama a seguir é um exemplo de categorias e tópicos para uma marca de mobília:

![Marca de Mobília](/help/dashboards/assets/diagram-example.png)

#### Etapa 4 — Gerar prompts com base em palavras-chave reais {#gsc-four}

Para cada tópico, o sistema gera prompts semelhantes à forma como as pessoas reais conversam com os assistentes de IA. Cada prompt é diretamente influenciado por palavras-chave de pesquisa reais do Google Search Console, transformando a intenção de palavra-chave em perguntas de conversação naturais.

Essa abordagem (baseada em palavras-chave) significa:

* Os prompts refletem a demanda real, não questões hipotéticas.
* O idioma reflete como seus clientes realmente formulam as coisas.
* A cobertura abrange toda a amplitude do que as pessoas pesquisam no seu site.

A geração de prompts também considera o perfil da sua marca, incluindo produtos, concorrentes, posicionamento do setor e público-alvo, para garantir que os prompts sejam contextualmente precisos.

#### Etapa 5 - Garantia de qualidade e entrega {#gsc-five}

Antes da entrega, cada prompt passa por várias verificações de qualidade automatizadas:

* Desduplicação — prompts quase idênticos são removidos.
* Equilíbrio de proporção de marca — garante uma combinação realista (aproximadamente 75% sem marca, ~25% com marca).
* Qualidade da linguagem — desmonta frases robóticas de modo que incita o som natural.
* Verificações de consistência — valida datas, remove frases de preenchimento e garante uma duração concisa.

Além disso, cada prompt é marcado com sua categoria, tópico, tipo de intenção e classificação com/sem marca, pronto para o LLM Optimizer começar a monitorar.

#### Anatomia do Prompt {#prompt-anatomy}

Após a conclusão do processo acima, cada prompt entregue ao LLM Optimizer terá os seguintes atributos:

| Texto | Descrição |
|---------|----------|
| Texto | O prompt, semelhante a como um usuário o digitaria em um assistente de IA |
| Categoria | O tema de negócios amplo atribuído a este prompt. |
| Tópico | O subtópico específico dentro da categoria. |
| Região | O mercado alvo (por exemplo, EUA, Reino Unido e assim por diante). |
| Intenção | A mentalidade do usuário: informativa, comparativa, transacional, instrutiva, de planejamento ou delegação. |
| Tipo | O tipo pode ser de marca (menciona a marca/produtos) ou sem marca (questão genérica do setor). |

### Como usar {#how-to-use}

Siga as etapas apresentadas abaixo para integrar e usar as consultas do Google Search Console com o LLM Optimizer.

#### Conectar o Google Search Console {#connect-console}

Antes de usar esse recurso, é necessário integrar sua conta do Google Search Console ao LLM otimizer.

1. Abra o painel Configuração do cliente.
1. Navegue até a guia Google Search Console e clique em **Conectar conta**.
   ![Console do Google Search](/help/dashboards/assets/google-console.png)
1. Faça logon com uma conta do Google que tenha acesso à propriedade do Console de pesquisa desejada.
   ![Conta do Google](/help/dashboards/assets/google-account.png)
1. Escolha a propriedade que deseja conectar.
   ![Propriedade do Console](/help/dashboards/assets/console-property.png)
1. Após a conclusão da conexão, o LLM Optimizer começa a recuperar consultas de pesquisa relevantes.
   ![Recuperando Dados](/help/dashboards/assets/console-complete.png)

#### Revisar e pesquisar consultas {#search-query}

Depois de integrar a conta do Google Search Console ao otimizador do LLM, você pode revisar a lista de tópicos e prompts originados do console de pesquisa e adicionar os prompts da lista.

1. Na guia Google Search Console, revise a lista de tópicos e prompts originados no Search Console.
   ![Lista de Solicitações](/help/dashboards/assets/prompts-list.png)
1. Clique na categoria de tópico/prompt desejada para expandir a lista.
1. Use o botão **Adicionar** para adicionar prompts da lista. Você também pode adicionar prompts e categorias em massa usando **Adicionar tudo**.
   ![Adicionar Prompts](/help/dashboards/assets/add-prompts.png)
1. Quando estiver satisfeito com a seleção, clique em **Salvar** na mensagem de notificação.

#### Exibir consultas adicionadas na lista Prompts {#prompts-list}

Depois que uma consulta é adicionada, ela aparece na guia [Prompts](#prompts-brand) no painel Configuração do cliente. Os prompts originados do Google Search Console são marcados com um ícone do Google Search Console na coluna **Origin**. O ícone ajuda a distinguir entre prompts baseados no comportamento de pesquisa do usuário real daqueles adicionados manualmente ou de outras fontes.

### Perguntas frequentes {#gsc-faq}

P: Com que frequência os prompts são atualizados no painel do Google Search Console?

Os prompts originados no Google Search Console geralmente são atualizados uma vez por mês. Cada atualização extrai os dados de consulta de pesquisa mais recentes do Console de pesquisa do Google, executa novamente o pipeline de geração e atualiza o conjunto de prompts. Isso garante que seus prompts permaneçam alinhados às tendências de pesquisa atuais e às mudanças sazonais no comportamento do usuário.

P: Quantos prompts normalmente são originados no Google Search Console?

O número depende do tamanho da implantação e da quantidade de categorias rastreadas. Por exemplo:

| Categorias | Total de tópicos | Solicitações Entregues |
|---------|----------|----------|
| 1-2 | 3-8 | ~65-180 |
| 4-5 | 12-20 | ~270-450 |
| 10 | 30-40 | ~675-900 |

Nosso objetivo é fornecer conjuntos de solicitações que atendam às metas de qualidade comunicadas durante a avaliação e a integração: pelo menos 20 solicitações por tópico, com 3 a 4 tópicos por categoria e um equilíbrio saudável de marca/sem marca.

P: Quando verei os prompts originados no Google Search Console depois que eu me conectar ao Google Search Console?

Geralmente, os prompts estão disponíveis **dentro de algumas horas** após a conexão do Console de Pesquisa do Google ser estabelecida. O pipeline extrai automaticamente os dados de pesquisa, processa esses dados pelas etapas de geração e controle de qualidade e fornece o prompt final definido para o LLM Optimizer.

P: Quem pode se conectar ao Google Search Console?

Qualquer pessoa com **Proprietário** ou **Permissão Completa** na propriedade do Console de Pesquisa do Google pode autorizar a conexão. Esses são os níveis de permissão que concedem acesso de leitura aos dados de consulta de pesquisa. Se não tiver certeza sobre o seu nível de permissão, você poderá verificá-lo em **Configurações>Usuários** e permissões no Console do Google Search.

P: Posso marcar os prompts como ignorados ou ignorados para que eu não os veja na lista de prompts do Google Search Console?

Sim, você pode excluir qualquer prompt que não deseja monitorar. Os prompts excluídos são removidos da sua lista de prompts ativa e não aparecerão em relatórios futuros. Se um prompt excluído for gerado novamente em uma atualização mensal subsequente, você poderá removê-lo novamente.

P: Depois que eu adicionar prompts do Console do Google Search à minha lista de prompts, dentro de quanto tempo eu verei os dados de Presença da marca desses prompts?

Os dados de presença da marca para prompts adicionados recentemente serão exibidos durante a próxima atualização de dados programada, que normalmente é executada no início de cada semana. Dependendo de quando você adicionar os prompts, poderá ver os resultados em alguns dias.
