---
title: Otimizar na borda – CDN gerenciada pelo AEM Cloud Service (Fastly)
description: Saiba como configurar a CDN gerenciada do AEM Cloud Service (Fastly) para a otimização na borda no LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:31:38.650Z'
TQID: 'https://experienceleague.adobe.com/qrCODY3Qg6dDd9QRcaYGdN4YVCgKAsl56UTAVZpsIwE'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: e06fae5f-830b-4222-a469-b5e148d36465
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 836
ht-degree: 20%

---


# CDN gerenciada do AEM Cloud Service (Fastly)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após a conclusão da instalação, verifique o cabeçalho `x-edgeoptimize-request-id` na resposta.

## Pré-requisitos

Para acessar esse recurso:

- Os clientes pagos devem ter acesso ao **Perfil de produto IMS dos usuários do Adobe LLM Optimizer**. Entre em contato com o administrador da organização para solicitar acesso.
  ![Adicionar usuário a um perfil de produto](/help/assets/optimize-at-edge/cs-fastly-user-product-profiles.png)
- Clientes de avaliação devem fazer parte do grupo IMS **LLMO Admin**. Se o grupo não existir, o administrador da organização poderá criá-lo e adicionar você.
  ![Criar grupo IMS do Administrador de LLMO](/help/assets/optimize-at-edge/cs-fastly-create-ims-group.png)

>[!NOTE]
> Esse recurso não é compatível com o Safari nem com os modos de navegação incógnito/privado.

## Etapas para ativar o roteamento

Para iniciar o roteamento do tráfego agêntico para o Edge Otimize:

1. Na LLM Optimizer, abra **Configuração do cliente** e selecione a guia **Configuração de CDN**.

   ![Acesse a Configuração do cliente](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. Localize a seção **Implantar otimizações em agentes de IA**. Clique no botão **Habilitar**.

   ![Implantar otimizações em agentes de IA — pendente](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. Na caixa de diálogo de confirmação, selecione **Habilitar** para confirmar se deseja habilitar o roteamento. Se um erro aparecer, consulte a seção [Solução de problemas](#troubleshooting) para resolvê-lo.

   ![Habilitar caixa de diálogo de confirmação do mecanismo de otimização](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. Uma vez confirmado, o roteamento levará alguns minutos para ser concluído.

   ![Roteamento em andamento](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   Recarregue a página após 5 minutos para verificar se o roteamento foi concluído. Quando o roteamento estiver configurado e ativo, o status será atualizado para **Concluído** com uma marca de seleção verde confirmando que o roteamento está habilitado. Nenhuma outra ação é necessária da sua parte.

   ![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   Para desabilitar o roteamento a qualquer momento, retorne à seção **Implantar otimizações em agentes de IA** da guia **Configuração de CDN** e clique em **Desabilitar**.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de contas da Adobe ou com `llmo-at-edge@adobe.com`.

## Solução de problemas

Se um erro for exibido durante a ativação ou desativação do roteamento, ele será semelhante ao seguinte:

![Erro de Caixa de Diálogo de Confirmação](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

Use a lista abaixo para identificar o erro e siga as instruções.

1. **O usuário não tem acesso ao produto LLMO**

   **Causa:** a conta de usuário não tem o contexto de produto do LLM Optimizer no seu perfil do Adobe IMS. Isso é necessário para clientes pagos configurarem o roteamento CDN.

   **Recomendação:** verifique se você recebeu o Perfil de Produto **Usuários do Adobe LLM Optimizer** no Adobe Admin Console pelo seu Org Admin.

2. **Somente membros do grupo de administradores do LLMO podem configurar o roteamento CDN**

   **Causa:** sua conta não é membro do grupo IMS **Administrador do LLMO**. Isso é necessário para que clientes de avaliação configurem o roteamento de CDN.

   **Recomendação:** verifique se você foi adicionado ao Grupo IMS do **Administrador do LLMO** no Adobe Admin Console pelo seu Administrador da Organização.

3. **O tipo de CDN solicitado aem-cs-fastly não corresponde à CDN detectada para este domínio**

   **Causa:** Isso indica que o tipo de CDN detectado para seu site não é *CDN gerenciada pelo AEM Cloud Service (Fastly)*.

   **Recomendação:** verifique se seu site é distribuído por meio da CDN gerenciada do AEM Cloud Service (Fastly).

4. **Erro ao analisar o site**

   **Causa:** o LLM Optimizer não conseguiu acessar seu site durante a configuração de roteamento. Isso pode acontecer se o site estiver inativo, inacessível ou se a solicitação atingir o tempo limite.

   **Recomendação:** verifique se o site está acessível publicamente e retorne uma resposta válida e tente novamente.

5. **O site não retornou uma resposta válida para a investigação de roteamento**

   **Causa:** O site retornou um status HTTP inesperado (não 2xx ou 301) quando sondado durante a instalação.

   **Recomendação:** verifique se o site está retornando uma resposta bem-sucedida (2xx) para a URL base registrada no LLM Optimizer e tente novamente.

6. **Falha de autenticação com o serviço IMS upstream**

   **Causa:** talvez a sessão tenha expirado ou tenha ocorrido um problema de autenticação com o Adobe IMS durante a solicitação de roteamento.

   **Recomendação:** Faça logout do LLM Optimizer, entre novamente e tente habilitar o roteamento novamente.

Se o problema persistir, entre em contato com a equipe de conta da Adobe ou `llmo-at-edge@adobe.com`.

## (Opcional) Verifique a configuração

Após a conclusão da configuração de roteamento, você pode, opcionalmente, verificar se o tráfego de bot de IA está sendo roteado para o Edge Otimize e se o tráfego humano permanece inalterado.

1. **Testar tráfego de bot (deve ser otimizado)**

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

   Você também pode confirmar o roteamento na interface do LLM Optimizer. Abra a **Configuração do cliente** e selecione a guia **Configuração de CDN**. Quando o roteamento está ativo, a seção **Implantar otimizações em agentes de IA** exibe **Concluído**.

   ![Implantação de otimizações em agentes de IA — concluída](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
