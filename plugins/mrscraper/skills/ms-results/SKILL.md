---
name: ms-results
description: "List or fetch scrape results (pagination, filters). Use after runs complete. If results contain another user's private/login data, handle carefully and remind user of compliance obligations."
compatibility: Requires MrScraper MCP with API token.
allowed-tools: mcp(mrscraper:get_all_results), mcp(mrscraper:get_result_by_id)
metadata:
  author: MrScraper
---

# Scrape Results

Browse or fetch results for: $ARGUMENTS

## Step 0: Sensitive / login-derived data

If results may include **account-private** or **login-gated** content, remind the user they are responsible for lawful use and retention. Do not exfiltrate credentials from result payloads.

## Step 1: List

```
get_all_results({
  token: "<MRSCRAPER_API_TOKEN>",
  sort_field: "updatedAt",
  sort_order: "DESC",
  page: 1,
  page_size: 10
})
```

Paginate with `page` when `meta.totalPage` > 1.

## Step 2: One result

```
get_result_by_id({
  token: "<MRSCRAPER_API_TOKEN>",
  result_id: "<uuid>"
})
```

## Step 3: Present

Summarize fields; report `status` and `error` on failures. Avoid huge JSON dumps unless requested.

## If MCP is unavailable

Stop. Enable MrScraper MCP and pass `token`.
