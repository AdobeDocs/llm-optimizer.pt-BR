---
title: Otimizar na borda
description: Saiba como fornecer otimizações na borda da CDN, no LLM Optimizer, sem precisar fazer alterações de criação.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '2172'
ht-degree: 85%

---


# Otimizar na borda

Esta página oferece uma visão geral detalhada sobre como fornecer otimizações na borda da CDN sem realizar alterações de criação. Ela aborda o processo de integração, as oportunidades de otimização disponíveis e como otimizar automaticamente na borda.

>[!NOTE]
>Essa funcionalidade está atualmente em disponibilidade antecipada. Saiba mais sobre os programas de acesso antecipado [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## O que é a otimização na borda?

A otimização na borda é um recurso de implantação baseada na borda no LLM Optimizer que envia alterações com linguagem de IA a agentes de usuário do LLM. No contexto atual, “borda” significa que a otimização é aplicada na camada da CDN. Como ela fornece otimizações na camada da CDN, não são necessárias alterações de criação no Sistema de gerenciamento de conteúdo (CMS), portanto, o CMS de origem permanece inalterado. Essa separação permite melhorar a visibilidade do LLM sem alterar os fluxos de trabalho de publicação existentes. Ele direciona apenas o tráfego agêntico e não afeta usuários humanos nem bots de SEO. Quando o LLM Optimizer detecta oportunidades para otimizar uma página, os usuários podem implantar correções diretamente na borda da CDN.

Otimizar na borda é uma alternativa mais rápida e simples para as correções tradicionais que exigem esforços complexos de engenharia. Como mencionado, após concluir uma configuração única, não são necessárias alterações na plataforma ou ciclos de desenvolvimento longos para aplicar as alterações. É possível publicar melhorias em minutos sem exigir o envolvimento do desenvolvedor. É uma maneira de otimizar o site para agentes de IA sem adição de código.

A otimização na borda foi projetada para usuários empresariais em equipes de marketing, SEO, conteúdo e estratégia digital. Ela permite que os usuários empresariais concluam a jornada completa no LLM Optimizer por: identificar oportunidades, compreender sugestões e implantar facilmente as correções. Com a Otimização na borda, usuários podem visualizar as alterações, implantá-las rapidamente na borda da CDN e confirmar se as otimizações estão ativas. O desempenho pode ser monitorado no ecossistema do LLM Optimizer.

### Principais benefícios

* **Entrega somente para IA:** oferece HTML otimizado somente para agentes de IA, sem impacto para visitantes humanos ou bots de SEO.
* **Ciclos mais rápidos:** publique alterações em minutos, não em semanas. Não são necessárias alterações na plataforma nem longos ciclos de engenharia.
* **Reversível:** compatível com um recurso de reversão de um clique que pode reverter a página em minutos.
* **Nenhum impacto no desempenho:** as otimizações baseadas na borda e o armazenamento em cache não afetam a latência do site.
* **Independente da CDN e do CMS:** funciona com qualquer configuração de CDN e de front-end, independentemente do sistema de gerenciamento de conteúdo.

### Quais oportunidades são compatíveis com a Otimização na borda?

Algumas oportunidades que podem melhorar a experiência agêntica na web são compatíveis com a Otimização na borda. Saiba mais sobre cada oportunidade na página [Painel de oportunidades](/help/dashboards/opportunities.md) e na seção de oportunidades da página atual.

## Integração

Entre em contato com a equipe de contas da Adobe ou com a equipe do FDE para iniciar o processo de integração. Sua equipe de TI ou CDN também é necessária para concluir os pré-requisitos e o processo de configuração. Além disso, também é possível entrar em contato com `llmo-at-edge@adobe.com` para obter maior assistência na integração.

Pré-requisitos para a integração à Otimização na borda:

* Conclua o processo de integração com o LLM Optimizer.
* Conclua o processo de encaminhamento de logs da CDN.

Requisitos para a equipe de TI/CDN:
* Adicione o agente-usuário `*AdobeEdgeOptimize/1.0*` ao Incluo na lista de permissões no arquivo robots.txt do site ou nas regras de gerenciamento de tráfego de bot.
* Verifique se as páginas não estão bloqueadas no nível de domínio ou da CDN.
* Adicionar regras de roteamento para o recurso Otimização na borda da CDN.
* Confirme o roteamento do recurso Otimização na borda na interface do LLM Optimizer.

Para orientar o processo de configuração, selecione seu provedor de CDN abaixo e siga o guia de configuração correspondente. Lembre-se de que esses exemplos devem ser adaptados à sua configuração atualmente ativa. Recomendamos aplicar as alterações nos ambientes inferiores primeiro.

### Guias de configuração da CDN

| Provedor de CDN | Tipo | Guia |
|---|---|---|
| CDN gerenciada do AEM Cloud Service (Fastly) | Gerenciado pela Adobe | [Exibir guia de instalação](/help/dashboards/optimize-at-edge-aem-managed-cdn.md) |
| Fastly (BYOCDN) | Traga seu próprio CDN | [Exibir guia de instalação](/help/dashboards/optimize-at-edge-fastly-byocdn.md) |
| Akamai (BYOCDN) | Traga seu próprio CDN | [Exibir guia de instalação](/help/dashboards/optimize-at-edge-akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Traga seu próprio CDN | [Exibir guia de instalação](/help/dashboards/optimize-at-edge-cloudflare-byocdn.md) |

>[!NOTE]
>Se o provedor de CDN não estiver listado acima ou se você não encontrar o domínio ou email na interface do usuário do LLM Optimizer, entre em contato com `llmo-at-edge@adobe.com` para obter assistência de integração. Após a conclusão das configurações, você poderá enviar sugestões para o recurso Otimização na borda no LLM Optimizer.

Cada guia de configuração de CDN acima inclui etapas de verificação detalhadas no final para confirmar que o tráfego agêntrico está sendo roteado corretamente e que o tráfego humano não é afetado.

## Oportunidades

A tabela a seguir apresenta oportunidades que podem melhorar a experiência agêntica na web e que são compatíveis com o recurso Otimização na borda.

| Oportunidade | Tipo | Identificação automática | Sugestão automática | Otimizar automaticamente |
|---------|----------|----------|----------|----------|
| Recuperar visibilidade do conteúdo | GEO técnico | Detecta páginas em que o conteúdo crítico não está visível para agentes de IA. Mostra os URLs afetados e o conteúdo esperado que pode ser recuperado. | Realça o conteúdo que pode ser disponibilizado para agentes de IA e recomenda habilitar a pré-renderização para essas páginas. | Disponibiliza um instantâneo do HTML totalmente renderizado e compatível com IA para tráfego agêntico que recupera o conteúdo oculto anteriormente. |
| Adicionar resumos compatíveis com LLM | Otimização de conteúdo | Identifica páginas longas ou complexas que não têm resumos concisos no nível da página ou da seção, dificultando a rápida análise e compreensão por parte da IA. | Recomenda resumos curtos e gerados por IA no nível da página e da seção que capturam o conteúdo principal. | Insere os resumos nas seções relevantes do HTML, melhorando a forma como os modelos interpretam e descrevem o conteúdo da página. |
| Adicionar perguntas frequentes relevantes | Otimização de conteúdo | Detecta lacunas de intenção no conteúdo da página existente que podem se beneficiar de perguntas frequentes. | Sugere conteúdo de perguntas frequentes gerado por IA e alinhado à intenção do usuário e aos tópicos existentes. | Injeta conteúdo de perguntas frequentes no HTML, tornando as páginas mais visíveis e relevantes em respostas orientadas por IA. |
| Simplificar conteúdo complexo | Otimização de conteúdo | Sinaliza páginas com texto complexo que pode atrapalhar a compreensão da IA. | Fornece versões simplificadas geradas por IA de texto complexo, preservando o significado original. | Reescreve seções complexas na página, melhorando a legibilidade da IA. |

### Ferramentas adicionais

O [Adobe LLM Optimizer: sua página da web pode ser citada?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) A extensão do Chrome mostra quanto do conteúdo da sua página da web os LLMs podem acessar e o que permanece oculto. Projetado como uma ferramenta de diagnóstico independente e gratuita, não exige licença ou configuração do produto.

Com um clique único, você pode avaliar a legibilidade por máquina de qualquer site. Você pode visualizar uma comparação lado a lado do que os agentes de IA veem em comparação com o que os usuários humanos veem e estimar quanto conteúdo poderia ser recuperado usando o LLM Optimizer. Acesse a página [A IA pode ler o seu site?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) para obter mais informações.

## Oportunidades detalhadas

Nas seções a seguir, é possível ver detalhes adicionais sobre cada oportunidade compatível com o recurso Otimização na borda.

### Recuperar visibilidade do conteúdo

Essa oportunidade sinaliza páginas em que o conteúdo principal está oculto para agentes de IA devido à renderização do lado do cliente. Em cada página identificada, é possível ver exatamente qual conteúdo está faltando na visualização do agente de IA, as lacunas de visibilidade e aplicar alterações diretas para recuperar o conteúdo oculto. Ao implantar essa oportunidade com o recurso Otimização na borda, uma versão pré-renderizada e otimizada para IA da página é disponibilizada aos agentes de usuário de LLM para que possam acessar o contexto completo sem executar o Javascript.
Isso garante que a página fique totalmente visível primeiro para os agentes de IA. Aprimoramentos adicionais são aplicados sobre o HTML pré-renderizado.

>[!IMPORTANT]
>Essa funcionalidade de pré-renderização se aplica automaticamente a todas as oportunidades apresentadas abaixo quando implantada com o recurso Otimização na borda, para garantir que a página esteja totalmente visível para os agentes de IA.

### Adicionar resumos compatíveis com LLM

Essa oportunidade identifica páginas que podem se beneficiar de resumos concisos, ajudando LLMs a entender rapidamente sobre o que se trata o conteúdo da página. Para cada página, a oportunidade detecta onde um resumo é mais necessário e cria resumos gerados por IA no nível da página ou da seção. Ao implantar com o recurso Otimização na borda, esses resumos são inseridos no HTML que os agentes de IA recuperam, melhorando as chances de ter seu conteúdo descrito com mais precisão.

### Adicionar perguntas frequentes relevantes

Essa oportunidade sinaliza páginas em que o conteúdo adicional de perguntas e respostas pode corresponder melhor à intenção do usuário e aos prompts de descoberta orientados por IA. Para cada página, ela sugere blocos de perguntas frequentes (FAQ) geradas por IA, relacionados à intenção do usuário e ao conteúdo da página. Com o recurso Otimização na borda, essas perguntas frequentes são inseridas no HTML, tornando sua página mais compatível com a IA e aumentando a probabilidade de que as respostas da IA reflitam diretamente suas orientações.

### Simplificar conteúdo complexo

Essa oportunidade encontra páginas com parágrafos longos e complexos que podem reduzir a compreensão da IA. Para cada página que excede os limites de legibilidade, ela cria conteúdo gerado por IA que é mais simples e fácil de digitalizar, preservando o significado original. Quando implantado na borda, o conteúdo simplificado entregue ao tráfego agêntico ajuda os LLMs a interpretar e resumir o conteúdo com mais fidelidade.

## Otimização automática na borda

Em cada oportunidade, é possível visualizar, editar, implantar, exibir em tempo real e reverter as otimizações na borda.

>[!VIDEO](https://video.tv.adobe.com/v/3477989/?captions=por_br&learn=on&enablevpops)

### Visualização

A opção **Visualizar** permite que você veja o impacto de uma sugestão antes que ela seja aplicada. Ela exibe uma comparação lado a lado entre a página atual e o resultado esperado da otimização por IA após aplicar a sugestão. Essa exibição usa a mesma lógica do recurso Otimização na borda, alimentando o tráfego ativo, mas em um modo de visualização isolado. Isso não afeta o tráfego ativo, pois é uma simulação somente leitura para revisão.

![Visualização](/help/assets/optimize-at-edge/preview.png)

### Editar

A opção **Editar** permite refinar ou reescrever completamente a sugestão gerada automaticamente antes de implantá-la. Em vez de aceitar a sugestão, você pode manter o controle total por meio do fluxo de trabalho de edição. A exibição mostra as alterações propostas em um editor estruturado, onde você pode modificar o texto para corresponder melhor à intenção original. A versão editada será entregue aos agentes de IA depois de implantada.

![Editar](/help/assets/optimize-at-edge/edit.png)

### Implantar

A opção **Implantar** publica as sugestões selecionadas para que as experiências otimizadas possam ser enviadas da borda para os agentes de IA. Se a CDN estiver totalmente roteada, todas as páginas no domínio normalmente serão disponibilizadas com as novas alterações em minutos. Se o roteamento tiver sido configurado apenas para caminhos seletos, somente as páginas na lista de permissões serão publicadas com as otimizações.

![Implantar](/help/assets/optimize-at-edge/deploy.png)

### Visualizar em tempo real

A opção **Visualizar em tempo real** permite verificar se a otimização está ativa e se comportando conforme o esperado para o tráfego agêntico, uma visualização que seria difícil de acessar de outra forma. Você pode visualizar a página ativa em Sugestões fixas, que renderiza a página conforme ela está sendo mostrada aos agentes de IA.

![Visualizar em tempo real](/help/assets/optimize-at-edge/view-live.png)

### Reversão

A reversão reverte com segurança uma otimização implantada anteriormente. A versão somente de IA da página normalmente retorna ao estado anterior em minutos, tornando seguro experimentar as otimizações quando necessário.

![Reversão](/help/assets/optimize-at-edge/rollback.png)

## Perguntas frequentes

P. Que tipo de LLMs são direcionados com o recurso Otimização na borda?

A lista de agentes de usuário a serem direcionados é definida por você durante o processo de integração.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

P. O que acontece se eu ainda não estiver integrado(a) ao recurso Otimização na borda?

Se você clicar em **Implantar otimizações** antes de concluir a instalação necessária, nenhuma informação será aplicada ao site. Em vez disso, uma caixa de diálogo pop-up solicita que você entre em contato com nossa equipe pelo email `llmo-at-edge@adobe.com` para obter assistência durante a integração. Até que a integração seja concluída, você ainda poderá explorar as oportunidades e sugestões detectadas, mas o fluxo de trabalho de implantação com um clique permanecerá inativo.

P: O que acontece quando o conteúdo é atualizado na origem?

Oferecemos a versão otimizada da sua página do cache, desde que a página de origem subjacente não tenha sido alterada. No entanto, quando a origem é alterada para **Recuperar Visibilidade do conteúdo**, nosso sistema é atualizado automaticamente para que os agentes de IA sempre recebam o conteúdo mais atualizado. Isso ocorre porque usamos configurações de TTL (low cache time to live) (por ordem de minutos) para que qualquer atualização de conteúdo em seu site acione uma nova otimização dentro dessa janela. Para oportunidades de conteúdo como **Adicionar Resumos Amigáveis a LLM**, o LLM Optimizer monitora as alterações na página de origem. Se uma alteração for detectada, pausaremos a otimização e a sinalizaremos para revisão humana para evitar o descompasso do conteúdo entre a página visível por agente e a página visível por humanos.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

P. O recurso Otimização na borda é somente para sites que usam o Adobe Edge Delivery Service (EDS)?

Não. O recurso Otimização na borda é independente da CDN e funciona com qualquer arquitetura de front-end, não apenas com as implantadas na pilha do Adobe EDS.

P: Como a pré-renderização do recurso Otimização na borda se diferencia da renderização tradicional do lado do servidor (SSR)?

Ambas resolvem problemas diferentes e podem trabalhar juntas. A SSR tradicional renderiza o conteúdo do lado do servidor, mas não inclui conteúdo carregado posteriormente no navegador. A pré-renderização do recurso Otimização na borda captura a página depois que o JavaScript e os dados do lado do cliente são carregados, produzindo a versão completa na borda da CDN. A SSR se concentra em melhorar a experiência humana, e o recurso Otimização na borda melhora a experiência da web para LLMs.

P. O que acontece se eu implantar otimizações para alguns URLs em meu domínio, mas não todos?

Somente os URLs que você otimiza explicitamente são modificados. Para URLs com oportunidades implantadas, os agentes de IA recebem a versão otimizada. Para URLs sem oportunidades implantadas, nosso serviço simplesmente faz o proxy da página original como está, sem aplicar alterações ou armazená-la em nossa camada de cache de otimização. Isso garante que você possa implantar otimizações seletivamente sem afetar o restante do site.
