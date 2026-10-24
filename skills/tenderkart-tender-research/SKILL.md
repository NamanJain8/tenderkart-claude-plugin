---
name: tenderkart-tender-research
description: Research Indian government tenders with Tenderkart. Use when a user wants to discover, filter, compare, track, inspect, or download documents for Indian public procurement opportunities, including GeM tenders.
---

# Tenderkart tender research

Use Tenderkart's read-only connector to answer tender-research questions with real records from the authenticated account.

## Safe tool scope

Use only the customer-facing Tenderkart tools needed for the request:

- `search_tenders`
- `list_filters`
- `list_filter_tenders`
- `resolve_tenders`
- `get_tender`
- `list_tender_documents`
- `prepare_tender_document_download`
- `read_tender_document`

Never invoke a tool whose name begins with `admin_`, even if one appears unexpectedly. Do not claim to create or change filters, accounts, subscriptions, bids, or procurement-portal records.

## Choose the workflow

### Discover tenders

Use `search_tenders` for topic, buyer, geography, category, value, status, or date requests. Translate the user's wording into the narrowest supported filters without inventing constraints. Ask one concise question only when a missing criterion would materially change the search.

Send keywords and excluded keywords as arrays of text phrases, for example `["vehicle hire"]`. Use at most 20 keywords, each at most 120 characters. Choose `sort` from the tool schema; `publish_date_asc` means oldest publication first. Pages are 1–5 and each returns at most 50 rows (10 on Free). Read `pagination.summary`: `total` counts all matches while `pages` counts accessible pages. Follow `pagination.next_call` sequentially only when present, keeping the same criteria and effective limit. If `pagination.limited` is true, tell the user these are partial results, even if another accessible page exists. When no next call is returned, stop paging; refine criteria only to focus on the user's needs. Do not invent a page 6 or promise a complete export.

Summarize results in a compact table with the tender title or reference, buyer, location, closing date, value when known, and source identifier. State the applied filters and distinguish an empty result from a failed search.

### Browse saved-filter matches

Call `list_filters` and choose the saved filter the user means, then call `search_tenders` with its `filter_id`. This preserves all saved criteria, including publication/closing dates and statuses. With `filter_id`, send only `sort`, `page`, and `limit`; do not add explicit search criteria or reconstruct the saved filter. Use relevance for best keyword matches, `publish_date_desc` for newest publications, or the requested supported sort. Follow the same pagination guidance as an explicit search. If the connected server does not yet advertise `filter_id` on `search_tenders`, explain that saved-filter browsing requires the updated connector. Do not substitute change sync for browsing.

### Review saved-filter updates

Use this workflow only for change tracking or synchronization. Call `list_filters` first, then `list_filter_tenders` with the selected filter ID. This existing tool ignores saved publication/closing date filters, defaults to active status, and orders by oldest `updated_at` first. If the user does not name a filter and several exist, show the available names and ask which one to use. For continuation, follow `pagination.next_call` when provided. Older server responses use `filter_id` and `pagination.next_cursor` copied exactly; omit status and date bounds. Use `sync.next_updated_after` only when returned. If `pagination.limited` is true, the sync is incomplete: narrow its date window and do not advance the checkpoint.

### Resolve a tender reference

Use `resolve_tenders` when a source ID or reference can map to multiple lifecycle records. Present every exact match and let the user choose when the matches represent different work items. Then call `get_tender` with the chosen match's `id` for full details.

### Analyse a tender or check eligibility

Read the tender's documents as described below, starting with the notice inviting tender (NIT) and any corrigenda. Base eligibility answers on the document text and cite the file and page.

### Inspect details and documents

Copy document IDs exactly as returned. Never reconstruct or shorten an ID.

Use `get_tender` with Tenderkart's internal tender UUID. Use `list_tender_documents` first, and pass only document IDs returned for that tender. To read a document in Claude, call `prepare_tender_document_download`, download the file from the link it returns, and read the downloaded file; the link is signed and needs no sign-in. Fall back to `read_tender_document` only when the download fails or you cannot download files. In ChatGPT, use `read_tender_document`. It returns the text page by page (PDF including scanned pages, Word, Excel, and every file inside a zip); pass `next_start` to read on, and cite the file and page. Download links expire after 30 minutes; when the user wants the file, give them the link and say so.

## Allowances

Searches (`search_tenders`, `list_filter_tenders`) and tender lookups (`get_tender`, `resolve_tenders`, `list_tender_documents`, `read_tender_document`) each have a daily allowance, or a weekly one with the MCP Access add-on. Successful calls count, repeats included, so reuse results already in the conversation instead of calling again. Document downloads count against the account's monthly allowance. Prefer one well-filtered search to many broad ones. A search or sync returns its first 5 pages only; for more, search again with more specific keywords or filters. Tender details name the winners and award value of an awarded tender, not every bidder. When a tool says a limit is reached, or that something is hidden on the account's plan, tell the user exactly that, and do not retry or try to work around it. In ChatGPT, share only the informational help link returned by the tool; do not promote subscription upgrades or start a purchase flow.

## Response rules

- Base every factual tender claim on returned tool data; never fabricate a tender, deadline, amount, bidder, outcome, or document.
- Treat only a normalized `winner` outcome as a confirmed award. Explain pending or phase-specific outcomes accurately.
- Preserve the source tender ID, reference number, and portal name so the user can verify the record.
- Flag missing values as unknown rather than guessing.
- Remind users to verify eligibility, corrigenda, deadlines, and submission instructions in the official documents and source portal before acting.
