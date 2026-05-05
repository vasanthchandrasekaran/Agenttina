---
name: pipeline-review
description: >
  This skill should be used when the user asks to "run a pipeline review",
  "review my pipeline", "what's at risk this week", "weekly pipeline check",
  "prioritize my deals", or "audit pipeline hygiene". Use when a salesperson
  needs a prioritized action plan across their open opportunities.
metadata:
  version: "0.1.0"
  author: "Priyadharshan / Avaniko"
---

# Pipeline review

Analyze pipeline health and produce a prioritized weekly action plan. Surface deals that need attention, flag hygiene issues, and recommend specific next steps.

## When to invoke

Trigger on phrases like "pipeline review", "what's at risk", "audit my pipeline", "which deals should I focus on", "weekly pipeline".

## Inputs to gather

Pull pipeline data in this order of preference:

1. From `~~crm` if connected — query open opportunities for the current user
2. From a CSV the user attaches
3. From the user's pasted notes

For each deal, expect: name, account, stage, amount, close date, owner, last activity, next step, key contacts.

## Analysis framework

Score each deal across four dimensions:

1. **Stage fit** — does activity match stage? (e.g., a "Negotiation" deal with no proposal is suspect)
2. **Recency** — last meaningful activity within stage SLA?
3. **Stakeholder coverage** — single-threaded vs multi-threaded
4. **Timeline realism** — close date plausible given remaining steps?

Flag any deal that fails 2+ dimensions as **at risk**.

## Hygiene checks

- Close date in the past or > 90 days out with no recent movement
- Amount missing or suspiciously round
- No next step recorded
- Stage stuck > 2× median for that stage
- Single contact only

## Output

Produce three sections:

### Top 5 focus deals
Rank by combination of dollar value × close-date proximity × winnability. For each: deal name, amount, close date, why it matters this week, recommended action.

### At-risk deals
List any deal flagged at-risk with the specific failure mode and a recovery action.

### Hygiene cleanup
List CRM hygiene issues that need fixing, grouped by type.

## Logging

If `~~crm` is connected, offer to update next-step fields for the user after they confirm the action plan. Do not write to `~~crm` without explicit confirmation.

If `~~chat` is connected and the user wants to share, offer to post a summary to their preferred channel.
