# Tenderkart for Claude and ChatGPT

Tenderkart helps businesses discover and research Indian government tenders from Claude and ChatGPT. The plugin combines a workflow skill with Tenderkart's remote MCP connector so the assistant can search the tender corpus, review saved-filter updates, resolve tender references, inspect tender details, read a document's text page by page, and prepare temporary download links. The assistant can analyse the returned documents with file and page references.

## What the plugin can do

- Search active and historical tenders by keywords, authority, location, category, value, status, and dates.
- Browse the authenticated account's saved-filter matches with saved dates and statuses, or separately sync tender changes.
- Resolve a portal tender ID or reference number and inspect the matching tender records.
- Read tender details, list available documents, read their text, and create a short-lived download link for an accessible document.

Tenderkart is read-only in Claude and ChatGPT. It cannot create or delete saved filters, change an account, purchase a subscription, submit a bid, or act on a government procurement portal. Users should verify deadlines, eligibility, corrigenda, and submission requirements against the official tender documents and source portal.

## Connection and data handling

The bundled connector uses OAuth at `https://tenderkart.in/mcp`. Each user signs in to Tenderkart and authorizes their assistant to access only the tender data available to that Tenderkart account. Any Tenderkart account can connect, free or paid; what the assistant sees and how many requests it can make follow the account's plan. The plugin contains no API keys or account credentials.

When the assistant uses the connector, it sends the search criteria or identifiers needed for the requested task to Tenderkart. Tenderkart returns accessible saved-filter metadata, tender records, document metadata and text, or a temporary signed document URL. Tenderkart's [privacy policy](https://tenderkart.in/privacy) and [terms of service](https://tenderkart.in/terms) apply.

For setup help, visit the [Tenderkart MCP setup guide](https://tenderkart.in/mcp-setup) or [contact Tenderkart support](https://tenderkart.in/contact).
