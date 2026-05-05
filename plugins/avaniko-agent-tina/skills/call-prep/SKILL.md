---
name: call-prep
description: >
  This skill should be used when the user asks to "prep me for my call with [company]",
  "I'm meeting with [company] prep me", "call prep [company]", "get me ready for
  [meeting]", or needs an agenda and attendee research before a sales meeting.
metadata:
  version: "0.1.0"
  author: "Priyadharshan / Avaniko"
---

# Call prep

Produce a single-page brief for an upcoming sales call: who's attending, what they care about, where the deal stands, suggested agenda, and the one thing the rep must accomplish.

## When to invoke

Trigger on "prep me for [company]", "I'm meeting with [company]", "call prep", "ready me for the [name] meeting".

## Inputs to gather

In this order:

1. `~~calendar` — pull the meeting, attendees, time, prior link
2. `~~crm` — opportunity stage, last activity, prior notes, deal value
3. `~~email` — last 3 threads with attendees
4. `~~enrichment` or web — fill gaps on attendees not yet known
5. User-supplied context

If the meeting is not in `~~calendar`, ask the user for: company, attendees, meeting type, what they want from the call.

## Brief structure

### 1. Top line

One sentence: stage, value, last activity, the goal of this call.

### 2. Attendees

Per attendee: name, title, role on the buying side, recent public activity (talks, posts, hires), one personal/professional connection point.

### 3. Where we are

- Last meaningful interaction and what was promised
- Open questions from prior call
- Known objections
- Champion vs blocker mapping

### 4. Suggested agenda

3–5 line items, time-boxed. Tailor to meeting type:

- **Discovery** — open with confirmation of context, then 4–6 targeted discovery questions, close with timeline + next-step ask
- **Demo** — anchor on the 2 strongest pains found in discovery; cut anything tangential
- **Negotiation** — confirm decision criteria; pre-empt likely concessions; agree on close path
- **Renewal/upsell** — lead with value delivered; tie to expansion thesis

### 5. The one thing

The single outcome the rep needs from this call — not three, one.

### 6. Risks & curveballs

Anticipate hostile questions or objections. Prepare crisp answers.

## Output

Default to a concise markdown brief. Offer to save as a live artifact if the rep wants to re-open it on their phone before the call.

## Post-call

After the call, suggest the rep run the `call-summary` skill with their notes or transcript.
