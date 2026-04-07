---
schema: agentcompanies/v1
kind: skill
slug: engineering
name: Quadro Engineering Standards
description: Coding standards, architecture patterns, and technical conventions for the Quadro CRM codebase
license: MIT
metadata:
  paperclip:
    tags:
      - engineering
      - code-quality
      - standards
---

# Quadro Engineering Standards

Technical conventions and rules that all engineering agents must follow when working on the Quadro CRM codebase.

## Codebase Location

- **Repo**: /Users/belguith/Workspace/opensaas/flex
- **App**: /Users/belguith/Workspace/opensaas/flex/app (Wasp application)
- **Blog**: /Users/belguith/Workspace/opensaas/flex/blog (Astro Starlight)
- **E2E Tests**: /Users/belguith/Workspace/opensaas/flex/e2e-tests (Playwright)
- **Deploy**: Fly.io (Amsterdam) — quadro-crm-client, quadro-crm-server

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, TypeScript, Tailwind CSS, Radix UI, react-i18next |
| Charts | ApexCharts |
| Forms | React Hook Form |
| Routing | React Router DOM |
| Backend | Wasp framework (full-stack), Node.js/Express |
| ORM | Prisma 5.19 |
| Database | PostgreSQL |
| Auth | Wasp built-in auth |
| Payments | Stripe |
| Email | Mailgun |
| Storage | AWS S3 |
| Calendar | Google Calendar API |
| Kitchen integration | Cyncly Winner Flex API |
| PDFs | PDFKit |
| Testing | Playwright (E2E) |

## Mandatory Coding Rules

### 1. No Hardcoded Values
Never hardcode enum values, magic strings, or configuration constants inline. Always extract to shared constants:
- **Location**: `app/src/shared/constants/`
- Examples: pipeline stage names, subscription tier names, org status values, role names, API endpoint paths

```typescript
// ❌ Wrong
if (project.status === 'discovery') { ... }

// ✅ Right
import { PIPELINE_STAGES } from '../shared/constants/pipeline';
if (project.status === PIPELINE_STAGES.DISCOVERY) { ... }
```

### 2. No Absolute Paths in Code
Use relative imports or Wasp path aliases. Never use `/Users/...` or `process.cwd()` style absolute paths.

### 3. Internationalization (i18n) Required
Every user-facing string (UI text, email subjects, error messages) must have i18n keys for both EN and FR:
- Frontend: `react-i18next` with `useTranslation()` hook
- Backend emails: use existing i18n email helper patterns
- New strings → add to both `en.json` and `fr.json` translation files

### 4. Minimal Changes
Only modify what the task requires. Do not refactor surrounding code, add comments to unchanged code, or "improve" unrelated functions.

### 5. Read Before Edit
Always read the full file (or relevant sections) before editing. Understand existing patterns before introducing new ones.

### 6. Prefer Edit Over Create
Prefer editing existing files over creating new ones. Do not create new utility files for one-time operations.

### 7. Security Baseline
- All DB queries: use Prisma (no raw SQL unless reviewed by CTO)
- Auth: use Wasp's auth system — do not bypass or duplicate
- No secrets in code — all via environment variables
- Sanitize user input before rendering (no XSS)
- No SQL injection (Prisma parameterizes by default)

### 8. Prisma Migrations
- Never apply destructive migrations without CTO review
- Test migrations on local DB before production
- Keep schema changes backward-compatible where possible

## Architecture Patterns

### File Structure (Wasp conventions)
```
app/
├── src/
│   ├── shared/
│   │   └── constants/        # ALL shared constants live here
│   ├── client/               # React components and pages
│   │   ├── components/       # Reusable UI components
│   │   └── pages/            # Route-level pages
│   └── server/               # Server actions, queries, jobs
│       ├── actions/          # Wasp actions (mutations)
│       └── queries/          # Wasp queries (reads)
├── schema.prisma             # Database schema
└── main.wasp                 # Wasp configuration
```

### UI Component Patterns
- Use existing Radix UI + Tailwind component patterns from the codebase
- Do not import new UI libraries without CTO approval
- Follow Tailwind class conventions already established in the project

### API Integration Quirks

**Winner Flex API**:
- Requests: PascalCase field names
- Responses: camelCase field names
- `contactGuid` is embedded in `projectAddresses[0]`, not at the project root level
- Known quirk: filter parameters must be double-checked against API docs

**Search UX Pattern**:
- Decouple input field value (local React state) from the actual search query (API trigger)
- Fire search on Enter keypress only — do NOT fire on every keystroke (causes focus loss bugs)

**PDF Generation (PDFKit)**:
- Follow existing quote PDF patterns (`app/src/server/pdf/`)
- Do not use a different PDF library — PDFKit is established and working

## Testing

- Write Playwright E2E tests for any new user-facing workflow
- Test location: `e2e-tests/`
- Run tests locally before opening PR: `npm run test:e2e`
- Tests must pass before CTO review

## Deployment

- **CI/CD**: GitHub Actions (auto-deploy on main branch merge)
- **Staging**: Test on Fly.io staging environment before production push
- **Production**: Deploy only after CTO approval for non-trivial changes
- **Environment vars**: Managed via Fly.io secrets — never in code or `.env` committed to git

## PR Review Checklist

Before requesting CTO review, verify:
- [ ] No hardcoded values (constants in shared/constants/)
- [ ] All user-facing strings have i18n keys (EN + FR)
- [ ] No absolute paths
- [ ] Security: no SQL injection, no XSS, no exposed secrets
- [ ] Minimal change — only what was required
- [ ] Playwright test written for new workflow (if applicable)
- [ ] Prisma migration reviewed (if schema changed)
- [ ] PR description explains: what changed, why, how to test
