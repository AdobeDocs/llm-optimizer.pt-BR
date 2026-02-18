---
title: Otimizar na Edge - Cloud Flare (BYOCDN)
description: Saiba como configurar o Cloudflare BYOCDN para otimizar no Edge no LLM Optimizer.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 1%

---


# Cloudflare (BYOCDN)

Essa configuração roteia o tráfego de agente (solicitações de bots de IA e agentes de usuário LLM) para o serviço de back-end de Otimização da Edge (`live.edgeoptimize.net`). Visitantes humanos e bots de SEO continuam a ser oferecidos de sua origem como de costume. Para testar a configuração, após a conclusão da instalação, procure o cabeçalho `x-edgeoptimize-request-id` na resposta.

**Pré-requisitos**

Antes de configurar as regras de roteamento do Cloud Worker, verifique se você:

* Uma conta CloudFlare com Workers ativados em seu domínio.
* Acesso às configurações de DNS do seu domínio no Cloud Flare.
* O processo de integração do LLM Optimizer foi concluído.
* Encaminhamento de log CDN concluído para o LLM Optimizer.
* Uma chave de API de otimização do Edge recuperada da interface do usuário do LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Como funciona o roteamento**

Quando configurada corretamente, uma solicitação para o seu domínio (por exemplo, `www.example.com/page.html`) de um agente de usuário agente é interceptada pelo Cloud Worker e roteada para o back-end do Edge Otimize. A solicitação de backend inclui os cabeçalhos necessários.

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
| `x-edgeoptimize-url` | O caminho do URL original e a sequência de consulta da solicitação. | `/page.html` ou `/products?id=123` |
| `x-edgeoptimize-api-key` | A chave de API fornecida pela Adobe para o seu domínio. | `your-api-key-here` |
| `x-edgeoptimize-config` | String de configuração para diferenciação da chave de cache. | `LLMCLIENT=TRUE;` |

**Etapa 1: Criar o Trabalho da Cloudflare**

1. Faça logon no painel do Cloud.
2. Navegue até **Trabalhadores e páginas** na barra lateral.
3. Clique em **Criar aplicativo** e depois em **Criar Trabalhador**.
4. Nomeie seu trabalhador (por exemplo, `edge-optimize-router`).
5. Clique em **Implantar** para criar o trabalhador com o código padrão.

