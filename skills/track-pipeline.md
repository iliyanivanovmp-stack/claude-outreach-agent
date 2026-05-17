---
name: track-pipeline
description: Show pipeline status summary and flag leads that need attention today.
---

## When to invoke

When operator asks for pipeline status, wants to see who replied, says "what's next", or at the start of the daily loop.

## Workflow

1. Read `leads/pipeline.csv`.

2. Group leads by status and count each:

```
To Research:  X leads
Researched:   X leads
Draft Ready:  X leads
Sent:         X leads
Replied:      X leads
Booked:       X leads
Dead:         X leads
```

3. Flag these (print as a separate list):
   - Leads with `sent_at` more than 3 days ago and no `replied_at` value: "Follow-up due"
   - Leads with a `replied_at` value and status not yet `Booked` or `Dead`: "Reply needs handling"

4. Ask: "Which status do you want to work on?"

## Example output

```
Pipeline: 47 leads total

To Research:  12
Researched:   8
Draft Ready:  3
Sent:         18
Replied:      4
Booked:       2
Dead:         0

Needs attention:
- 6 leads sent 3+ days ago, no reply yet (follow-up due)
- 4 leads replied, not yet handled

Which status do you want to work on?
```

## Follow-up logic

If the operator chooses to work on follow-ups, for each flagged lead:

1. Check if there is a reply. If yes, read it and decide: book, respond, or mark Dead.
2. If no reply after 3+ days: draft a short follow-up (2-3 lines, reference the first message, new angle or new CTA).
3. Follow the same approval flow as `/write-outreach` before sending.

Maximum 2 follow-ups per prospect. After that, mark `Dead` and move on.
