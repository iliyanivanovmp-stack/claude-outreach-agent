# The Outreach Agent

## Replace $400-$1,000/month in outreach tools.
## One Claude Code subscription. One agent.

I was paying for Apollo, Instantly, and Hunter every month.
Then I built an agent that does all three.

This repo is that agent.

It runs inside Claude Code. It finds leads, researches them, writes personalized first-touch messages, sends via Gmail, and tracks everything in a CSV. No monthly SaaS fees. No dashboards you don't need. Just the work, done in your terminal.

**Who this is for:** Founders, agency owners, and solo operators running outbound who are tired of paying for 4-6 tools that barely talk to each other.

**What you get:** A working Claude Code outreach agent you install once and run every day.

---

## What this replaces

| Tool | Purpose | Typical monthly cost |
|---|---|---|
| Apollo.io | Lead finding + email sequences | $79-149 |
| Instantly | Email delivery + warmup | $37-97 |
| Hunter.io | Email finding + verification | $49 |
| Reply.io | Reply management + follow-ups | $60 |
| Phantombuster | LinkedIn scraping + data | $56 |
| Clay | AI enrichment columns | $149 |
| **Total** | | **$430-560+** |

Add LinkedIn Sales Navigator ($99/month) and you're over $600 before you've sent a single message.

This agent covers all of it with your existing Claude Code subscription plus a free Gmail MCP.

---

## Prerequisites

- Claude Code installed: `npm install -g @anthropic-ai/claude-code`
- Claude Pro or Max subscription (the $20/month one works)
- Gmail account for sending
- Exa API key: free tier gives you ~1,000 searches/month (exa.ai)

---

## Setup

**Step 1: Clone this repo**

```bash
git clone https://github.com/iliyanivanov/claude-outreach-agent
cd claude-outreach-agent
```

**Step 2: Copy the env file**

```bash
cp .env.example .env
```

Fill in your Exa API key. Gmail credentials come in Step 3.

**Step 3: Install the MCPs**

Open (or create) `~/.claude/mcp.json` and add:

```json
{
  "mcpServers": {
    "exa": {
      "command": "npx",
      "args": ["-y", "exa-mcp-server"],
      "env": { "EXA_API_KEY": "your-exa-key-here" }
    },
    "gmail": {
      "command": "npx",
      "args": ["-y", "@gptscript-ai/gmail-mcp-server"],
      "env": {
        "GMAIL_CLIENT_ID": "your-client-id",
        "GMAIL_CLIENT_SECRET": "your-client-secret",
        "GMAIL_REFRESH_TOKEN": "your-refresh-token"
      }
    }
  }
}
```

To get Gmail credentials:

1. Go to console.cloud.google.com and create a project
2. Enable the Gmail API
3. Create OAuth 2.0 credentials (Desktop App type)
4. Run the auth flow once to get your refresh token

Takes about 10 minutes the first time.

**Step 4: Install the skills**

```bash
cp -r skills/* ~/.claude/skills/
```

**Step 5: Open the agent**

```bash
claude
```

Then start with `/find-leads [describe your ICP]`.

Example: `/find-leads B2B SaaS founders, 10-50 employees, US-based, recently raised seed or Series A`

---

## Skills included

### `/find-leads`

Finds 10-20 prospects matching your ICP via Exa search. Writes results to `leads/pipeline.csv` with name, company, role, LinkedIn URL, email guess, and the signal that surfaced them.

### `/research-prospect`

Builds a 1-page brief on any prospect before you write to them. Pulls recent LinkedIn activity, company news, hiring signals, and funding rounds. Takes 60-90 seconds per lead. Updates pipeline status to "Researched."

### `/write-outreach`

Drafts a personalized first-touch email for a researched lead. Ties the opener to the specific signal from the research step. No templates. The output is a draft waiting for your approval before anything is sent.

### `/track-pipeline`

Shows your pipeline grouped by status. Flags leads sent 3+ days ago with no reply (time for a follow-up) and replies that need handling. Your lightweight CRM replacement.

---

## How the daily loop works

```
/find-leads [ICP]           → adds 10-20 leads to pipeline.csv
/research-prospect [name]   → builds the brief, updates status
/write-outreach [name]      → drafts the message, waits for your OK
[you approve]               → agent sends via Gmail, logs the timestamp
/track-pipeline             → shows what needs attention today
```

Nothing sends without your explicit approval. The agent drafts, you decide.

---

## What to expect

First week running daily: 50-100 personalized first-touch messages out the door.

From 1,000 sends:
- 5-15% open rate (personalization beats blasting)
- 3-8 conversations started
- 1-3 calls booked depending on your offer and ICP fit

These are benchmarks, not guarantees. Your ICP and offer do more work than the tool.

---

## Customize for your ICP

Edit `CLAUDE.md` and fill in your ICP under the `## ICP on file` section. The more specific you are, the better the agent's lead quality.

Bad: "SaaS companies"
Better: "B2B SaaS founders at 10-50 person companies who recently posted about scaling their sales team"

Also update `CLAUDE.md` with your name and company so the agent writes in your voice.

---

## Questions

Stuck? Hit me up. iliyan.ivanov.mp@gmail.com · [Book a call](https://aiessentials.us/)

If you want this running end-to-end for your agency, the [24/7 Pipeline Engine](https://aiessentials.us/24-7-pipeline-engine) handles the whole system for you.
