---
name: find-leads
description: Find 10-20 prospects matching an ICP using Exa search. Appends results to leads/pipeline.csv.
---

## When to invoke

When the operator says `/find-leads [ICP description]` or asks for new leads.

## Workflow

1. Parse the ICP from the operator's message. If none given, read the ICP from `CLAUDE.md`.

2. Build 3-5 Exa search queries based on the ICP. Examples:
   - `"[role] at [company type] [location]"`
   - `"[company type] [buying signal]" site:linkedin.com`
   - `"[role]" "[company type]" funding OR hiring`

3. Run the searches. For each result, extract:
   - Full name
   - Company name
   - Role / title
   - LinkedIn URL (if found)
   - Email guess: `firstname@company.com` and `firstname.lastname@company.com`
   - The specific signal that surfaced them (e.g., "posted about hiring SDRs", "company raised $5M Series A")

4. Deduplicate across searches. Remove anyone already in `leads/pipeline.csv`.

5. Append new leads to `leads/pipeline.csv` with status `To Research`.

6. Report back: "Added X leads. Top 3 signals found: [list]."

## Output format (CSV row)

```
name, company, role, linkedin_url, email_guess, signal, status, notes, sent_at, replied_at
Jane Smith, Acme Corp, Head of Sales, https://linkedin.com/in/janesmith, jane@acmecorp.com, "posted about scaling SDR team to 5 reps", To Research, , ,
```

## If Exa is unavailable

Fall back to web search. Search Google for `site:linkedin.com/in "[role]" "[company type]"`. Extract profiles from results. Quality will be lower but the flow still works.
