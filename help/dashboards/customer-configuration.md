---
title: Configuração do cliente
description: Use a configuração do cliente para definir como a marca será monitorada e analisada na plataforma do LLM Optimizer.
feature: Customer Configuration
autotag-review: '2026-05-15T17:45:12.067Z'
TQID: 'https://experienceleague.adobe.com/qa7zk54n9G19-Azz9f6mn7V1kAGvnJSOJjpxbTBeHgc'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: e69d5a42-0217-4ca5-9396-a9a826a170da
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: f16c1bda1c9919a62077811653f92d5fc2c74045
workflow-type: tm+mt
source-wordcount: 3935
ht-degree: 57%

---


# Configuração do cliente {#customer-configuration}

O painel Configuração do cliente é uma ferramenta poderosa que fornece insights sobre a visibilidade da marca em LLMs. Ao configurar corretamente categorias, tópicos e prompts é possível garantir que a marca esteja bem posicionada para aparecer em respostas geradas pelo LLM. Essa configuração garante que a plataforma personalize insights para o contexto empresarial, permitindo visibilidade, tráfego e análise de oportunidades precisos.

O painel Configuração do cliente (mostrado abaixo) aplica-se caso sua organização ainda utilize esta navegação.

![Painel Configuração do cliente](/help/dashboards/assets/customer-config.png)

Para configurar como o LLM Optimizer monitora e analisa a presença da marca em diferentes mercados e cenários competitivos, você tem acesso às seguintes guias:

