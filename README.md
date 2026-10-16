# TenderKart for Claude

TenderKart helps businesses discover and research Indian government tenders from Claude. The plugin combines a workflow skill with TenderKart's remote MCP connector so Claude can search the tender corpus, review saved-filter updates, resolve tender references, inspect tender details, and prepare temporary document download links.

## What the plugin can do

- Search active and historical tenders by keywords, authority, location, category, value, status, and dates.
- List the authenticated account's saved filters and review tenders that changed in a filter.
- Resolve a portal tender ID or reference number and inspect the matching tender records.
- Read tender details, list available documents, and create a short-lived download link for an accessible document.

TenderKart is read-only in Claude. It cannot create or delete saved filters, change an account, purchase a subscription, submit a bid, or act on a government procurement portal. Users should verify deadlines, eligibility, corrigenda, and submission requirements against the official tender documents and source portal.

## Connection and data handling

The bundled connector uses OAuth at `https://tenderkart.in/mcp`. Each user signs in to TenderKart and authorizes Claude to access only the tender data available to that TenderKart account. The plugin contains no API keys or account credentials.

When Claude uses the connector, it sends the search criteria or identifiers needed for the requested task to TenderKart. TenderKart returns accessible saved-filter metadata, tender records, document metadata, or a temporary signed document URL. TenderKart's [privacy policy](https://tenderkart.in/privacy) and [terms of service](https://tenderkart.in/terms) apply.

For setup help, visit the [TenderKart MCP setup guide](https://tenderkart.in/mcp-setup) or [contact TenderKart support](https://tenderkart.in/contact).
