---
title: Otimizar na borda — Cloudflare (BYOCDN)
description: Saiba como configurar o Cloudflare BYOCDN para otimizar na borda no LLM Optimizer.
feature: Opportunities
autotag-review: '2026-05-15T17:40:49.847Z'
TQID: 'https://experienceleague.adobe.com/HkaDwdHRGZJnip-1Bp-4Z-ovwcBPxFUSDqeLUVNu0zo'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 1906
ht-degree: 68%

---


# Cloudflare (BYOCDN)

Essa configuração roteia o tráfego agêntico (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end do Edge Optimize (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam sendo atendidos a partir da sua origem normalmente. Para testar a configuração, após sua conclusão, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras de roteamento do Cloudflare Worker, certifique-se de ter:

* Uma conta da Cloudflare com o Workers habilitado no seu domínio.
* Acesse as configurações de DNS do seu domínio no Cloudflare.
* Uma chave da API do Edge Optimize obtida na interface do usuário do LLM Optimizer. Para obter as etapas, consulte [Recuperar suas chaves de API](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key).
* (Opcional) Para testar o roteamento de preparo, consulte [Chave de API de preparo](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional).

**Como funciona o roteamento**

Quando configurada corretamente, uma solicitação ao seu domínio (por exemplo, `www.example.com/page.html`) de um usuário agêntico é interceptada pelo Cloudflare Worker e roteada para o back-end do Edge Otimize. A solicitação de back-end inclui os cabeçalhos necessários.

**Testando a solicitação de back-end**

Você pode verificar o roteamento fazendo uma solicitação direta para o back-end do Edge Otimize.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Cabeçalhos obrigatórios**

Os seguintes cabeçalhos devem ser definidos nas solicitações para o back-end do Edge Otimize:

| Cabeçalho | Descrição | Exemplo |
|--------|-------------|---------|
| `x-forwarded-host` | O host original da solicitação. Obrigatório para identificar o domínio do site. | `www.example.com` |
| `x-edgeoptimize-url` | O caminho do URL original e a string de consulta da solicitação. | `/page.html` ou `/products?id=123` |
| `x-edgeoptimize-api-key` | A chave de API fornecida pela Adobe para o seu domínio. | `your-api-key-here` |
| `x-edgeoptimize-config` | String de configuração para diferenciação de chave de cache. | `LLMCLIENT=TRUE;` |

## Opções de configuração

Há duas maneiras de configurar o Cloud Worker para otimização do Edge:

* [**Opção 1: Implantar no Cloudflare (recomendado)**](#option-1-deploy-to-cloudflare) — Cria automaticamente um novo trabalhador e solicita as variáveis e os segredos de ambiente necessários. Use esta opção se você não tiver um Cloud Worker existente para este domínio.
* [**Opção 2: Configuração manual**](#option-2-manual-setup) — instruções passo a passo para criar e configurar o funcionário você mesmo. Use esta opção se você já tiver um Cloud Worker configurado no seu domínio — será necessário mesclar o código de Otimização do Edge ao seu trabalhador existente (consulte [Etapa 2: adicionar o código do Worker](#option-2-manual-setup)) ou se você preferir controle total sobre a implantação.

Independentemente da opção escolhida, você deve vincular manualmente o trabalhador ao seu domínio. Consulte [Etapa: adicionar uma rota ao seu domínio](#add-a-route-to-your-domain).

## Opção 1: implantar no Cloud Flare

Esta opção usa o botão **Implantar na Nuvem** para criar automaticamente o trabalhador e configurar as variáveis de ambiente e os segredos necessários na sua conta da Nuvem. Essa é a maneira mais rápida de começar se você estiver configurando um novo trabalhador.

>[!IMPORTANT]
>
>Use esta opção somente se você **não** tiver um Cloud Worker em seu domínio. Se você já tiver um trabalhador, use a [Opção 2: Configuração manual](#option-2-manual-setup) para adicionar a lógica de roteamento do Edge Otimize ao seu trabalhador existente.

**Etapa 1: implantar o trabalhador**

Clique no botão abaixo para implantar o trabalhador Edge Otimize na sua conta do Cloud Flare:

[![Implantar no Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/cloudflare/automation)

**Etapa 2: preencher o formulário de implantação**

Clicar no botão abre a página Configuração de trabalhadores. Preencha o formulário da seguinte maneira:

![Página de configuração do Cloud Flare Workers](/help/assets/optimize-at-edge/cloudflare-deploy-form.png)

1. **Conta Git** — selecione sua conta GitHub ou GitLab na lista suspensa. O Cloud Flare bifurca o código do trabalhador em um repositório em sua conta. Se nenhuma conta estiver listada, você poderá adicionar uma nova conexão diretamente da lista suspensa selecionando **+ Nova conexão GitHub** ou **+ Nova conexão GitLab**. Para obter mais informações, consulte o [guia de integração Git da Cloudflare](https://developers.cloudflare.com/workers/ci-cd/builds/git-integration/github-integration/).

   ![Lista suspensa de contas Git mostrando as opções Nova conexão GitHub e Nova conexão GitLab](/help/assets/optimize-at-edge/cloudflare-git-connection.png)
2. **Criar repositório Git privado** — Deixe esta opção marcada (padrão).
3. **Nome do projeto** — Deixe como `edge-optimize-router` ou insira um nome de sua escolha.
4. **EDGE_OTIMIZE_API_KEY** — Cole a chave de API do Edge Otimize fornecida pela Adobe. Esse valor é armazenado como um segredo criptografado.
5. **EDGE_OTIMIZE_TARGET_HOST** — Insira o domínio do site sem o protocolo (por exemplo, `www.example.com`).
6. **Comando de compilação** — Deixe vazio.
7. **Comando de implantação** — Deixe como `npm run deploy` (pré-preenchido).
8. **Compilações para ramificações de não produção** — Deixe desmarcado. Este é um recurso de fluxo de trabalho de desenvolvedor e não é necessário para esta implantação.
9. Clique em **Criar e implantar**.

Após a implantação do trabalhador, prossiga para [Adicionar uma rota ao seu domínio](#add-a-route-to-your-domain) para vincular o trabalhador ao seu domínio. O roteamento não é configurado automaticamente e deve ser concluído manualmente.

## Opção 2: configuração manual

Siga estas etapas para criar e configurar o trabalhador manualmente.

**Etapa 1: criar o Cloudflare Worker**

1. Faça login no painel do Cloudflare.
2. Navegue até **Trabalhadores e páginas** na barra lateral.
3. Clique em **Criar aplicativo** e depois em **Criar Trabalhador**.
4. Nomeie seu trabalhador (por exemplo, `edge-optimize-router`).
5. Clique em **Implantar** para criar o trabalhador com o código padrão.

![Painel do Cloudflare Workers](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Etapa 2: adicionar o código do trabalhador**

Depois de criar o trabalhador, clique em **Editar código** e substitua o código padrão pelo seguinte. Se você já tiver um Cloud Worker existente, mescle o código abaixo com seu código de trabalhador existente, em vez de substituí-lo totalmente.

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");
    edgeOptimizeHeaders.delete("x-edgeoptimize-fetcher-key"); // Optional (required only in case of WAF)

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    // edgeOptimizeHeaders.set("x-edgeoptimize-fetcher-key", "<YOUR FETCHER KEY>"); // Optional (required only in case of WAF)

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Clique em **Salvar e implantar** para publicar o trabalhador.

![Editor de código do Cloud Worker](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Etapa 3: configurar variáveis e segredos de ambiente**

As variáveis de ambiente armazenam configurações confidenciais, como sua chave de API, de forma segura.

1. Nas configurações do seu trabalhador, acesse **Configurações** > **Variáveis**.
2. Em **Variáveis de ambiente**, clique em **Adicionar variável**.
3. Adicione as seguintes variáveis:

   | Nome da variável | Descrição | Obrigatório |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Sua chave da API do Edge Optimize fornecida pela Adobe. | Sim |
   | `EDGE_OPTIMIZE_TARGET_HOST` | O host de destino para solicitações do Edge Optimize (enviadas como cabeçalho `x-forwarded-host`) e o domínio de origem para failover. Deve ser apenas o domínio, sem o protocolo (por exemplo, `www.example.com`, e não `https://www.example.com`). | Sim |

4. Para a chave de API, clique em **Criptografar** para armazená-la com segurança.
5. Clique em **Salvar e implantar**.

![Variáveis de ambiente do Cloudflare](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

## Adicionar uma rota ao seu domínio {#add-a-route-to-your-domain}

Independentemente da opção de configuração usada, é necessário vincular manualmente o trabalhador ao seu domínio. Essa etapa ativa o trabalhador em seu tráfego.

1. Vá para as **Configurações** > **Acionadores** do seu trabalhador.
2. Em **Rotas**, clique em **Adicionar rota**.
3. Insira seu padrão de domínio (por exemplo, `www.example.com/*` ou `example.com/*`).
4. Selecione sua zona na lista suspensa.
5. Clique em **Salvar**.

Como alternativa, você pode configurar rotas no nível da zona:

1. Navegue até o domínio no Cloudflare.
2. Vá para **Rotas dos trabalhadores**.
3. Clique em **Adicionar rota** e especifique o padrão e o trabalhador.

![Rotas do Cloudflare Worker](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Verificação do comportamento de failover**

Se o Edge Optimize não estiver disponível ou apresentar um erro, o trabalhador será automaticamente redirecionado para a sua origem. As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo`:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Você pode monitorar eventos de failover nos logs do Cloud Workers para solucionar problemas.

**Entendendo a lógica do Worker**

O Cloud Worker implementa a seguinte lógica:

1. **Detecção do agente do usuário:** verifica se o agente do usuário da solicitação recebida corresponde a algum dos bots agênticos definidos (sem distinção entre maiúsculas e minúsculas).

2. **Direcionamento de caminho:** filtra opcionalmente solicitações com base em caminhos direcionados. Por padrão, todas as páginas HTML (URLs que terminam com `/`, sem extensão ou `.html`) são roteadas. Você pode especificar caminhos específicos usando a matriz `TARGETED_PATHS`.

3. **Proteção contra loops:** o cabeçalho `x-edgeoptimize-request` evita loops infinitos. Quando o Edge Optimize envia solicitações de volta para sua origem, esse cabeçalho é definido como `"1"`, e o trabalhador encaminha a solicitação sem roteá-la de volta para o Edge Optimize.

4. **Segurança de cabeçalho:** antes de definir os cabeçalhos do Edge Optimize, o trabalhador remove quaisquer cabeçalhos `x-edgeoptimize-*` existentes da solicitação recebida para evitar ataques de injeção de cabeçalhos.

5. **Mapeamento de cabeçalho:** o trabalhador define os cabeçalhos necessários para o Edge Optimize:
   * `x-forwarded-host` – Identifica o domínio do site original.
   * `x-edgeoptimize-url` – Preserva o caminho da solicitação original e a string de consulta.
   * `x-edgeoptimize-api-key` – Autentica a solicitação com o Edge Optimize.
   * `x-edgeoptimize-config` – Fornece a configuração da chave de cache.

6. **Lógica de failover:** Se o Edge Optimize retornar qualquer código de status de erro (erros 4XX do cliente ou erros 5XX do servidor) ou se a solicitação falhar devido a um erro de rede, o worker executará automaticamente o failover para sua origem usando `EDGE_OPTIMIZE_TARGET_HOST`. A resposta de failover inclui o cabeçalho `x-edgeoptimize-fo: 1` para indicar que o failover ocorreu.

7. **Tratamento de redirecionamento:** a opção `redirect: "manual"` garante que as respostas de redirecionamento do Edge Otimize sejam passadas para o cliente sem que o trabalhador as siga.

**Personalizando a configuração**

Você pode personalizar o comportamento do trabalhador modificando as constantes de configuração na parte superior do código:

**Lista de bots agênticos**

Modifique a matriz `AGENTIC_BOTS` para adicionar ou remover agentes do usuário:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**Caminhos direcionados**

Por padrão, todas as páginas do HTML são roteadas para o Edge Otimize. Para limitar o roteamento a caminhos específicos, modifique a matriz `TARGETED_PATHS`:

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**Comportamentos de failover**

Por padrão, o trabalhador entra em failover sempre que ocorre um erro 4XX ou 5XX no Edge Optimize. Personalizar este comportamento:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Considerações importantes**

* **Comportamento de failover:** o trabalhador executará automaticamente o failover para sua origem se o Edge Otimize retornar qualquer erro (códigos de status 4XX ou 5XX) ou se a solicitação falhar devido a um erro de rede. O failover usa `EDGE_OPTIMIZE_TARGET_HOST` como o domínio de origem (semelhante ao `F_Default_Origin` do Fastly ou ao `Default_Origin` do CloudFront). As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo: 1`, que pode ser usado para monitoramento e depuração.

* **Armazenamento em cache:** o Cloudflare armazena em cache as respostas com base no URL por padrão. Como o tráfego agêntico recebe conteúdo diferente do tráfego humano, certifique-se de que a configuração de cache leve isso em consideração. Considere usar a API de cache ou cabeçalhos de cache para diferenciar o conteúdo armazenado em cache. O cabeçalho `x-edgeoptimize-config` deve ser incluído na sua chave de cache.

* **Limitação de taxa:** monitore seu uso do Edge Otimize e considere implementar a limitação de taxa para tráfego agêntico, se necessário.

* **Testes:** sempre teste a configuração em um ambiente de preparo antes de implantá-la na produção. Verifique se tanto o tráfego agêntico quanto o humano se comportam conforme o esperado. Teste o comportamento de failover simulando erros do Edge Optimize.

* **Logs:** habilite os logs do Cloudflare Workers para monitorar solicitações e solucionar problemas. Navegue até **Trabalhadores** > **seu trabalhador** > **Logs** para exibir os logs em tempo real. O trabalhador registra eventos de failover para fins de depuração.

**Resolução de Problemas**

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| Nenhum cabeçalho `x-edgeoptimize-request-id` na resposta | A rota do trabalhador não corresponde ou o agente de usuário não está na lista de bots agênticos. | Verifique se o padrão de rota corresponde ao URL da solicitação. Verifique se o agente do usuário está na matriz `AGENTIC_BOTS`. |
| Erros 401 ou 403 do Edge Otimize | Chave de API inválida ou ausente. | Verifique se `EDGE_OPTIMIZE_API_KEY` está definido corretamente nas variáveis e nos segredos do ambiente. Entre em contato com a Adobe para confirmar se a chave de API está ativa. |
| Redirecionamentos ou loops infinitos | O cabeçalho de proteção contra loops não está sendo definido ou verificado corretamente. | Certifique-se de que a verificação do cabeçalho `x-edgeoptimize-request` esteja em vigor. |
| Tráfego humano afetado | A lógica de roteamento do trabalhador é muito ampla. | Verifique se a lógica de correspondência do agente do usuário está correta e não diferencia maiúsculas de minúsculas. Verifique se `TARGETED_PATHS` está configurado corretamente. |
| Tempos de resposta lentos | Latência de rede para o back-end do Edge Optimize. | Isso é esperado para a primeira solicitação. As solicitações subsequentes são armazenadas em cache no Edge Otimize. |
| Cabeçalho `x-edgeoptimize-fo: 1` na resposta | O Edge Otimize retornou um erro e um failover para a origem ocorreu. | Verifique os logs do Cloud Workers para obter o código de erro específico. Verifique o status do serviço do Edge Optimize com a Adobe. |
| O failover não está funcionando | Sinalizadores de failover desabilitados ou erro na lógica de failover. | Verificar se `FAILOVER_ON_4XX` e `FAILOVER_ON_5XX` estão definidos como `true`. Verifique se há mensagens de erro nos logs do trabalhador. |
| Determinados caminhos não estão sendo otimizados | O caminho não corresponde aos caminhos direcionados ou ao padrão de página HTML. | Verifique se o caminho está em `TARGETED_PATHS` (se especificado) e corresponde ao padrão regex de página HTML. |
| Solicitações com falha devido a host inválido | `EDGE_OPTIMIZE_TARGET_HOST` inclui o protocolo (por exemplo, `https://`). | Use apenas o nome de domínio sem protocolo (por exemplo, `example.com`, não `https://example.com`). |
| Erro 530 durante failover | O Cloudflare não pode se conectar à origem ou a solicitação de failover tem cabeçalhos inválidos. | Certifique-se de que a função de failover remova os cabeçalhos do Edge Otimize. Verifique se a origem está acessível e se o DNS está configurado corretamente. |

**Permitir otimização na Edge por meio de regras de firewall (opcional)**

{{waf-allowlist-setup}}

**Verificar a configuração**

Após concluir a configuração, verifique se o tráfego de bots está sendo roteado para o Edge Optimize e se o tráfego humano permanece inalterado.

**1. Tráfego de bots de teste (deve ser otimizado)**

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

**2. Teste o tráfego humano (NÃO deve ser afetado)**

Simule uma solicitação regular de navegador humano:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

A resposta **não** deve conter o cabeçalho `x-edgeoptimize-request-id`. O conteúdo da página e o tempo de resposta devem permanecer idênticos aos de antes da habilitação da otimização na borda.

**3. Como diferenciar entre os dois cenários**

| Cabeçalho | Tráfego de bots (otimizado) | Tráfego humano (não afetado) |
|---|---|---|
| `x-edgeoptimize-request-id` | Presente — contém uma ID de solicitação exclusiva | Ausente |
| `x-edgeoptimize-fo` | Presente somente se houver um failover (valor: `1`) | Ausente |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
