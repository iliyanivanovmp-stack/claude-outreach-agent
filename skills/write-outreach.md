---
name: write-outreach
description: Draft a personalized first-touch email for a researched prospect. Waits for operator approval before sending.
---

## When to invoke

When operator says `/write-outreach [name]` or during the daily loop for "Researched" leads.

## Message structure

**Subject line:**
- Specific, not clever
- Mentions their company name or something from the research
- 5-8 words max
- No: "Quick question", "Following up", "Thought of you"

**Body (5-7 lines, no paragraphs):**

Line 1: The signal. Not a compliment. The specific thing you noticed.
`Saw your post about [X].` or `Noticed [Company] just [signal].`

Line 2: The pain. One sentence.
`Most [role]s at that stage [common problem].`

Line 3: The offer. One sentence. Specific, not vague.
`We help [role]s [specific outcome] without [the thing they hate].`

Line 4: Social proof or result (optional, use if you have a real number).
`Done this for [N] [company types] in the last [timeframe].`

Line 5: The CTA. One question. Not "let's connect."
`Worth a [X]-minute call this week to show you how it works for your setup?`

## Message rules

- No: "I hope this finds you well", "I came across your profile", "we'd love to connect", "touching base", "reaching out because"
- One thought per line
- No bold, no bullet points, no subject: line repetition in the body
- Write in the operator's voice from `CLAUDE.md`. Short sentences. Direct.
- Total email under 100 words.

## Workflow

1. Pull the research brief for the prospect from the `notes` column in `leads/pipeline.csv`.
2. Draft subject + body using the brief's signal and pain hypothesis.
3. Print the draft.
4. Say: "Ready to send to [email]. Type 'send it' to confirm."
5. Wait. Do not send until the operator types explicit confirmation.
6. On confirmation: send via Gmail MCP. Log `sent_at` timestamp in `leads/pipeline.csv`. Set status to `Sent`.

## Example output

```
Subject: SDR productivity post

Hi Jamie,

Saw your post on SDR productivity last week. Most VP Sales teams at Series B find the research step is where the time goes.

We remove that step entirely. Reps get a pre-researched brief on every prospect before they pick up the phone.

Done this for 4 SaaS teams in the past 6 months. Average ramp time dropped by 30%.

Worth a 20-minute call this week to see if it fits your setup?

[Operator name]
[Cal link]
```

Ready to send to jamie@stackline.com. Type 'send it' to confirm.
