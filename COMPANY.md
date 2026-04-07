---
schema: agentcompanies/v1
kind: company
slug: quadro-crm
name: Quadro CRM
description: Vertical SaaS CRM for kitchen professionals — from first contact to final installation
version: 1.0.0
license: MIT
authors:
  - name: Belguith C.
goals:
  - Reach 10 paying customers in 16 weeks (€490–990 MRR)
  - Deliver Phase 18 admin dashboard with SaaS KPIs
  - Recruit 10 early adopters in France and Belgium
  - Establish SNEC partnership for channel distribution
  - Build product-market fit in the independent kitchen business segment
includes:
  - agents/ceo/AGENTS.md
  - agents/cto/AGENTS.md
  - agents/product-manager/AGENTS.md
  - agents/engineer/AGENTS.md
  - agents/growth-marketer/AGENTS.md
  - agents/sales-rep/AGENTS.md
  - agents/customer-success/AGENTS.md
  - projects/gtm-16-week/PROJECT.md
  - projects/phase-18-admin/PROJECT.md
  - projects/early-adopter-program/PROJECT.md
  - skills/kitchen-domain/SKILL.md
  - skills/outreach/SKILL.md
  - skills/engineering/SKILL.md
requirements:
  secrets:
    - ANTHROPIC_API_KEY
    - GITHUB_TOKEN
    - LINEAR_API_KEY
    - NOTION_API_KEY
metadata:
  tags:
    - saas
    - crm
    - kitchen
    - startup
    - b2b
    - france
  brandColor: "#2563eb"
---

# Quadro CRM — Agent Company

Quadro CRM is a vertical SaaS platform built exclusively for kitchen professionals: dealers, custom manufacturers, and installation companies. It replaces the fragmented stack of Excel, email, paper notes, and disconnected tools with a single workflow covering the entire sales lifecycle — from first customer contact to quote, order, warehouse tracking, installer scheduling, and final delivery documentation.

## Mission

**Make kitchen businesses run better.** Give independent kitchen companies the same operational leverage previously reserved for enterprise players — without the enterprise price tag or complexity.

## Market Context

- France's kitchen equipment market: €3.7B (2024), >1 million kitchens/year
- 10–15% of players are independent businesses underserved by existing tools
- Primary competitors: Winner Flex (€150–500/mo, overkill), generic CRMs (no vertical workflow), Excel (no workflow at all)
- Our price: €49–€199/month — 3× cheaper than nearest specialized alternative

## Product Status

Production-deployed at https://quadro-crm-client.fly.dev/
- 17 development phases completed
- Full feature set: CRM, quoting, orders, warehouse, installer scheduling, delivery docs, i18n (EN/FR), Winner Flex integration, multi-tenant
- Phase 18 (admin SaaS dashboard) in progress

## Operating Principles

1. **Customer obsession** — every decision traces back to the kitchen business owner's daily pain
2. **Ship fast, learn faster** — bias toward deployed code over perfect plans
3. **Vertical depth over horizontal breadth** — go deeper on kitchen workflows, not wider into generic CRM
4. **Founder-led sales** — personal outreach, direct demos, hands-on onboarding until 10 customers
5. **Frugal by default** — <€2,000 acquisition budget; maximize founder leverage
