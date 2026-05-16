---
title: Enriquecimento do catálogo de produtos
description: Saiba como a LLM Optimizer identifica produtos com descrições genéricas ou tecnicamente densas e como melhorá-las usando enriquecimentos narrativos gerados por IA viabilizados pelo Adobe Commerce.
feature: Opportunities
autotag-review: '2026-05-15T17:45:51.619Z'
TQID: 'https://experienceleague.adobe.com/5ihGQ8L-37uWsZSDo4TVCUPBPqsqqQ5waGbH3VKPIig'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1266
ht-degree: 0%

---


# Enriquecer catálogo de produtos

As LLMs tentam conectar atributos de produto ao valor real, aos casos de uso e à intenção do comprador. Quando os nomes e as descrições dos produtos não comunicam esse valor claramente, é menos provável que seus produtos sejam citados, recomendados ou exibidos na descoberta orientada por IA. Isso ocorre porque os agentes de IA raciocinam por meio de relacionamentos, não campos de dados brutos. Uma lista de produtos com um nome como &quot;Coffee Grinder X200&quot; e uma descrição listando especificações técnicas (potência do motor, configurações de moagem etc.) dá um LLM muito pouco para trabalhar quando um comprador pede para &#39;o melhor espresso moedor para um barista de casa&#39;.

A oportunidade Enriquecimento do catálogo de produtos identifica produtos no catálogo do Commerce, onde os nomes e as descrições são muito genéricos, muito densos tecnicamente ou muito ambíguos para que os LLMs possam interpretar com precisão. Desenvolvido pela Adobe Commerce, ele gera enriquecimentos orientados por narrativa e intencionais para seus nomes e descrições de produtos e os aplica diretamente ao catálogo da Commerce com um único clique.

Ele apresenta duas métricas principais rapidamente:

- **URLs** — uma lista de Páginas de Detalhes do Produto (produtos no catálogo) que foram avaliadas quanto à qualidade do enriquecimento.
- **Tráfego de Agente** — O total de visitas e interações em um site iniciadas e orientadas por agentes de IA autônomos (como assistentes ou bots alimentados por LLM) que atuam em nome dos usuários para descobrir, recuperar ou se envolver com conteúdo.

![Enriquecer painel do Catálogo de Produtos](/help/dashboards/opportunities/assets/enrich-product-catalog-overview.png)

>[!NOTE]
>
>No momento, esta oportunidade está na Beta e pode ser ativada pelos clientes da Adobe Commerce. Entre em contato com o Gerente de conta para obter acesso ao beta.

## Como funciona

O Adobe Commerce Catalog Agent lê os dados do catálogo de produtos e analisa cada SKU do produto, incluindo todos os atributos técnicos, contexto da categoria, variantes e nome e descrição existentes. Ele identifica produtos em que o nome ou a descrição atual não comunica o valor relevante para o comprador e gera uma alternativa enriquecida que traduz os detalhes técnicos em uma linguagem clara e alinhada à intenção.

Por exemplo, um produto denominado *&quot;Coffee Grinder X200&quot;* com uma descrição listando &quot;18 configurações de moagem, motor de 450W&quot; pode ser enriquecido para explicar que &#39;O X200 oferece consistência de espresso no nível do café porque seu sistema de moagem de 18 etapas emparelha com um motor de alto torque para resultados repetíveis em casa&#39;. Atributos como preço e inventário são intencionalmente excluídos do enriquecimento — o Catalog Agent focaliza atributos que determinam o valor do produto, como ele é usado e por que ele é importante para um comprador.

Os produtos com sugestões de enriquecimento são exibidos na tabela **URLs with suggestions**, priorizadas pelo impacto do enriquecimento. Para cada produto identificado, a LLM Optimizer fornece:

- **Nome Atual** — O nome do produto existente como ele aparece no catálogo do Adobe Commerce.
- **Nome Atualizado** — O nome de produto gerado pela IA e orientado por valor que comunica a intenção e o contexto relevantes para o comprador aos LLMs.
- **Descrição atual** — A descrição do produto existente como ela aparece no catálogo do Adobe Commerce.
- **Descrição sugerida** - A descrição gerada pela IA que traduz os atributos técnicos do seu produto em uma narrativa que ajuda os LLMs a entender o produto, o valor da narrativa e por que ele é importante.

![Produtos com tabela de sugestões](/help/dashboards/opportunities/assets/enrich-product-catalog-suggestions.png)

## Produtos com sugestões

A tabela **URLs com sugestões** lista todos os produtos com oportunidades de enriquecimento. Para cada produto, você pode:

- **Expanda a linha** para exibir a Análise de IA e o enriquecimento proposto.
- **Edite** o nome ou a descrição do produto proposto antes de aplicar, para alinhar-se à voz da sua marca e às diretrizes de comercialização.
- **Implante a Otimização** para os produtos que deseja enriquecer e publique-a diretamente no catálogo do Adobe Commerce.
- **Marcar como Corrigido** depois que o enriquecimento tiver sido revisado e aplicado.
- **Ignore** sugestões que não são relevantes para sua estratégia de catálogo.

