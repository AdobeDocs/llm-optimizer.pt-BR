---
source-git-commit: e9309dc8f8d1d81b953483f17dcb424e46d5cd3b
workflow-type: tm+mt
source-wordcount: '457'
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

## Opcional: testar o roteamento em um nome de host de preparo {#retrieve-staging-edge-optimize-api-key}

**Opcional: Testar roteamento em um nome de host de preparo**

Se você quiser validar o roteamento em um ambiente inferior antes de habilitar o roteamento de produção, poderá configurar um nome de host de preparo.

**Requisitos**

* O nome de host de preparo deve estar no **mesmo domínio registrável** que a produção (por exemplo, `https://staging.example.com` quando a produção for `https://www.example.com`).
* Apenas **um** domínio de preparo por site. Depois de salvo, não é possível alterá-lo sem entrar em contato com a Adobe.

**Obtenha sua chave de API de preparo**

1. Abra **Configuração do cliente** e selecione **Configuração da CDN**.
2. Em **Implantar otimizações para agentes de IA**, selecione **Adicionar domínio de preparo** (ou **Domínio de preparo** se um domínio de preparo já estiver configurado).
3. Insira a URL de preparo completa incluindo `https://` e selecione **Definir Domínio**.
4. Copie a chave de API de **preparo** da caixa de diálogo de confirmação.

![Chave de API do domínio de preparo](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Implante as mesmas regras de roteamento no ambiente de preparo usando a chave de API de preparo.

**Testar tráfego de bot de preparo**

Substitua `https://staging.example.com/page.html` com seu caminho e URL de preparo real. **Êxito:** a resposta inclui o cabeçalho `x-edgeoptimize-request-id`.

Se precisar de ajuda, contate `llmo-at-edge@adobe.com`.

## Verificar o status do roteamento no LLM Optimizer {#verify-routing-status-in-ui}

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração de CDN**.

![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Permitindo a otimização no Edge por meio de regras de firewall (opcional) {#waf-allowlist-setup}

Se o CDN usar um WAF ou Gerenciador de bot:

* Inclua na lista de permissões o agente de usuário `*AdobeEdgeOptimize/1.0*` no WAF ou no Gerenciador de bot para que o serviço Otimizar na Edge possa buscar o conteúdo de origem.
* Se o firewall exigir verificação adicional além do agente do usuário, gere um segredo (por exemplo, `openssl rand -hex 32`) e:
   * Adicione `x-edgeoptimize-fetcher-key` com o segredo em suas regras de roteamento junto com os outros cabeçalhos `x-edgeoptimize-*`.
   * Adicione uma regra do WAF ou do Gerenciador de bot para permitir solicitações em que `x-edgeoptimize-fetcher-key` corresponde ao mesmo segredo.
* Otimizar no Edge encaminha esse cabeçalho como está — você é o proprietário do ciclo de vida completo da chave.

## Retornar à visão geral {#return-to-overview}

Para saber mais sobre como Otimizar na Edge, incluindo oportunidades disponíveis, fluxos de trabalho de otimização automática e perguntas frequentes, volte para a [visão geral de Otimizar na Edge](/help/dashboards/optimize-at-edge/overview.md).
