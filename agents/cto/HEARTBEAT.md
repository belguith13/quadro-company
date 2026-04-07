# HEARTBEAT.md — CTO

Run this checklist on every heartbeat (scheduled: Monday 9am CET, after CEO).

## 1. Check Production Health
- Review Fly.io deployment status for quadro-crm-client and quadro-crm-server
- Check recent GitHub Actions runs — any failed deployments?
- Review error logs for critical failures
- Check Stripe webhook delivery success rate

## 2. Review Engineering Backlog
- What tasks are assigned to Engineer? Are they blocked?
- What's the status of Phase 18 (admin SaaS dashboard)?
- Any PRs awaiting review?

## 3. Code Review Priority
- Prioritize PRs from Engineer — unblock within 24h
- Check for: no hardcoded values, constants in shared/, no absolute paths, no security issues

## 4. Triage New Technical Issues
- Any bugs reported by Customer Success? Assess severity and fix timeline.
- Any Winner Flex API issues? (Known quirk: PascalCase in, camelCase out; projectAddresses[0] for contactGuid)

## 5. Integration Health
- Winner Flex webhook sync: any failures in logs?
- Google Calendar sync: any auth token expiry issues?
- Mailgun: any bounced emails or delivery failures?

## 6. Weekly Report to CEO
Write brief status:
- What shipped this week (with feature name + impact)
- What's in progress (with ETA)
- Any blockers or risks
- Any production incidents
