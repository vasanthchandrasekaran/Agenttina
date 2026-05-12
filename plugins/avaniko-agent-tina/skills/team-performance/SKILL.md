---
name: team-performance
description: >
  Use this skill when the user asks about team performance, rep activity,
  weekly numbers, leaderboard, who's active, how the team is doing, or
  wants to compare reps. Trigger on phrases like "team performance",
  "how is my team doing", "who's been active this week", "weekly numbers",
  "rep activity", "leaderboard", "who's behind", "top performer",
  "how many leads did [rep] create", "what did the team do this week".
metadata:
  version: "0.2.0"
  author: "Priyadharshan / Avaniko"
---

# Team performance

Query the CRM database and report on rep-level activity, leads, and deals for a given time window. Surface who is leading, who is behind, and anything anomalous.

## When to invoke

Trigger on: "team performance", "how is my team doing", "weekly numbers", "rep activity", "leaderboard", "who's active this week", "who's behind", "top performer", "how many leads did [rep] create", "what did the team do this week/month/today".

## Data source

Use `~~database` if connected (CData Connect AI with PostgreSQL1 is the standard Avaniko setup). If not connected, ask the user to paste a CSV export or provide a summary.

### CData Connect AI — confirmed schema (Avaniko CRM, PostgreSQL1)

Catalog: `PostgreSQL1`, Schema: `public`. Fully-qualified table format: `[PostgreSQL1].[public].[table]`.

| Table | Key columns |
|---|---|
| `users` | `id`, `name`, `email`, `role` |
| `activities` | `id`, `user_id`, `entity_type`, `entity_id`, `action`, `description`, `created_at` |
| `deals` | `id`, `owner_id`, `deal_name`, `company_name`, `value`, `stage`, `won_lost_status`, `created_at`, `last_activity` |
| `leads` | `id`, `owner_id`, `company_name`, `status`, `score`, `created_at`, `last_activity` |

## Default time window

"This week" = Monday of current ISO week through Sunday. "Today" = CURRENT_DATE. "This month" = date_trunc('month', CURRENT_DATE). Always state the window used.

## Queries — run all four in parallel

Replace `<WEEK_START>` (e.g. `'2026-05-11'`) and `<WEEK_END>` (e.g. `'2026-05-18'`).

### 1. Activities per rep
```sql
SELECT u.[name] AS rep,
       COUNT(a.[id]) AS activity_count,
       COUNT(DISTINCT a.[action]) AS action_types
FROM [PostgreSQL1].[public].[activities] a
INNER JOIN [PostgreSQL1].[public].[users] u ON a.[user_id] = u.[id]
WHERE a.[created_at] >= '<WEEK_START>' AND a.[created_at] < '<WEEK_END>'
GROUP BY u.[name]
ORDER BY activity_count DESC
```

### 2. Leads created per rep
```sql
SELECT u.[name] AS rep, COUNT(l.[id]) AS leads_created
FROM [PostgreSQL1].[public].[leads] l
INNER JOIN [PostgreSQL1].[public].[users] u ON l.[owner_id] = u.[id]
WHERE l.[created_at] >= '<WEEK_START>' AND l.[created_at] < '<WEEK_END>'
GROUP BY u.[name]
ORDER BY leads_created DESC
```

### 3. Deals created per rep
```sql
SELECT u.[name] AS rep,
       COUNT(d.[id]) AS deals_created,
       SUM(d.[value]) AS total_value
FROM [PostgreSQL1].[public].[deals] d
INNER JOIN [PostgreSQL1].[public].[users] u ON d.[owner_id] = u.[id]
WHERE d.[created_at] >= '<WEEK_START>' AND d.[created_at] < '<WEEK_END>'
GROUP BY u.[name]
ORDER BY deals_created DESC
```

### 4. Deals won per rep
```sql
SELECT u.[name] AS rep,
       COUNT(d.[id]) AS deals_won,
       SUM(d.[value]) AS won_value
FROM [PostgreSQL1].[public].[deals] d
INNER JOIN [PostgreSQL1].[public].[users] u ON d.[owner_id] = u.[id]
WHERE d.[won_lost_status] = 'won'
  AND d.[last_activity] >= '<WEEK_START>' AND d.[last_activity] < '<WEEK_END>'
GROUP BY u.[name]
ORDER BY deals_won DESC
```

## Output format

Three sections with compact tables:
1. **Activity Log** — rep, activity count, action variety
2. **Leads Created** — rep, count
3. **Deals** — rep, deals created, value, deals won, won value

Follow with 2–3 lines of plain-English commentary: who leads, anything anomalous, who has zero activity.

## Anomaly flags

- **Single action type with 100+ count**: likely bulk import or automation — flag it, don't count as human activity.
- **Leads created but no activities**: rep is prospecting but not logging follow-up.
- **Rep absent from all queries**: zero activity this week — name them explicitly, don't silently omit.

## Drill-down

If the user asks "what is [rep] working on?" or "show me [rep]'s deals":
```sql
SELECT d.[deal_name], d.[company_name], d.[stage], d.[value], d.[expected_close_date]
FROM [PostgreSQL1].[public].[deals] d
INNER JOIN [PostgreSQL1].[public].[users] u ON d.[owner_id] = u.[id]
WHERE u.[name] ILIKE '%<rep_name>%' AND d.[won_lost_status] IS NULL
ORDER BY d.[expected_close_date] ASC
LIMIT 20
```

If the user asks "what did [rep] log?":
```sql
SELECT a.[action], a.[description], a.[entity_type], a.[created_at]
FROM [PostgreSQL1].[public].[activities] a
INNER JOIN [PostgreSQL1].[public].[users] u ON a.[user_id] = u.[id]
WHERE u.[name] ILIKE '%<rep_name>%'
  AND a.[created_at] >= '<WEEK_START>' AND a.[created_at] < '<WEEK_END>'
ORDER BY a.[created_at] DESC
LIMIT 50
```

## Artifact offer

After delivering the answer, offer once: "Want me to turn this into a live dashboard you can check each morning?" If yes, use `mcp__cowork__create_artifact`.
