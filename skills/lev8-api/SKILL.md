---
name: lev8-api
description: Use the lev8 HTTP API and hosted MCP endpoint for Entity Search, Contact Search, and credit balance.
---

# lev8 API

Use this skill when a user asks to call lev8, configure the hosted lev8 MCP endpoint, or work with Entity Search, Contact Search, or credit balance.

## Authentication

- HTTP API base URL: `https://app.lev8.com`
- Hosted MCP endpoint: `https://api.lev8.com/mcp`
- Use `LEV8_API_KEY` for HTTP API calls and MCP Bearer authentication.
- Never print, echo, cat, grep with output, paste, or log a complete lev8 Token.

## Entity Search

Entity Search is asynchronous:

1. `POST /v1/entity-search/create_task`
2. `GET /v1/entity-search/status?leads_search_id=...`
3. `GET /v1/entity-search/fetch?leads_search_id=...&pts=0&num=5`

Continue fetching with the next `pts = pts + count`. Finish only when task status is `done` and local `pts >= ready_count`.

## Contact Search

Use `POST /v1/contact-search` to find one email or phone number. Put identity signals in `objective` when available.

## Credit Balance

Use `GET /v1/credit/balance` for a safe smoke test. Print only status codes or non-sensitive response fields.

## MCP

Configure the hosted MCP endpoint with Bearer authentication. The Token is transport auth, not a tool argument.

```bash
codex mcp add lev8 \
  --url https://api.lev8.com/mcp \
  --bearer-token-env-var LEV8_API_KEY
```

## References

- `/api-reference/entity-search`
- `/api-reference/contact-search`
- `/api-reference/credit-balance`
- `/mcp-reference`
