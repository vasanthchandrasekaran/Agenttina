# Avaniko Agent Tina

A sales co-pilot plugin for revenue teams. Helps with pipeline review, account research, call preparation, outreach drafting, and autonomous deal-health analysis.

## Components

### Skills

- **pipeline-review** — Weekly pipeline health check: prioritize deals, flag stale opportunities, surface single-threaded risks
- **account-research** — Research a target account or prospect and produce actionable sales intel
- **call-prep** — Prepare for a sales call with attendee research, account context, and a suggested agenda
- **draft-outreach** — Research a prospect then draft personalized cold or warm outreach

### Agents

- **deal-health-analyst** — Autonomous deal scoring across stage fit, engagement, stakeholder coverage, and timeline realism

## Setup

This plugin is tool-agnostic. It uses placeholders (`~~crm`, `~~chat`, `~~email`, `~~enrichment`) that resolve to whichever tools you connect. See `CONNECTORS.md` for the full mapping.

Recommended connectors:

- A CRM (HubSpot, Salesforce, Close, Pipedrive)
- Calendar / email (Google, Outlook)
- Chat (Slack, Microsoft Teams)
- Optional: enrichment (Clay, ZoomInfo, Similarweb)

If no connectors are available, every skill still works — it just falls back to web research and user-provided context.

## Usage

Trigger any skill by describing what you need:

- "Run my pipeline review"
- "Research Acme Corp"
- "Prep me for my call with [company]"
- "Draft outreach to [name] at [company]"
- "Check the health of the [deal name] deal"

## Customization

This plugin uses generic tool categories. To bind it to specific products in your stack, run the `cowork-plugin-customizer` skill or edit `CONNECTORS.md` directly.

## License

MIT
