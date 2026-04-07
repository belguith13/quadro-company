---
schema: agentcompanies/v1
kind: project
slug: phase-18-admin
name: Phase 18 — Admin SaaS Dashboard
description: Super-admin dashboard with SaaS KPIs, org management, revenue analytics, and system health
owner: cto
targetDate: 2026-05-01
status: in_progress
metadata:
  tags:
    - engineering
    - product
    - admin
    - analytics
---

# Phase 18 — Admin SaaS Dashboard

## Goal

Give the Quadro CRM super-admin (founder) visibility into the full business — revenue, customer health, platform usage, and system status — from a single dashboard.

## Deliverables

### 1. Revenue Analytics
- MRR (Monthly Recurring Revenue) — computed from active Stripe subscriptions
- ARR (Annual Recurring Revenue) — MRR × 12
- ARPU (Average Revenue Per User/Org)
- Revenue trend chart — 12-month line chart (ApexCharts)
- Plan distribution: % of orgs on Starter vs. Team vs. Enterprise
- New MRR vs. churned MRR (waterfall chart)

### 2. Organization Management
- Table: all organizations with columns — name, plan, created date, last activity, user count, project count, status (active/trial/suspended)
- Actions: suspend org, reactivate org, change plan, view org details
- Filter/sort by: plan, status, last activity, created date

### 3. CRM Usage Metrics
Per-org aggregated stats (read from Prisma):
- Projects created (total + last 30 days)
- Quotes sent
- Orders tracked
- Installers assigned
- Active users in last 30 days

### 4. Trial & Conversion Funnel
- Trials started (last 30 days)
- Trial-to-paid conversion rate
- Average time to convert (days)
- Churned orgs (last 30 days)

### 5. System Health
- Winner Flex webhook delivery log: success rate, last 50 events table
- Google Calendar sync status per org
- Mailgun delivery rate (last 7 days)
- Fly.io uptime indicator

## Technical Spec

- New admin route: `/admin/dashboard` — protected by super-admin role
- All charts: ApexCharts (existing library) — follow existing dashboard chart patterns
- All tables: existing Radix UI + Tailwind table components
- Stripe data: query via Stripe SDK (server-side) — no new Stripe account setup needed
- All new strings: i18n keys (EN + FR)
- Shared constants: plan tier names, org status values → `app/src/shared/constants/`
- No new UI libraries

## Acceptance Criteria

- [ ] Revenue dashboard shows correct MRR/ARR from Stripe data
- [ ] Org table loads all organizations with correct metrics
- [ ] Super-admin can suspend and reactivate an org
- [ ] Webhook log shows last 50 events with status (success/fail)
- [ ] All charts render correctly on mobile (responsive)
- [ ] All text is available in EN and FR
- [ ] No hardcoded values — all constants extracted to shared/constants/
