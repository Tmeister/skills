---
name: growth-planning
description: Use when defining or revising a date-bounded growth plan for the JWT business and needing current HQ data, repo state, and strategy context before proposing a revenue target and evidence-backed initiatives.
---

# Growth Planning

## Overview

This is the shared medium-term strategy workflow for the JWT estate. `jwt-hq` remains the control center, but the skill now lives in the shared skills repo.

## When to Use

- When a new planning window needs a growth plan
- When an existing plan is stale and needs to be revised from fresh data
- When `morning-review` needs an approved strategy document to operate against

Do not use this skill to create GitHub issues, change code, or publish work. It is the strategy pass, not the execution pass.

## Required Read Order

1. `../shared/jwt-estate.json`
2. `<hq>/README.md`
3. `<hq>/AGENTS.md`
4. `<hq>/registry/local-paths.md`
5. `<hq>/registry/repos.md`
6. `<hq>/docs/business/kpis.md`
7. `<hq>/docs/business/pricing.md`
8. `<hq>/docs/playbooks/data-refresh.md`
9. `<hq>/docs/playbooks/growth-planning.md`
10. Latest Freemius summary in `<hq>/data/freemius/snapshots/`
11. Latest GA4 summary in `<hq>/data/google-analytics/snapshots/`
12. Latest monthly growth report in `<hq>/reports/monthly/`
13. Current open HQ issue state in `jwtpro/jwt-hq`
14. Lightweight recent activity in `jwt-site`, `wp-api-jwt-auth`, `jwt-auth-pro`, and `jwt-auth-docs`

Resolve `<hq>` from `../shared/jwt-estate.json`.

## Workflow

1. Define the planning window.
   - Use the requested start date and end date.
   - Name the output file `<hq>/reports/quarterly/YYYY-MM-DD-to-YYYY-MM-DD-growth-plan.md`.
2. Refresh business data if the plan depends on fresher numbers.
   - Pull the latest Freemius data.
   - Pull the latest GA4 data.
   - Rebuild the latest growth report if needed.
3. Establish the baseline.
   - Summarize current earnings, payments, subscriptions, and available retention signals.
   - Summarize current traffic, landing pages, campaign signals, and attribution visibility.
   - Summarize open HQ issue state and relevant repo activity.
4. Identify the most important findings.
   - Separate bottlenecks from opportunities.
   - Trace each finding back to current data, repo state, issue state, or a concrete business gap.
5. Propose the plan.
   - Propose one numeric earnings target for the requested window.
   - Define supporting KPIs and guardrails.
   - Derive `3-5` initiatives from evidence only.
   - Define what is not in scope for the window.
6. Write the growth plan.
   - Use `<hq>/templates/growth-planning.md`.
   - Fill the required sections completely.
7. Stop.
   - Do not create issues.
   - Do not start implementation work.

## Decision Rules

- Keep one primary business goal for the planning window.
- Treat traffic, SEO, content, pricing, and product work as candidate levers, not fixed top-level goals.
- Do not preload initiative categories.
- Every proposed initiative must cite why it matters now.
- Propose the numeric target, but do not treat it as final until the human approves it.
- Include a `Decision Questions` section when the data does not justify a single confident path.

## Helper Commands

The HQ repo already has data-refresh helpers that this skill may use. They are support tools, not the definition of the workflow.

```bash
npm run fetch:freemius
npm run normalize:freemius
npm run fetch:ga4 -- --date-range=last30days
npm run normalize:ga4
npm run report:growth -- --range=last30days
```

## Expected Outputs

- `<hq>/reports/quarterly/YYYY-MM-DD-to-YYYY-MM-DD-growth-plan.md`
- one proposed earnings target for the requested window
- supporting KPIs and guardrails
- `3-5` initiatives derived from current evidence
- a `Not In Scope` section that prevents drift
- a `Decision Questions` section for items requiring human direction

## Stop Boundary

Do not:

- create HQ issues
- create child repo issues
- change application code
- open implementation branches in product repos
- publish content
- merge pull requests
- release or deploy anything

When the plan is written, stop and wait for review.