* [Prompts](#prompts-brand)
* [Categorias](#categories)
* [Outras marcas](#other-brands)
* [Aliases da marca](#brand-aliases)
* [Configuração da CDN](#agentic-cdn)
* [Google Search Console](#google-console)
* [Sugestões de prompt com base em Tentativas de Citação e Tráfego de referência](#prompt-suggestions)

Se você estiver na [Experiência centrada na marca](/help/overview/quick-start.md#brand-centric-experience), navegue até **Gerenciamento de marcas** para definir e configurar marcas, aliases de marcas e determinar os concorrentes a serem monitorados. O painel **Gerenciamento de marcas** também é usado para configurar integrações, como o Google Search Console, o Adobe Analytics e o encaminhamento de logs de CDN relacionados a URLs associados a marcas. Você pode fazer isso clicando nas guias correspondentes: GSC, CDN e assim por diante.

![Gerenciamento de marcas — navegação do aplicativo (Experiência centrada na marca)](/help/assets/brand-centric-experience/llmo-app-shell.png)

![Gerenciamento de marcas — visão geral da configuração (Experiência centrada na marca)](/help/assets/brand-centric-experience/brands-management-configuration.png)

>[!IMPORTANT]
>
> Para obter mais detalhes sobre como configurar categorias, tópicos e prompts, consulte a página [Práticas recomendadas para configurar categorias, tópicos e prompts](/help/overview/best-practices-topics-prompts.md).

## Prompts {#prompts-brand}

Na guia **Prompts**, você pode revisar, gerenciar e personalizar prompts. É possível fazer upload de um arquivo .csv de [Análise de presença da marca](/help/dashboards/brand-presence.md) e a lista será preenchida com prompts e tópicos dessa análise, ou [Baixar uma biblioteca de prompts](/help/overview/best-practices-topics-prompts.md) criada pela Adobe. Também é possível excluir, modificar e adicionar tópicos e seus prompts associados, conforme necessário.

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

Para clientes que estão na [Experiência centrada na marca](/help/overview/quick-start.md#brand-centric-experience), para adicionar Tópicos e Prompts, navegue até **Gerenciamento de prompts**.

![Gerenciamento de prompts (Experiência centrada na marca)](/help/assets/brand-centric-experience/prompts-management.png)

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

Para excluir um alias de marca, clique no ícone **Excluir** na lista de aliases.

## Configuração da CDN {#cdn-configuration}

Nessa guia, é possível configurar os fluxos da CDN para permitir que o Adobe LLM Optimizer analise os dados da CDN. Esses dados serão usados para alimentar painéis (como o tráfego agêntico), fornecendo insights sobre padrões de tráfego, métricas de desempenho e oportunidades de otimização. Para integrar o provedor da CDN, clique em **Integrar CDN**.

![CDN de configuração do cliente](/help/overview/assets/cc-cdn.png)

Na janela **Integrar provedor da CDN**:

1. Selecione o provedor da CDN.
2. Clique em **Integrar** para habilitar o encaminhamento de logs.

Caso selecione **Outro**, entre em contato com llmo-now@adobe.com para obter ajuda.

## Google Search Console {#google-console}

O Adobe LLM Optimizer permite integrar sua conta do Google Search Console para trazer consultas de pesquisa reais diretamente para a interface. Ao exibir consultas reais do Google Search Console, você pode criar conjuntos de prompts baseados no comportamento de pesquisa real e em padrões de descoberta de alta intenção. Isso ajuda você a priorizar os prompts com base na demanda comprovada e alinha os esforços de otimização do LLM com a forma como os usuários pesquisam atualmente. Além disso, você mantém o controle total, pois as consultas nunca são adicionadas automaticamente e devem ser selecionadas explicitamente antes de se tornarem prompts ativos.

### Como funciona {#how-it-works}

O mais importante que você deve lembrar sobre a integração entre o LLM Optimizer e o Google Search Console é o seguinte: em vez de adivinhar manualmente o que os clientes podem perguntar a um assistente de IA, analisamos o que eles **já estão pesquisando** e transformamos essas consultas reais em prompts naturais e conversacionais. Esse processo de transição de consultas de pesquisa para prompts de IA é exemplificado no diagrama abaixo.

![Fluxo do processo](/help/dashboards/assets/diagram-flow.png)

De modo geral, o processo tem cinco etapas:

#### Etapa 1: colete seus dados de pesquisa reais {#gsc-one}

O processo começa com as palavras-chave que seu público-alvo realmente usa quando encontra seu site pelo Google. Este conjunto de dados brutos (frequentemente milhares de consultas únicas) é a base para tudo o que se segue.

#### Etapa 2: analisar o significado e filtrar para garantir a segurança {#gsc-two}

Cada consulta é analisada quanto ao seu significado semântico (o que o usuário realmente está perguntando) e passa por um filtro de segurança que remove conteúdo inadequado ou que não esteja de acordo com a marca. Isso garante que apenas palavras-chave limpas e relevantes avancem.

#### Etapa 3: agrupe em categorias e tópicos {#gsc-three}

As consultas relacionadas são agrupadas automaticamente em **categorias** (temas comerciais amplos) e **tópicos** (subtópicos específicos dentro de cada categoria). O sistema prioriza as categorias que já estão definidas na configuração do LLM Optimizer. Além disso, também pode revelar novas categorias que seus dados de pesquisa indicam, mas que ainda não estão sendo monitoradas. O diagrama a seguir é um exemplo de categorias e tópicos de uma marca de móveis:

![Marca de móveis](/help/dashboards/assets/diagram-example.png)

#### Etapa 4: gerar prompts baseados em palavras-chave reais {#gsc-four}

Para cada tópico, o sistema gera prompts semelhantes à forma como pessoas reais conversam com assistentes de IA. Cada prompt é diretamente influenciado por palavras-chave de pesquisa reais do Google Search Console, transformando a intenção da palavra-chave em perguntas conversacionais naturais.

Com essa abordagem (baseada em palavras-chave):

* Os prompts refletem a demanda real, não questões hipotéticas.
* A linguagem reflete a forma como os clientes realmente se expressam.
* A cobertura abrange toda a gama de termos que as pessoas pesquisam no seu site.

A geração de prompts também leva em consideração o perfil da sua marca — incluindo produtos, concorrentes, posicionamento no setor e público-alvo — para garantir que os prompts sejam contextualmente precisos.

#### Etapa 5: controle de qualidade e entrega {#gsc-five}

Antes da entrega, cada prompt passa por diversas verificações de qualidade automatizadas:

* Desduplicação: prompts quase idênticos são removidos.
* Equilíbrio na proporção de marcas: garante uma combinação realista (aproximadamente 75% sem marca, aproximadamente 25% com marca).
* Qualidade da linguagem: elimina frases robóticas para que os prompts soem naturais.
* Verificações de consistência: valida datas, remove frases desnecessárias e garante um texto conciso.

Além disso, cada prompt é marcado com sua categoria, tópico, tipo de intenção e classificação de marca/sem marca, pronto para que o LLM Optimizer comece a monitorar.

#### Anatomia do prompt {#prompt-anatomy}

Após a conclusão do processo acima, cada prompt enviado ao LLM Optimizer terá os seguintes atributos:

| Texto | Descrição |
|---------|----------|
| Texto | O prompt, semelhante à forma como um usuário o digitaria em um assistente de IA, é apresentado |
| Categoria | O tema empresarial geral atribuído a este prompt. |
| Tópico | O subtópico específico dentro da categoria. |
| Região | O mercado-alvo (por exemplo, EUA, Reino Unido etc.). |
| Intenção | A mentalidade do usuário: informativa, comparativa, transacional, instrutiva, de planejamento ou delegação. |
| Tipo | O tipo pode ser com marca (menciona a marca/produtos) ou sem marca (questão genérica do setor). |

### Como usar {#how-to-use}

Siga as etapas apresentadas abaixo para integrar e usar as consultas do Google Search Console com o LLM Optimizer.

#### Conectar o Google Search Console {#connect-console}

Antes de usar esse recurso, é necessário integrar sua conta do Google Search Console ao LLM Optimizer.

1. Abra o painel **Configuração do cliente** (navegação clássica) ou o **Gerenciamento de marcas** (experiência centrada na marca) e vá para a integração do Google Search Console (tag GSC na experiência centrada na marca).
1. Navegue até a guia Google Search Console e clique em **Conectar conta**.
   ![Google Search Console](/help/dashboards/assets/google-console.png)
1. Faça logon com uma conta do Google que tenha acesso à propriedade do Search Console desejada.
   ![Conta do Google](/help/dashboards/assets/google-account.png)
1. Escolha a propriedade que deseja conectar.
   ![Propriedade do console](/help/dashboards/assets/console-property.png)
1. Após a conclusão da conexão, o LLM Optimizer começa a recuperar consultas de pesquisa relevantes.
   ![Recuperação de dados](/help/dashboards/assets/console-complete.png)

#### Revisar e pesquisar consultas {#search-query}

Depois de integrar a conta do Google Search Console ao LLM Optimizer, você pode revisar a lista de tópicos e prompts originados do console de pesquisa e adicionar os prompts da lista.

1. Na guia Google Search Console, revise a lista de tópicos e prompts originados no Search Console.
   ![Lista de prompts](/help/dashboards/assets/prompts-list.png)
1. Clique na categoria de tópico/prompt desejada para expandir a lista.
1. Use o botão **Adicionar** para adicionar prompts da lista. Você também pode adicionar prompts e categorias em massa usando **Adicionar tudo**.
   ![Adicionar prompts](/help/dashboards/assets/add-prompts.png)
1. Quando estiver satisfeito com a seleção, clique em **Salvar** na mensagem de notificação.

#### Exibir consultas adicionadas na lista Prompts {#prompts-list}

Após a adição de uma consulta, ela aparece na guia [Prompts](#prompts-brand), no painel Configuração do cliente (navegação clássica) ou no **Gerenciamento de prompts** (Experiência centrada na marca). Os prompts originados do Google Search Console são marcados com um ícone do Google Search Console na coluna **Origem**. O ícone ajuda a distinguir entre prompts baseados no comportamento de pesquisa do usuário real daqueles adicionados manualmente ou de outras fontes.

### Perguntas frequentes {#gsc-faq}

P: Com que frequência os prompts são atualizados no painel do Google Search Console?

Os prompts originados no Google Search Console geralmente são atualizados uma vez por mês. Cada atualização extrai os dados de consulta de pesquisa mais recentes do Google Search Console, executa novamente o pipeline de geração e atualiza o conjunto de prompts. Isso garante que os prompts permaneçam alinhados às tendências de pesquisa atuais e às mudanças sazonais no comportamento do usuário.

P: Quantos prompts normalmente são originados no Google Search Console?

O número depende do tamanho da implantação e da quantidade de categorias rastreadas. Por exemplo:

| Categorias | Total de tópicos | Prompts disponibilizados |
|---------|----------|----------|
| 1-2 | 3-8 | ~65-180 |
| 4-5 | 12-20 | ~270-450 |
| 10 | 30-40 | ~675-900 |

Nosso objetivo é fornecer conjuntos de prompts que atendam às metas de qualidade comunicadas durante a avaliação e a integração: pelo menos 20 prompts por tópico, com 3 a 4 tópicos por categoria e um equilíbrio saudável entre prompts com marca/sem marca.

P: Em quanto tempo verei as sugestões provenientes do Google Search Console depois de me conectar ao Google Search Console?

Os prompts geralmente ficam disponíveis **em algumas horas** após o estabelecimento da conexão com o Google Search Console. O pipeline extrai automaticamente os dados de pesquisa, processa esses dados pelas etapas de geração e controle de qualidade e fornece o prompt final definido para o LLM Optimizer.

P: Quem pode se conectar ao Google Search Console?

Qualquer pessoa com o status **Proprietário** ou **Permissão total** na propriedade do Google Search Console pode autorizar a conexão. Esses são os níveis de permissão que concedem acesso de leitura aos dados de consulta de pesquisa. Se não tiver certeza sobre seu nível de permissão, é possível verificá-lo em **Configurações>Usuários** e permissões no Google Search Console.

P: Posso marcar prompts como ignorados ou descartados para que eles não apareçam na lista de prompts do Google Search Console?

Sim, você pode excluir qualquer prompt que não deseja monitorar. Os prompts excluídos são removidos da sua lista de prompts ativos e não aparecem em relatórios futuros. Se um prompt excluído for gerado novamente em uma atualização mensal posterior, você pode removê-lo de novo.

P: Depois de adicionar prompts do Google Search Console à minha lista de prompts, em quanto tempo verei os dados de Presença da marca desses prompts?

Os dados de presença da marca de prompts adicionados recentemente são exibidos durante a próxima atualização de dados programada, que normalmente é executada no início de cada semana. Dependendo de quando os prompts são adicionados, você pode ver os resultados em alguns dias.

## Sugestões de prompt com base em Tentativas de Citação e Tráfego de referência {#prompt-suggestions}

Em vez de adivinhar quais prompts são importantes, as **Sugestões de Prompt** começam a partir de quais agentes de IA e usuários já estão acessando ou sendo referenciados no seu site.

O Adobe LLM Optimizer analisa seus dados de CDN para identificar quais páginas os agentes de IA já estão acessando consistentemente (tentativas de citação) e encaminhando usuários para (tráfego de referência LLM). Depois disso, ele gera automaticamente sugestões de prompt com base em lacunas na cobertura de prompt atual. Em vez de adivinhar quais URLs priorizar e quais prompts criar, o fluxo de trabalho começa com sinais de tráfego reais: páginas que os agentes já estão acessando e, em seguida, definir o tipo de prompts de usuário que essas páginas devem responder.

Quando uma página já está sendo acessada de forma consistente por agentes de IA, a questão não é como fazer com que os agentes saibam da página, mas quais perguntas o conteúdo da página pode responder. Sem prompts configurados para essas páginas, você não tem visibilidade de como sua marca aparece nas respostas de IA em tópicos mais importantes. Sugestões de solicitação do Tráfego de agente fecham essa lacuna para que você possa começar a rastrear e melhorar a visibilidade da marca das páginas em que os agentes já estão mais ativos.

>[!NOTE]
>
> Na [experiência centrada na marca](/help/overview/quick-start.md#brand-centric-experience), as sugestões de aviso são exibidas na seção **Gerenciamento de Avisos**.

### Como funciona {#prompt-suggestions-how-it-works}

O fluxo de trabalho de Sugestões de prompt é executado em quatro etapas, transformando os sinais de tráfego CDN em sugestões de prompt prontas para configuração. Cada etapa se baseia na anterior: a partir de páginas em que a atividade do agente de IA já foi comprovada, entender sobre o que essas páginas se referem, verificar o que já foi abordado e gerar prompts específicos, baseados e prontos para publicar.

![Sugestões de Solicitação do Fluxo de Trabalho de Tráfego Agencial](/help/dashboards/assets/prompt-suggestions-workflow.png)

#### Etapa 1 — identificação de páginas de alto sinal do tráfego agêntico {#prompt-suggestions-step-1}

O pipeline começa identificando as páginas em seu site com as quais os sistemas de IA já estão se envolvendo ativamente, usando dois sinais de seus dados de CDN: a frequência com que os sistemas de IA acessam suas páginas como fonte enquanto respondem a perguntas reais do usuário e se essas páginas já estão direcionando usuários reais para seu site a partir de respostas geradas por IA.

* **Tentativas de citação** — como os sistemas de IA acessaram uma página como uma possível fonte ao responder às perguntas dos usuários. O pipeline procura páginas que mostram uma atividade consistente de tentativa de citação semana após semana, fornecendo uma imagem mais holística do interesse do que um único momento.
* **tráfego de referência LLM** — instâncias em que um usuário clicou a partir de uma resposta gerada por IA para chegar à URL. O pipeline se concentra nos dados de referência mais recentes e prioriza páginas com o maior volume de visitas orientadas por IA, garantindo que as sugestões sejam baseadas em padrões de recomendação de IA atuais e comprovados.

| Sinal | O que significa |
|--------|---------------|
| Somente tentativas de citação | Os agentes estão acessando consistentemente essa página como uma possível fonte |
| Somente tráfego de referência LLM | Os agentes estão enviando usuários ativamente para esta página |
| Ambos | Os agentes acessam a página e os usuários clicam nela — o alvo de maior confiança |

Uma página pode ser qualificada por meio de um sinal ou de ambos. As páginas que mostram ambos os sinais representam os destinos de maior confiança para a geração de prompt.

#### Etapa 2 — Analisar o conteúdo e a intenção da página {#prompt-suggestions-step-2}

Para cada página qualificada, o pipeline lê o conteúdo da página e:

* **Resume** em uma descrição concisa e baseada em fatos que se torna a base para tudo o que se segue.
* **Classifica** o tipo de página, seja um Produto, Recurso, Suporte ou Hub.
* Identifica a **intenção de jornada principal** — o tipo de pergunta que a página está mais bem posicionada para responder, como informativa, instrutiva, comparativa ou transacional.

As duas classificações funcionam juntas. Por exemplo, os prompts gerados de uma página de suporte, como um guia ou tutorial de configuração, têm mais probabilidade de ser relevantes para um perfil de usuário existente do que um novo público-alvo.

#### Etapa 3 — Verificar cobertura de prompt existente {#prompt-suggestions-step-3}

Antes de gerar qualquer item novo, o pipeline verifica se cada página qualificada já está coberta por prompts configurados em sua conta do LLM Optimizer, sendo executada em duas etapas:

1. Uma verificação de similaridade semântica que identifica rapidamente os prompts candidatos da biblioteca de prompts existente que estão potencialmente relacionados à página.
2. Uma revisão baseada em LLM que pontua o desempenho de cada candidato a prompt se alinha ao conteúdo da página — não apenas se ele está topicamente relacionado, mas se ele cobre sobre o que a página é.

Uma página será considerada coberta se pelo menos um prompt existente atender a esse limite. As páginas sem correspondência adequada são identificadas como lacunas e movidas para a etapa 4.

#### Etapa 4 — Gerar, verificação de qualidade e prompts de classificação por URL {#prompt-suggestions-step-4}

![Geração de prompt e verificação de qualidade](/help/dashboards/assets/prompt-suggestions-generation.png)

Para cada página de lacuna, o pipeline gera prompts com som natural baseados no conteúdo da página. Ele começa identificando personas relevantes — alguém que faria perguntas realistas que esta página responde e cria um cenário realista em torno dessa persona antes de gerar prompts de candidato.

Cada prompt passa por uma análise de qualidade automatizada em três dimensões:

* Se é **específico** para esta página, em vez de uma pergunta genérica que poderia ser aplicada a qualquer página na categoria.
* Se está **aterrado** no conteúdo real da página.
* Se parece com algo que um **usuário real** digitaria em uma ferramenta de IA, como o ChatGPT.

Os prompts que não passarem nessa revisão serão reescritos com feedback específico e revisados novamente. Se eles ainda não passarem, serão descartados.

A etapa final é uma verificação de diversidade, os prompts em URLs muito semelhantes entre si são descartados da lista final. Cada prompt é marcado com seu tópico e categoria pré-configurados e inclui um campo de raciocínio que explica por que o URL de origem foi direcionado com base em sua tentativa de citação e sinais de tráfego de referência. Os prompts também recebem uma classificação de prioridade, para que você saiba em quais sugestões agir primeiro. Prioridade mais alta significa um sinal de IA combinado mais forte do URL de origem. Os prompts estão prontos para serem revisados na guia **Sugestões de Prompt** do painel Configuração do Cliente.

### Como usar {#prompt-suggestions-how-to-use}

1. Abra o painel **Configuração do Cliente** e vá para a guia **Sugestões de Prompt**.
1. Use o filtro **Source** para selecionar **Tentativa de Citação** para exibir sugestões geradas de tráfego de agente.
1. Revise as colunas **Raciocínio** e **Prioridade** para avaliar cada sugestão.
1. Selecione os prompts que deseja adicionar e clique em **Adicionar seleção** para adicioná-los aos prompts configurados.

![Guia Sugestões de Aviso com filtro de origem de Tentativa de Citação](/help/dashboards/assets/prompt-suggestions-citation-attempt.png)

![Adicionar sugestões de prompt selecionadas](/help/dashboards/assets/prompt-suggestions-add-selection.png)

### Perguntas frequentes {#prompt-suggestions-faq}

P: Minha organização precisa de alguma configuração adicional para usar esse recurso?

Esse recurso depende dos dados de log da CDN. Se você já tiver habilitado o [encaminhamento de log da CDN](#cdn-configuration), nenhuma configuração adicional será necessária. Sem logs CDN, os dados de tentativa de citação ou tráfego de referência não estarão disponíveis para análise.

P: Por que um URL específico não é exibido nas sugestões?

Há algumas razões comuns. A página pode ainda não ter uma atividade consistente de recuperação de IA ou um tráfego de referência significativo — sem um desses sinais, ela não entra no pipeline. Ele pode já estar coberto por um prompt configurado existente, pois o pipeline gera apenas sugestões para lacunas verdadeiras. Ou o tipo de página pode não ser elegível para geração de prompt.

P: As sugestões podem mudar com o tempo?

Sim. O pipeline é executado periodicamente à medida que novos dados de CDN são disponibilizados. À medida que o comportamento do usuário e do agente evolui (quais páginas estão sendo acessadas, com que frequência e quais estão impulsionando o tráfego de referência), as sugestões refletem essas alterações. As páginas que não eram de sinal alto antes podem se qualificar em execuções futuras e as lacunas existentes que foram abordadas não gerarão mais novas sugestões.

P: Por que eu estou vendo URLs que não esperava nas sugestões?

Os URLs exibidos se baseiam totalmente no comportamento agênico observado — páginas nas quais os sistemas de IA têm acessado ou encaminhado os usuários de forma consistente, independentemente do quão proeminentes eles aparecem na estratégia de conteúdo. Em alguns casos, essas podem ser páginas que você nunca considerou importantes, mas às quais a IA chegou repetidamente. Se um URL aparece nas sugestões, é porque os dados o suportam. Você sempre pode ignorar sugestões que não se encaixam em sua estratégia, mas os dados por trás de cada sugestão são baseados em atividades reais de IA.

P: O que significa o campo de raciocínio?

Cada prompt inclui uma explicação do motivo pelo qual seu URL de origem foi listado como uma sugestão. Para páginas qualificadas por meio de tentativas de citação, mostra como a página se classifica entre todas as páginas acessadas com base em tentativas semanais. Para páginas qualificadas por meio do tráfego de referência, ele mostra o mesmo para exibições de página de referência. As páginas com ambos os sinais mostram ambos. Isso ajuda você a entender a prioridade e escolher quais sugestões publicar primeiro.

Para uma página com ambos os sinais, o raciocínio pode parecer com: *Gerado para [URL da página] — ocupa o primeiro lugar entre 3% pela mediana das tentativas de citação semanal e 1% pelo tráfego de referência LLM.*

P: Como a prioridade é determinada?

A prioridade se baseia em uma pontuação combinada de dois sinais: como uma página é classificada entre todas as páginas por tentativas de citação e como ela é classificada entre todas as páginas por exibições de página de referência de LLM. Ambos são expressos como percentis e adicionados juntos, de modo que as páginas que pontuam fortemente em ambos os sinais naturalmente sobem para o topo. Uma página que a IA está acessando de forma consistente e enviando usuários ativamente sempre será classificada acima de uma página com apenas um sinal.

P: Como o pipeline decide quais páginas se qualificam com base em tentativas de citação?

O pipeline procura páginas que mostram uma atividade consistente de recuperação de IA ao longo do tempo. Para se qualificar, uma página deve atender a duas condições: deve mostrar atividade significativa em pelo menos metade das semanas nos dados disponíveis e sua contagem mediana de ocorrências agenciais durante essas semanas ativas deve ficar entre os 25% principais em todas as páginas. Ambas as condições devem ser mantidas — a frequência por si só não é suficiente e o volume de ocorrências por si só também não é suficiente.

P: Como o pipeline decide quais páginas se qualificam com base no tráfego de referência?

Uma página é qualificada se aparecer nos 10% principais de todas as páginas pelo total de visitas de indicação do LLM nos últimos três meses. Isso garante que as sugestões sejam fundamentadas em páginas que já estão gerando click-throughs reais e mensuráveis a partir das respostas da IA, com base no comportamento recente.

P: As sugestões de prompts estão disponíveis em idiomas diferentes do inglês?

Ainda não. No momento, o pipeline gera prompts somente em inglês. O suporte a vários idiomas será adicionado em uma versão futura.