As sugestões são organizadas em três modos de exibição: **Sugestões Atuais**, **Sugestões Fixas** e **Sugestões Ignoradas**. Depois que um enriquecimento é aplicado, ele é movido para Sugestões Fixas com um status de **Aplicado** e uma ação **Exibir no Catálogo** para verificar a atualização no Adobe Commerce. Os enriquecimentos aplicados podem ser revertidos a qualquer momento, restaurando o nome e a descrição originais do produto.

<!--[Fixed suggestions with Applied status](/help/dashboards/opportunities/assets/enrich-product-catalog-fixed.png)-->

## Implantar a otimização

Depois de revisar e, opcionalmente, editar as sugestões para os produtos selecionados, clique em **Implantar Otimizações** para publicar o nome e a descrição atualizados do produto no catálogo do Adobe Commerce. Uma caixa de diálogo de confirmação mostra os produtos selecionados e as alterações que estão sendo aplicadas. Após a confirmação, uma tela de resultados confirma quais produtos foram atualizados com êxito.

Como os enriquecimentos são aplicados diretamente ao catálogo do Adobe Commerce, os nomes e descrições atualizados dos produtos ficam imediatamente disponíveis em todos os canais que usam seu catálogo, incluindo suas lojas, feeds de anúncio e quaisquer integrações diretas de produtos do LLM. Isso garante que cada superfície onde seu produto aparece comunique informações consistentes e de alta qualidade.

>[!NOTE]
>
>O Enriquecimento do catálogo exige que o LLM Optimizer esteja conectado ao Adobe Commerce. Se a sua instância do Commerce ainda não estiver conectada ao LLM Optimizer, você será direcionado para a configuração da conexão antes que os enriquecimentos possam ser aplicados.

![Caixa de diálogo Aplicar enriquecimentos](/help/dashboards/opportunities/assets/enrich-product-catalog-deploy.png)

## Experimente na demonstração

Veja a oportunidade Enriquecer catálogo de produtos em ação usando o ambiente de demonstração Frescopa.

[Ver Enriquecer catálogo de produtos na demonstração Frescopa](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Perguntas frequentes

**Por que os nomes e as descrições dos produtos genéricos prejudicam a capacidade de descoberta da IA?**

Os LLMs não correspondem produtos a consultas do comprador ao procurar sobreposição de palavra-chave. Elas raciocinam sobre relacionamentos, conectando o que um comprador pretende encontrar com o que um produto realmente faz, para quem ele serve e como ele se compara às alternativas. Um nome de produto ou descrição que lista especificações técnicas sem comunicar o valor do mundo real fornece um LLM muito pouco contexto para se trabalhar. O resultado é que seu produto tem menos probabilidade de ser citado quando um comprador faz uma pergunta relevante, mesmo que seu produto seja a melhor correspondência para sua necessidade.

**Quais atributos de produto o Agente de Catálogo usa para gerar enriquecimentos?**

O Catalog Agent usa atributos que geram valor em seu catálogo Commerce que ajudam os LLMs a entender o que é um produto, como ele é usado e por que ele é importante. Atributos que agregam valor, como recursos do produto, casos de uso, propriedades do material, contexto da categoria e detalhes de compatibilidade. Atributos como preços e níveis de inventário são intencionalmente excluídos, pois não contribuem para a compreensão semântica do produto e podem tornar as descrições menos duráveis à medida que as condições mudam.

**É possível editar o enriquecimento gerado pela IA antes de aplicá-lo?**

Sim. Todas as sugestões incluem uma visualização editável do nome e da descrição do produto propostos. Você pode modificar o enriquecimento para alinhá-lo à voz da sua marca, corrigir imprecisões ou incorporar contexto adicional antes de aplicá-lo ao seu catálogo.

**O enriquecimento mudará o que os visitantes humanos veem em minha vitrine?**

Sim, visitantes humanos verão o nome e a descrição atualizados do produto na loja, juntamente com todos os outros canais que se originam no catálogo do Commerce. Isso é intencional: o objetivo é melhorar a maneira como seu produto é entendido em todos os lugares, não apenas pelos agentes de IA e também para evitar riscos de cloaking.

**O que acontece com meus outros canais de vendas quando aplico um enriquecimento?**

Como o enriquecimento é gravado diretamente no catálogo do Adobe Commerce, ele se propaga automaticamente para todos os canais que usam seu catálogo comercial como fonte da verdade, incluindo várias lojas, pipelines de publicidade e feeds diretos de produtos do LLM. Isso garante a consistência da marca e informações de produto coerentes para os LLMs que rastream a Internet para seus produtos.

**Posso reverter um enriquecimento se eu não estiver satisfeito com o resultado?**

Sim. Os enriquecimentos aplicados podem ser revertidos a qualquer momento a partir da exibição de Sugestões fixas, restaurando o nome e a descrição do produto original no catálogo do Adobe Commerce.
