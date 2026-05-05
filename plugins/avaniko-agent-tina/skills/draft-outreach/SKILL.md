---
name: draft-outreach
description: >
  This skill should be used when the user asks to "draft outreach to [person]",
  "write a cold email to [prospect]", "reach out to [name]", "draft a message
  to [contact]", or needs a personalized email/LinkedIn message based on
  prospect research.
metadata:
  version: "0.1.0"
  author: "Priyadharshan / Avaniko"
---

# Draft outreach

Research a prospect, then draft personalized outreach that earns a reply. Default to email. LinkedIn or `~~chat` formats on request.

## When to invoke

Trigger on "draft outreach", "cold email to [name]", "reach out to [contact]", "write a message to [prospect]".

## Required context

Confirm before drafting:

- Who — name, company, role
- Why now — what changed for the prospect or for us
- What the rep is offering and to whom it's relevant
- Desired call to action (15-min intro, demo, intro to teammate, doc review)

If any of these are missing, ask once before drafting. Do not invent a "why now."

## Research pass

Pull from `~~enrichment`, `~~crm`, and web. Find at minimum:

- One specific, recent (90-day) thing about the prospect or their company
- One angle that connects what they care about to what we offer
- The right channel based on their footprint (active on email vs LinkedIn vs `~~chat`)

## Drafting rules

- Subject line under 50 chars, lowercase, no clickbait
- Open line references the specific thing — never "I came across your profile"
- Body under 110 words for cold; under 180 for warm
- One CTA. Concrete. Time-bounded if possible.
- No "I hope this email finds you well", no humble-brag stats walls, no AI-cliché phrases ("in today's fast-paced world")
- Reference the rep's company once. The prospect's interests at least twice.

## Variants

By default, produce three variants of similar length, different angles:

1. Pain-led — opens with their pain, ties to our solution
2. Insight-led — opens with a non-obvious observation about their market
3. Connection-led — opens with shared context (mutual contact, event, content)

Label each. Let the rep pick.

## Output

Markdown with subject + body for each variant. Note the source citations the personalization rests on so the rep can verify.

## Logging

If `~~crm` is connected, offer to log the outreach as an activity after the rep sends.
