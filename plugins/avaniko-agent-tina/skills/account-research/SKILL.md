---
name: account-research
description: >
  This skill should be used when the user asks to "research [company]",
  "look up [person]", "intel on [prospect]", "tell me about [account]",
  "who is [name] at [company]", or needs background on a target account
  or buyer before outreach or a meeting.
metadata:
  version: "0.1.0"
  author: "Priyadharshan / Avaniko"
---

# Account research

Build a sales-actionable profile of a target company or person. Focus on what helps the rep — buying signals, pain points, who to reach, what to say.

## When to invoke

Trigger on phrases like "research Acme", "tell me about [company]", "who is [name] at [company]", "intel on [prospect]", "look up [target]".

## Sources, in order of preference

1. `~~crm` for any existing record, prior activity, owner notes
2. `~~enrichment` for firmographics, technographics, intent data
3. Web search for news, hires, funding, exec moves, product launches
4. Public filings, press releases, blog posts, podcasts
5. User-supplied context

If `~~crm` already has a record, lead with what's known and add net-new signals on top — do not duplicate.

## What to produce

### Company snapshot

- Industry, employee count, revenue band, HQ
- Recent funding / financial events
- Tech stack (relevant to your offering)
- Org chart shape — flat vs hierarchical, where buying authority sits

### Buying signals (last 90 days)

- Leadership changes
- Funding rounds, M&A activity
- Product launches, expansion, hiring sprees
- Public statements about pain points your offering addresses
- Stack changes (added or churned a competitor)

### Key people

For each named contact: title, tenure, prior roles, public posts/talks, likely priorities, common ground (shared schools, employers, communities).

### Sales angle

In 3 bullets, the strongest reasons this account would buy now and from us. Tie each to a specific signal — never generic.

### Recommended next action

One concrete next step: send X to Y, request intro from Z, attend their upcoming event, etc.

## Output format

Default to markdown. If the user wants an artifact they can re-open, offer to save as a live page.

## Citation discipline

Cite every external claim with the source URL. If a fact comes from `~~crm`, label it as such. Never fabricate dates, headcount, or executive names — say "unverified" instead.
