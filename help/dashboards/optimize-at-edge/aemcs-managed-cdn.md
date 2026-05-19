---
title: Otimizar na borda – CDN gerenciada pelo AEM Cloud Service (Fastly)
description: Saiba como configurar a CDN gerenciada do AEM Cloud Service (Fastly) para a otimização na borda no LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:31:38.650Z'
TQID: 'https://experienceleague.adobe.com/qrCODY3Qg6dDd9QRcaYGdN4YVCgKAsl56UTAVZpsIwE'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 836
ht-degree: 100%

---


# CDN gerenciada do AEM Cloud Service (Fastly)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após a conclusão, verifique se o cabeçalho `x-edgeoptimize-request-id` está presente na resposta.

## Pré-requisitos

Para acessar esse recurso:

- Os clientes pagos devem ter acesso ao Perfil de produto IMS dos **Usuários do Adobe LLM Optimizer**. Entre em contato com o administrador da organização para solicitar acesso.
  ![Adicionar usuário a um perfil de produto](/help/assets/optimize-at-edge/cs-fastly-user-product-profiles.png)
- Clientes de avaliação devem fazer parte do grupo IMS do **Administrador de LLMO**. Se o grupo não existir, o administrador da organização pode criá-lo e adicionar você.
  ![Criar grupo IMS do Administrador de LLMO](/help/assets/optimize-at-edge/cs-fastly-create-ims-group.png)

>[!NOTE]
> Esse recurso não é compatível com o Safari nem com os modos de navegação incógnito/privado.

## Etapas para habilitar o roteamento

Para iniciar o roteamento do tráfego agêntico para a otimização na borda:

1. No LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Acesse a configuração do cliente](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Clique no botão **Habilitar**.

   ![Implantar otimizações em agentes de IA: pendente](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. Na caixa de diálogo de confirmação, selecione **Habilitar** para confirmar se deseja habilitar o roteamento. Se um erro aparecer, consulte a seção [Solução de problemas](#troubleshooting) para resolvê-lo.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. Uma vez confirmado, o roteamento leva alguns minutos para ser concluído.

   ![Roteamento em andamento](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   Recarregue a página após 5 minutos para verificar se o roteamento foi concluído. Assim que o roteamento estiver configurado e ativo, o status será atualizado para **Concluído** com uma marca de seleção verde confirmando que o roteamento está habilitado. Nenhuma outra ação é necessária da sua parte.

   ![Implantar otimizações em agentes de IA: concluído](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   Para desabilitar o roteamento a qualquer momento, retorne à seção **Implantar otimizações em agentes de IA** na guia **Configuração de CDN** e clique em **Desabilitar**.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de contas da Adobe ou com `llmo-at-edge@adobe.com`.

## Solução de problemas

Se ocorrer um erro ao ativar ou desativar o roteamento, ele será semelhante ao seguinte:

![Erro na Caixa de diálogo de confirmação](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

Use a lista abaixo para identificar o erro e siga as instruções.

1. **O usuário não tem acesso ao produto LLMO**

   **Causa:** a conta de usuário não tem o contexto de produto do LLM Optimizer no perfil do Adobe IMS. Isso é necessário para clientes pagos configurarem o roteamento de CDN.

   **Recomendação:** verifique se o perfil de produto **Usuários do Adobe LLM Optimizer** foi atribuído a você no Adobe Admin Console pelo administrador da sua organização.

2. **Somente membros do grupo de administradores do LLMO podem configurar o roteamento de CDN**

   **Causa:** sua conta não é membro do grupo IMS do **Administrador do LLMO**. Isso é necessário para que clientes de avaliação configurem o roteamento de CDN.

   **Recomendação:** verifique se você foi adicionado ao Grupo IMS do **Administrador do LLMO** no Adobe Admin Console pelo Administrador da organização.

3. **O tipo de CDN solicitado aem-cs-fastly não corresponde à CDN detectada para este domínio**

   **Causa:** isso indica que o tipo de CDN detectado para seu site não é *CDN gerenciada pelo AEM Cloud Service (Fastly)*.

   **Recomendação:** verifique se o seu site é distribuído por meio da CDN gerenciada do AEM Cloud Service (Fastly).

4. **Erro ao analisar o site**

   **Causa:** o LLM Optimizer não conseguiu acessar seu site durante a configuração de roteamento. Isso pode acontecer se o site estiver inativo, inacessível ou se a solicitação atingir o tempo limite.

   **Recomendação:** verifique se o site está acessível publicamente e retorna uma resposta válida e tente novamente.

5. **O site não retornou uma resposta válida para a análise de roteamento**

   **Causa:** o site retornou um status HTTP inesperado (não um 2xx ou 301) quando sondado durante a configuração.

   **Recomendação:** verifique se o site está retornando uma resposta bem-sucedida (2xx) para o URL base registrado no LLM Optimizer e tente novamente.

6. **Falha de autenticação com o serviço IMS upstream**

   **Causa:** talvez a sessão tenha expirado ou tenha ocorrido um problema de autenticação com o Adobe IMS durante a solicitação de roteamento.

   **Recomendação:** Saia do LLM Optimizer e faça login novamente. Em seguida, tente habilitar o roteamento outra vez.

Se o problema persistir, entre em contato com a equipe de contas da Adobe ou `llmo-at-edge@adobe.com`.

## (Opcional) Verificar a configuração

Depois que a configuração de roteamento for concluída, você poderá verificar opcionalmente se o tráfego de bots de IA está sendo roteado para a Otimização de borda e se o tráfego humano permanece inalterado.

1. **Testar tráfego de bots (deve ser otimizado)**

   Simular uma solicitação de bot de IA usando um agente de usuário agêntico:

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: chatgpt-user"
   ```

   Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

   ```
   < HTTP/2 200
   < x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
   ```

2. **Testar tráfego humano (NÃO deve ser afetado)**

   Simule uma solicitação regular de navegador humano:

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
   ```

   A resposta não deve conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos aos de antes da habilitação da otimização na borda.

3. **Como diferenciar entre os dois cenários**

   | Cabeçalho | Tráfego de bots (otimizado) | Tráfego humano (não afetado) |
   |---|---|---|
   | `x-edgeoptimize-request-id` | Presente — contém uma ID de solicitação exclusiva | Ausente |
   | `x-edgeoptimize-fo` | Presente somente se houver um failover (valor: `1`) | Ausente |

4. **Verificar status do roteamento no LLM Optimizer**

   Você também pode confirmar o roteamento na interface do usuário do LLM Optimizer. Abra a **Configuração do cliente** e selecione a guia **Configuração da CDN**. Quando o roteamento está ativo, a seção **Implantar otimizações em agentes de IA** exibe **Concluído**.

   ![Implantar otimizações em agentes de IA — concluído](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
