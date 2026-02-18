---
source-git-commit: beae935e7a34f5bccbe21578fa9a928912958710
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---
# Trechos

## Verifique a configuração - Adobe Managed CDN {#verify-setup-adobe-aem-cs-cdn}

**Verificar a configuração**

Após concluir a configuração, verifique se o tráfego de bot está sendo roteado para o Edge Otimize e se o tráfego humano não foi afetado.

**1. Tráfego de bot de teste (deve ser otimizado)**

Simular uma solicitação de bot de IA usando um user-agent agêntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Testar tráfego humano (NÃO deve ser afetado)**

Simular uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta deve **não** conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos a antes de habilitar a opção Otimizar no Edge.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bot (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém um ID de solicitação exclusivo | Ausente |
| `x-edgeoptimize-fo` | Presente somente se houver failover (valor: `1`) | Ausente |

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

## Verificar a configuração - BYOCDN {#verify-setup-byocdn}

**Verificar a configuração**

Após concluir a configuração, verifique se o tráfego de bot está sendo roteado para o Edge Otimize e se o tráfego humano não foi afetado.

**1. Tráfego de bot de teste (deve ser otimizado)**

Simular uma solicitação de bot de IA usando um user-agent agêntico:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Uma resposta bem-sucedida inclui o cabeçalho `x-edgeoptimize-request-id`, confirmando que a solicitação foi roteada pelo Edge Otimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Testar tráfego humano (NÃO deve ser afetado)**

Simular uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta deve **não** conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos a antes de habilitar a opção Otimizar no Edge.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bot (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém um ID de solicitação exclusivo | Ausente |
| `x-edgeoptimize-fo` | Presente somente se houver failover (valor: `1`) | Ausente |

O status do roteamento de tráfego também pode ser verificado na interface do usuário do LLM Optimizer. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

![Status do Roteamento de Tráfego de IA com roteamento habilitado](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Etapas de recuperação da chave de API {#retrieve-byocdn-api-key}

**Etapas para recuperar sua chave de API:**

1. Navegue até **Configuração do cliente** e selecione a guia **Configuração da CDN**.

   ![Navegar até a Configuração do Cliente](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Em **Roteamento de tráfego de IA para Implantar Otimizações**, marque a caixa de seleção **Implantar Otimizações em Agentes de IA**.

   ![Otimizações de Implantação de Tarefa para Agentes de IA](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copie a chave da API e prossiga com as etapas de configuração de roteamento abaixo.

   ![Copiar a chave de API](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >Nesse estágio, o status pode mostrar uma cruz vermelha indicando que a configuração ainda não foi concluída. Isso é esperado — quando você concluir a configuração de roteamento abaixo e o tráfego de bot de IA começar a fluir, o status será atualizado para uma marca de seleção verde confirmando que o roteamento foi ativado com êxito.

Além disso, se você precisar de ajuda com as etapas acima, entre em contato com a equipe de conta da Adobe ou com o `llmo-at-edge@adobe.com`.

## Retornar à visão geral {#return-to-overview}

Para saber mais sobre como Otimizar na Edge, incluindo oportunidades disponíveis, fluxos de trabalho de otimização automática e perguntas frequentes, volte para a [visão geral de Otimizar na Edge](/help/dashboards/optimize-at-edge.md).
