# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~crm` might mean HubSpot, Salesforce, Close, or Pipedrive.

Plugins are tool-agnostic — they describe sales workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category   | Placeholder    | Common options                                     |
| ---------- | -------------- | -------------------------------------------------- |
| CRM        | `~~crm`        | HubSpot, Salesforce, Close, Pipedrive              |
| Database   | `~~database`   | CData Connect AI (recommended), direct Postgres    |
| Chat       | `~~chat`       | Slack, Microsoft Teams, Discord                    |
| Email      | `~~email`      | Gmail, Outlook                                     |
| Calendar   | `~~calendar`   | Google Calendar, Outlook                           |
| Enrichment | `~~enrichment` | Clay, ZoomInfo, Similarweb, Apollo                 |
| Notes      | `~~notes`      | Notion, Confluence, Google Docs                    |

## CData Connect AI (for team performance & CRM queries)

The **team-performance** skill queries the Avaniko CRM database directly. The recommended connector is **CData Connect AI**, which exposes the Postgres CRM as a SQL-queryable MCP tool.

Connection used: `PostgreSQL1` (catalog), schema `public`. Tables: `users`, `activities`, `deals`, `leads`, `contacts`, `notes`.

To enable: install the CData Connect AI connector in Cowork and ensure the `PostgreSQL1` connection is configured pointing at your CRM database.

## Fallback behavior

When a connector is not configured, skills fall back to:

- Web search for company and person research
- User-supplied context pasted into chat
- File attachments (call notes, transcripts, CSV exports)

No skill hard-requires a specific connector.
