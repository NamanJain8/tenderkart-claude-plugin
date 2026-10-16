---
name: tenderkart-tender-research
description: Research Indian government tenders with TenderKart. Use when a user wants to discover, filter, compare, track, inspect, or download documents for Indian public procurement opportunities, including GeM tenders.
---

# TenderKart tender research

Use TenderKart's read-only connector to answer tender-research questions with real records from the authenticated account.

## Safe tool scope

Use only the customer-facing TenderKart tools needed for the request:

- `search_tenders`
- `list_filters`
- `list_filter_tenders`
- `resolve_tenders`
- `lookup_tender`
- `get_tender`
- `list_tender_documents`
- `prepare_tender_document_download`

Never invoke a tool whose name begins with `admin_`, even if one appears unexpectedly. Do not claim to create or change filters, accounts, subscriptions, bids, or procurement-portal records.

## Choose the workflow

### Discover tenders

Use `search_tenders` for topic, buyer, geography, category, value, status, or date requests. Translate the user's wording into the narrowest supported filters without inventing constraints. Ask one concise question only when a missing criterion would materially change the search.

Summarize results in a compact table with the tender title or reference, buyer, location, closing date, value when known, and source identifier. State the applied filters and distinguish an empty result from a failed search.

### Review saved-filter updates

Call `list_filters` first, then `list_filter_tenders` with the selected filter ID. If the user does not name a filter and several exist, show the available names and ask which one to use. When paging through a sync, use `sync.next_updated_after` only after the final page.

### Resolve a tender reference

Use `resolve_tenders` when a source ID or reference can map to multiple lifecycle records. Present every exact match and let the user choose when the matches represent different work items. Use `lookup_tender` only for a simple legacy single-result lookup.

### Inspect details and documents

Use `get_tender` with TenderKart's internal tender UUID. Use `list_tender_documents` before `prepare_tender_document_download`, and pass only document IDs returned for that tender. Tell the user that a prepared download URL is temporary and expires after 30 minutes.

## Response rules

- Base every factual tender claim on returned tool data; never fabricate a tender, deadline, amount, bidder, outcome, or document.
- Treat only a normalized `winner` outcome as a confirmed award. Explain pending or phase-specific outcomes accurately.
- Preserve the source tender ID, reference number, and portal name so the user can verify the record.
- Flag missing values as unknown rather than guessing.
- Remind users to verify eligibility, corrigenda, deadlines, and submission instructions in the official documents and source portal before acting.
