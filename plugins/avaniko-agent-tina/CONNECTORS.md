# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~crm` might mean HubSpot, Salesforce, Close, or Pipedrive.

Plugins are tool-agnostic — they describe sales workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category   | Placeholder    | Common options                                     |
| ---------- | -------------- | -------------------------------------------------- |
| CRM        | `~~crm`        | HubSpot, Salesforce, Close, Pipedrive              |
| Chat       | `~~chat`       | Slack, Microsoft Teams, Discord                    |
| Email      | `~~email`      | Gmail, Outlook                                     |
| Calendar   | `~~calendar`   | Google Calendar, Outlook                           |
| Enrichment | `~~enrichment` | Clay, ZoomInfo, Similarweb, Apollo                 |
| Notes      | `~~notes`      | Notion, Confluence, Google Docs                    |

## Fallback behavior

When a connector is not configured, skills fall back to:

- Web search for company and person research
- User-supplied context pasted into chat
- File attachments (call notes, transcripts, CSV exports)

No skill hard-requires a specific connector.
