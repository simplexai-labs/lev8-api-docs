---
name: lev8-api
description: Find people, companies, KOLs/creators, Shopify stores, and contact details through hosted Lev8 MCP tools.
---

# Lev8 MCP

Use this skill when a user asks to configure the hosted Lev8 MCP endpoint, find people, find companies, find KOLs or creators, find Shopify stores, or find contact details through MCP tools.

## Authentication

- Hosted MCP endpoint: `https://api.lev8.com/mcp`
- Use `LEV8_API_KEY` for MCP Bearer authentication.
- Never print, echo, cat, grep with output, paste, or log a complete lev8 Token.

## Entity Search

Entity Search is asynchronous. Use the MCP tools in this order:

1. `entity_search_create`
2. `entity_search_status`
3. `entity_search_fetch`

Continue fetching with the next `pts = pts + count`. Finish only when task status is `done` and local `pts >= ready_count`.

## Contact Search

Use `contact_search` to find one email or phone number. Put identity signals in `objective` when available.

## Credit Balance

Use `credit_balance` when the user asks to check available credits. Print only non-sensitive response fields.

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