![Painel de Trabalhadores em Nuvem](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Etapa 2: adicionar o código do Trabalhador**

Depois de criar o trabalhador, clique em **Editar código** e substitua o código padrão pelo seguinte:

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

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

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

**Etapa 3: configurar variáveis de ambiente**

As variáveis de ambiente armazenam configurações confidenciais como sua chave de API com segurança.

1. Nas configurações do seu trabalhador, navegue até **Configurações** > **Variáveis**.
2. Em **Variáveis de Ambiente**, clique em **Adicionar variável**.
3. Adicione as seguintes variáveis:

   | Nome da variável | Descrição | Obrigatório |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Sua chave de API de otimização Edge fornecida pela Adobe. | Sim |
   | `EDGE_OPTIMIZE_TARGET_HOST` | O host de destino para as solicitações de Otimização do Edge (enviadas como cabeçalho `x-forwarded-host`) e o domínio de origem para failover. Deve ser somente o domínio sem protocolo (por exemplo, `www.example.com`, não `https://www.example.com`). | Sim |

4. Para a chave de API, clique em **Criptografar** para armazená-la com segurança.
5. Clique em **Salvar e implantar**.

![Variáveis de ambiente de nuvem](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Etapa 4: adicionar uma rota ao seu domínio**

Para ativar o worker no seu domínio:

1. Vá para as **Configurações** > **Acionadores** do seu trabalhador.
2. Em **Rotas**, clique em **Adicionar rota**.
3. Insira seu padrão de domínio (por exemplo, `www.example.com/*` ou `example.com/*`).
4. Selecione sua zona na lista suspensa.
5. Clique em **Salvar**.

Como alternativa, você pode configurar rotas no nível da zona:

1. Navegue até o domínio no Cloud Flare.
2. Vá para **Rotas dos Trabalhadores**.
3. Clique em **Adicionar rota** e especifique o padrão e o trabalhador.

![Rotas de Trabalho da Cloudflare](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Verificando o comportamento de failover**

Se o Edge Otimize estiver indisponível ou retornar um erro, o worker efetuará automaticamente o failover para sua origem. As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo`:

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Você pode monitorar eventos de failover nos logs do Cloud Workers para solucionar problemas.

**Entendendo a lógica do Worker**

O Cloud Worker implementa a seguinte lógica:

1. **Detecção do Agente do Usuário:** verifica se o agente do usuário da solicitação recebida corresponde a qualquer um dos bots de agente definidos (não diferencia maiúsculas de minúsculas).

2. **Direcionamento de caminho:** filtra opcionalmente solicitações com base em caminhos direcionados. Por padrão, todas as páginas do HTML (URLs terminadas com `/`, sem extensão ou `.html`) são roteadas. Você pode especificar caminhos específicos usando a matriz `TARGETED_PATHS`.

3. **Proteção de loop:** O cabeçalho `x-edgeoptimize-request` impede loops infinitos. Quando o Edge Otimize faz solicitações de volta à sua origem, esse cabeçalho é definido como `"1"` e o trabalhador transmite a solicitação sem roteá-la de volta para o Edge Otimize.

4. **Segurança de cabeçalho:** Antes de configurar cabeçalhos Edge Otimize, o trabalhador remove todos os cabeçalhos `x-edgeoptimize-*` existentes da solicitação de entrada para evitar ataques de injeção de cabeçalho.

5. **Mapeamento de cabeçalho:** o trabalhador define os cabeçalhos necessários para a Otimização Edge:
   * `x-forwarded-host` - Identifica o domínio do site original.
   * `x-edgeoptimize-url` - Preserva o caminho da solicitação original e a sequência de consulta.
   * `x-edgeoptimize-api-key` - Autentica a solicitação com o Otimize do Edge.
   * `x-edgeoptimize-config` - Fornece a configuração da chave de cache.

6. **Lógica de failover:** se o Edge Otimize retornar qualquer código de status de erro (erros de cliente 4XX ou erros de servidor 5XX) ou a solicitação falhar devido a um erro de rede, o trabalhador efetuará automaticamente o failover para sua origem usando `EDGE_OPTIMIZE_TARGET_HOST`. A resposta de failover inclui o cabeçalho `x-edgeoptimize-fo: 1` para indicar que o failover ocorreu.

7. **Tratamento de redirecionamento:** a opção `redirect: "manual"` garante que as respostas de redirecionamento do Edge Otimize sejam passadas para o cliente sem que o trabalhador as siga.

**Personalizando a configuração**

Você pode personalizar o comportamento do trabalhador modificando as constantes de configuração na parte superior do código:

**Lista de bots de agente**

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

**Configuração de failover**

Por padrão, o trabalhador falha em qualquer erro 4XX ou 5XX do Edge Otimize. Personalizar este comportamento:

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

* **Comportamento de failover:** o trabalhador executará automaticamente o failover de sua origem se o Edge Otimize retornar qualquer erro (códigos de status 4XX ou 5XX) ou se a solicitação falhar devido a um erro de rede. O failover usa `EDGE_OPTIMIZE_TARGET_HOST` como o domínio de origem (semelhante ao `F_Default_Origin` do Fastly ou ao `Default_Origin` do CloudFront). As respostas de failover incluem o cabeçalho `x-edgeoptimize-fo: 1`, que pode ser usado para monitoramento e depuração.

* **Armazenamento em cache:** o Cloud Flare armazena em cache as respostas com base na URL por padrão. Como o tráfego de agente recebe conteúdo diferente do tráfego humano, certifique-se de que a configuração de cache tenha em conta isso. Considere usar a API de cache ou cabeçalhos de cache para diferenciar o conteúdo em cache. O cabeçalho `x-edgeoptimize-config` deve ser incluído na sua chave de cache.

* **Limitação de taxa:** monitore seu uso do Edge Otimize e considere implementar a limitação de taxa para tráfego de agente, se necessário.

* **Testando:** sempre teste a configuração em um ambiente de preparo antes de implantar em produção. Verifique se o tráfego de agentes e humanos se comportam conforme esperado. Teste o comportamento de failover simulando erros de Otimização do Edge.

* **Logs:** Habilite o log de Trabalhadores em Nuvem para monitorar solicitações e solucionar problemas. Navegue até **Workers** > **seu worker** > **Logs** para exibir os logs em tempo real. O trabalhador registra eventos de failover para fins de depuração.

**Resolução de Problemas**

| Problema | Causa possível | Solução |
|-------|----------------|----------|
| Nenhum cabeçalho `x-edgeoptimize-request-id` na resposta | A rota do trabalhador não corresponde ou o agente de usuário não está na lista de bots de agente. | Verifique se o padrão de rota corresponde ao URL da solicitação. Verifique se o agente do usuário está na matriz `AGENTIC_BOTS`. |
| Erros 401 ou 403 do Edge Otimize | Chave de API inválida ou ausente. | Verifique se `EDGE_OPTIMIZE_API_KEY` está definido corretamente nas variáveis de ambiente. Entre em contato com a Adobe para confirmar se a chave de API está ativa. |
| Redirecionamentos ou loops infinitos | O cabeçalho de proteção contra loop não está sendo definido ou foi verificado corretamente. | Verifique se a verificação do cabeçalho `x-edgeoptimize-request` está em vigor. |
| Tráfego humano afetado | A lógica de roteamento do trabalhador é muito ampla. | Verifique se a lógica de correspondência do agente do usuário está correta e não diferencia maiúsculas de minúsculas. Verifique se `TARGETED_PATHS` está configurado corretamente. |
| Tempos de resposta lentos | Latência de rede para o back-end de Otimização do Edge. | Isso é esperado para a primeira solicitação; as solicitações subsequentes são armazenadas em cache no Edge Otimize. |
| Cabeçalho `x-edgeoptimize-fo: 1` na resposta | O Edge Otimize retornou um erro e ocorreu failover para a origem. | Verifique os logs do Cloud Workers para obter o código de erro específico. Verifique o status do serviço de Otimização do Edge com o Adobe. |
| O failover não está funcionando | Sinalizadores de failover desabilitados ou erro na lógica de failover. | Verificar se `FAILOVER_ON_4XX` e `FAILOVER_ON_5XX` estão definidos como `true`. Verifique se há mensagens de erro nos logs do trabalhador. |
| Determinados caminhos não estão sendo otimizados | Caminho não correspondente aos caminhos direcionados ou ao padrão de página do HTML. | Verifique se o caminho está em `TARGETED_PATHS` (se especificado) e corresponde ao padrão regex da página do HTML. |
| Solicitações que falham com host inválido | `EDGE_OPTIMIZE_TARGET_HOST` inclui o protocolo (por exemplo, `https://`). | Use apenas o nome de domínio sem protocolo (por exemplo, `example.com`, não `https://example.com`). |
| Erro 530 durante failover | A nuvem não pode se conectar à origem ou a solicitação de failover tem cabeçalhos inválidos. | Certifique-se de que a função de failover remova os cabeçalhos Edge Otimize. Verifique se a origem está acessível e se o DNS está configurado corretamente. |

{{verify-setup-byocdn}}

{{return-to-overview}}
