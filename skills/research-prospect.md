---
name: research-prospect
description: Build a 1-page brief on one prospect before writing outreach. Updates pipeline status to Researched.
---

## When to invoke

When operator says `/research-prospect [name]` or during the daily loop for leads in "To Research" status.

## Workflow

1. Find the prospect in `leads/pipeline.csv` by name.

2. Run Exa searches:
   - `"[name]" "[company]"` (general profile)
   - `site:linkedin.com "[name]" "[company]"` (LinkedIn activity)
   - `"[company]" funding OR "series A" OR "series B" OR hiring` (company signals)
   - `"[company]" site:techcrunch.com OR site:crunchbase.com` (press and funding)

3. Build the brief (see format below).

4. Update `leads/pipeline.csv`: set status to `Researched`, write the signal to the `notes` column.

5. Print the brief for the operator.

## Brief format

```
[Name] · [Role] at [Company]

Company: [What they do, estimated size, stage. 1 line.]
Recent signal: [The specific thing that makes now the right time. 1-2 lines.]
Pain hypothesis: [What problem they likely have that your offer addresses. 1 line.]
Message angle: [One sentence tying the signal to the pain. This becomes your opener.]
Email: [best email guess]
LinkedIn: [URL]
```

## Example output

```
Jamie Torres · VP Sales at Stackline

Company: E-commerce analytics SaaS, ~80 employees, Series B (raised $18M in Jan 2025)
Recent signal: Posted 3 days ago about "the SDR productivity problem" and struggling to hit 40 activities/day per rep
Pain hypothesis: Scaling outbound motion after Series B. Too much manual work per rep, quota attainment dropping.
Message angle: Saw your post on SDR productivity. Most teams at your stage fix this by removing the research step entirely.
Email: jamie@stackline.com / jamie.torres@stackline.com
LinkedIn: https://linkedin.com/in/jamie-torres-vp
```

## If no signal found

Note "No recent signal found" in the brief. Recommend waiting for a signal before reaching out, or using a generic pain-based opener. Flag it to the operator.
