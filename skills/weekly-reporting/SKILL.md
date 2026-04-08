---
schema: agentcompanies/v1
kind: skill
slug: weekly-reporting
name: Weekly Status Reporting
description: Standard format all agents use to post weekly status to CEO — consistent structure, no prose fluff
license: MIT
metadata:
  paperclip:
    tags:
      - operations
      - reporting
      - async
---

# Weekly Status Reporting

Every agent posts a status report at the end of their heartbeat. CEO reads these to synthesize the company view without asking anyone for updates.

## When to Post

At the **end of every heartbeat run**, create a Paperclip issue or comment assigned to `ceo` with the subject:

```
[AGENT SLUG] Weekly Status — Week of [YYYY-MM-DD]
```

## Required Format

Copy this template exactly. Do not add prose or explanation outside these fields.

```
AGENT: [your slug]
PERIOD: [YYYY-MM-DD] to [YYYY-MM-DD]

DONE:
- [completed item 1]
- [completed item 2]

IN PROGRESS:
- [item] — [ETA or % complete]

BLOCKED:
- [item] — [what you need, from whom]
- (none)

METRICS:
- [your primary metric]: [value] (target: [target])
- [secondary metric]: [value]

RISK:
- [one sentence on the biggest risk you see this week]
- (none)

NEXT:
- [top 1-3 priorities for next week]
```

## Rules

1. **DONE** — only list things fully completed, not started. Partial work goes in IN PROGRESS.
2. **BLOCKED** — be specific: "Need Growth Marketer to deliver case study copy before I can publish" beats "waiting on content."
3. **METRICS** — always include your primary success metric vs. target. Never leave this blank.
4. **RISK** — one sentence. If no risk, write "(none)". Never leave blank.
5. **NEXT** — max 3 items. If you have more, you haven't prioritized.

## Agent Primary Metrics Reference

| Agent | Primary Metric | Target |
|-------|---------------|--------|
| CEO | Paying customers | 10 by 2026-08-01 |
| CTO | Phase 18 shipped | 2026-05-01 |
| Head of Product | Backlog weeks ahead of sprint | ≥2 sprints |
| Engineer | Tasks shipped on time | 100% within agreed ETA |
| Growth Marketer | Inbound trial signups/month | ≥5 |
| Sales Rep | Demos scheduled/week | ≥1 |
| Customer Success | Trial-to-paid conversion rate | ≥30% |

## CEO's Use of These Reports

CEO reads all reports on Monday morning before their own heartbeat. CEO does NOT reply to each one individually — they synthesize into their own memo and the Friday Board Memo. If a report is missing, CEO creates a task for that agent to post it immediately.
