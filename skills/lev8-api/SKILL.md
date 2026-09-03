---
name: lev8-api
description: Search entities and contacts, research questions, enrich records, and extract public lists through hosted Lev8 MCP tools.
---

# Lev8 MCP

Use this skill when a user asks to configure the hosted Lev8 MCP endpoint, find people, companies, creators, Shopify stores, Xiaohongshu accounts, WeChat Official Accounts, or contact details, answer research questions, enrich an entity, or extract social, GitHub, or public web-page lists.

## Authentication

- Hosted MCP endpoint: `https://app.lev8.com/mcp`
- Use `LEV8_API_KEY` for MCP Bearer authentication.
- Never print, echo, cat, grep with output, paste, or log a complete lev8 Token.

## Entity Search

Entity Search is asynchronous. Use the MCP tools in this order:

1. `entity_search_create`
2. `entity_search_status`
3. `entity_search_fetch`

Continue fetching with the next `pts = pts + count`. Finish only when task status is `done` or `error` and local `pts >= ready_count`.

Supported `entity_type` values are `person`, `company`, `twitter_creator`, `youtube_creator`, `tiktok_creator`, `instagram_creator`, `shopify_store`, `xiaohongshu`, and `wechat`. Use `wechat` for WeChat Official Account search.

For `entity_type: "xiaohongshu"` or `entity_type: "wechat"`, pass `enable_web_search: true`. Requests that omit `enable_web_search` or set it to `false` fail validation. Xiaohongshu and WeChat Official Account searches usually take 1 to 2 minutes before results are ready, so keep polling instead of creating a duplicate task.

## Contact Search

Use `contact_search` to find one email or phone number. Put identity signals in `objective` when available.

## Deep Search

Use `deep_search` for an open-ended research question. Treat `answer` as dynamic, non-null JSON: pass it through or inspect it at runtime instead of requiring a string or fixed object fields.

## Enrich

Use `enrich` when the user already has entity context and wants structured fields. Supply a non-empty object JSON Schema in `enrich_fields` and interpret `answer` using that caller-provided schema.

## Extract

Use `extract` for supported social or GitHub lists, or use `type: web2list` with an instruction and public HTTP or HTTPS URL. Social and GitHub limits default to 100 and may be at most 10000; web2list normalizes the limit to 100.

## Credit Balance

Use `credit_balance` when the user asks to check available credits. Print only non-sensitive response fields.

## MCP

Configure the hosted MCP endpoint with Bearer authentication. The Token is transport auth, not a tool argument.

```bash
codex mcp add lev8 \
  --url https://app.lev8.com/mcp \
  --bearer-token-env-var LEV8_API_KEY
```

## References

- `/api-reference/entity-search`
- `/api-reference/contact-search`
- `/api-reference/deep-search`
- `/api-reference/enrich`
- `/api-reference/extract`
- `/api-reference/credit-balance`
- `/mcp-reference`
