---
source-git-commit: da789100d814004687de2f46e18a295671dec4b8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---
# Trechos

## Etapas de recuperação da chave de API {#retrieve-byocdn-api-key}

**Etapas para recuperar a chave de API de otimização do Edge de produção:**

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Marque a caixa de seleção **Habilitar mecanismo de otimização**.

   ![Implantar otimizações em agentes de IA — pendente](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. No diálogo de confirmação, selecione **Habilitar**.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. Selecione **Exibir detalhes**. Na caixa de diálogo **Implantar detalhes de otimizações**, copie a **Chave da API de Produção** (use **Copiar** ao lado do campo).

   ![Chave da API de produção em Detalhes de otimizações de implantação](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >A caixa de diálogo pode mostrar que a configuração não está concluída. Isso é esperado até que o roteamento seja verificado — você ainda pode copiar a chave da API para que sua equipe de TI ou de CDN possa concluir a configuração.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

## Chave de API do domínio de preparo (opcional) {#retrieve-staging-edge-optimize-api-key}

Use um nome de host de preparo quando quiser testar Otimizar no Edge em um ambiente inferior antes que o tráfego de produção use as regras de roteamento.

**Pré-requisitos**

* O nome do host de preparo deve pertencer ao **mesmo domínio registrável** do site de produção (por exemplo, `https://staging.example.com` quando a produção for `https://www.example.com`).
* Somente **um** domínio de preparo pode ser configurado para o site. Depois de salvo, não pode ser alterado sem ajuda.

**Etapas**

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

2. Na seção **Implantar otimizações em agentes de IA**, selecione **Adicionar domínio de preparo** (ou **Domínio de preparo** se um domínio de preparo já estiver configurado).

3. Na caixa de diálogo **Domínio de Preparo**, insira a URL de preparo completa incluindo `https://` e selecione **Definir Domínio**.

   ![Caixa de diálogo de entrada Domínio de Preparo](/help/assets/optimize-at-edge/byocdn-staging-domain-input.png)

4. Confirme o domínio no próximo prompt. Quando o fluxo de trabalho for concluído, a caixa de diálogo **Domínios de Preparo** mostrará o domínio configurado e sua **chave de API**. Selecione **Copiar** para copiar a chave de API de preparo.

   ![Chave de API do domínio de preparo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Se precisar de ajuda, contate `llmo-at-edge@adobe.com`.

## Verificar o status do roteamento no LLM Optimizer {#verify-routing-status-in-ui}

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração de CDN**.

![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Retornar à visão geral {#return-to-overview}

Para saber mais sobre como Otimizar na Edge, incluindo oportunidades disponíveis, fluxos de trabalho de otimização automática e perguntas frequentes, volte para a [visão geral de Otimizar na Edge](/help/dashboards/optimize-at-edge/overview.md).
