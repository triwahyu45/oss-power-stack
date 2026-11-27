# 5 Agent MCP Connectors & Free Local-First Alternatives

> Distilled & upgraded for **100% free, local-first execution** — showing both the standard MCP connectors and zero-key open-source self-hosted/local alternatives.

---

## 1. Playwright MCP (`microsoft/playwright-mcp`) — 100% Free & Local

- **Repository**: [`microsoft/playwright-mcp`](https://github.com/microsoft/playwright-mcp) (`Apache-2.0`)
- **What it does**: Gives the agent accessibility-tree browser control (click, fill forms, E2E UI verification, screenshot capture, app automation without needing an API).
- **Zero-Key Setup**:
  ```json
  {
    "mcpServers": {
      "playwright": {
        "command": "npx",
        "args": ["-y", "@playwright/mcp@latest"]
      }
    }
  }
  ```
- **Note**: Install browser binaries once if needed (`npx playwright install`).

---

## 2. Firecrawl MCP (`firecrawl/firecrawl-mcp-server`) → Free Local Alternative: `Crawl4AI`

- **Hosted / Self-Hostable MCP**: [`firecrawl/firecrawl-mcp-server`](https://github.com/firecrawl/firecrawl-mcp-server) (free tier or Docker self-host; uses `$FIRECRAWL_API_KEY`).
  ```json
  {
    "mcpServers": {
      "firecrawl": {
        "command": "npx",
        "args": ["-y", "firecrawl-mcp"],
        "env": {
          "FIRECRAWL_API_KEY": "${FIRECRAWL_API_KEY}"
        }
      }
    }
  }
  ```
- **Free Local-First OSS Alternative (`Crawl4AI`)**: [`unclecode/crawl4ai`](https://github.com/unclecode/crawl4ai) (`Apache-2.0`, zero API keys) — runs local Playwright to extract clean Markdown, competitor pages, and brand assets offline/locally:
  ```bash
  pip install crawl4ai && crawl4ai-setup
  ```

---

## 3. PostHog MCP (`PostHog/mcp`) → Lightweight OSS Alternative: `Umami`

- **Hosted / Self-Hostable MCP**: [`PostHog/mcp`](https://github.com/PostHog/mcp) (generous free tier or self-hosted; product analytics, session replays, error tracking, SQL queries).
- **Quick Setup Wizard**:
  ```bash
  npx @posthog/wizard@latest mcp add
  ```
- **Manual Config** (uses `$POSTHOG_AUTH_HEADER` from local env):
  ```json
  {
    "mcpServers": {
      "posthog": {
        "command": "npx",
        "args": ["-y", "mcp-remote@latest", "https://mcp.posthog.com/mcp", "--header", "Authorization:${POSTHOG_AUTH_HEADER}"],
        "env": {
          "POSTHOG_AUTH_HEADER": "${POSTHOG_AUTH_HEADER}"
        }
      }
    }
  }
  ```
- **Lightweight Self-Hosted OSS Alternative**: [`umami-software/umami`](https://github.com/umami-software/umami) (`MIT`, simple privacy-first web analytics without heavy event pipelines).

---

## 4. Perplexity MCP → Free Local Alternative: `SearXNG` + Built-in Web Search

- **Caveat**: Official Perplexity MCP requires a **paid** Perplexity API key (`$PERPLEXITY_API_KEY`).
- **Free Local-First OSS Alternative (`SearXNG`)**: [`searxng/searxng`](https://github.com/searxng/searxng) (`AGPL-3.0`) — self-hosted privacy-respecting meta-search engine with local JSON API (`?format=json`), or pair directly with built-in agent `search_web` + `Crawl4AI` for zero-cost deep research.
  ```bash
  docker run -d -p 8080:8080 searxng/searxng:latest
  ```

---

## 5. Composio MCP (`ComposioHQ/composio`) → Self-Hostable OSS Alternatives: `n8n` / `Activepieces`

- **Hosted / Free-Tier MCP**: [`ComposioHQ/composio`](https://github.com/ComposioHQ/composio) (free tier; connects agents to 1,000+ SaaS apps via one managed OAuth bridge using `$COMPOSIO_API_KEY`).
- **Self-Hostable OSS Alternatives (Full Local Control)**:
  - [`n8n-io/n8n`](https://github.com/n8n-io/n8n) — visual workflow automation with 400+ integrations & native MCP server/client triggers.
  - [`activepieces/activepieces`](https://github.com/activepieces/activepieces) (`MIT`) — open-source Zapier/Make alternative with MCP toolkits you can self-host via Docker.
