---
name: morning-review
description: Use when starting the daily JWT HQ planning pass and needing fresh business data, issue movement, repo activity, and content-pipeline state before deciding what is ready for execution.
---

# Morning Review

## Overview

This is the shared daily HQ operator workflow for `jwt-hq`. It defines what the agent must review, how it decides what matters, what it writes, and where it stops. Helper scripts may assist with the mechanical parts, but the workflow lives here.

## When to Use

- At the start of the day in `jwt-hq`
- When yesterday's priorities need to be re-evaluated against fresh Freemius and GA4 data
- When HQ and child issue coordination needs to be updated before code or content work starts

Do not use this skill to implement repo changes. It is the planning pass, not the execution pass.

## Required Read Order

1. `../shared/jwt-estate.json`
2. `<hq>/README.md`
3. `<hq>/AGENTS.md`
4. `<hq>/registry/local-paths.md`
5. `<hq>/registry/repos.md`
6. `<hq>/docs/playbooks/issue-linking.md`
7. `<hq>/docs/playbooks/data-refresh.md`
8. `<hq>/docs/playbooks/morning-review.md`
9. `<hq>/scripts/seo/configs/editorial-scope.json`
10. `<hq>/data/seo/page-inventory.json`
11. Latest approved growth plan in `<hq>/reports/quarterly/` if one exists
12. Yesterday's daily brief if it exists
13. The active parent issue in `jwtpro/jwt-hq` when the run is anchored to a current initiative

Resolve `<hq>` from `../shared/jwt-estate.json`.

## Workflow

1. Refresh current business data.
   - Pull the latest Freemius incremental data.
   - Pull the latest GA4 last-30-days data.
   - Rebuild the current growth report.
2. Review current coordination state.
   - Read the latest approved growth plan when one exists.
   - Check what changed since yesterday in HQ issues.
   - Review lightweight recent activity in `jwt-site`, `wp-api-jwt-auth`, `jwt-auth-pro`, and `jwt-auth-docs`.
3. Check content pipeline status.
   - Read `<hq>/data/seo/page-inventory.json`.
   - Read `<hq>/data/seo/content-queue.json`.
   - Report how many inventory items are `existing`, `refresh`, `new`, and `reject`.
   - Flag the inventory as stale when it has not been refreshed for the current planning window.
   - Confirm queued topics still map to approved inventory items.
   - Count topics remaining this week with status not yet `published` or `superseded`.
   - Identify the next actionable topic by priority only when it maps to an approved inventory item, using the site issue as the execution contract.
   - Count how many topics were published this week vs the target of 3.
   - If the latest GSC data shows a quick win or declining query that relates to a queued or draft-PR topic, note it.
4. Analyze what changed.
   - Identify material movement in traffic, revenue, subscriptions, conversion-related signals, and project state.
   - Separate opportunities from risks.
   - Decide whether an existing HQ issue should be updated or whether a new one is warranted.
5. Update the action graph.
   - Create or update parent HQ issues conservatively.
   - Create child repo issues only when implementation scope is already clear.
   - Every child issue must link back to one parent HQ issue.
6. Write the daily brief.
   - Save it to `<hq>/reports/daily/YYYY-MM-DD-morning-review.md`.
   - Include `Summary`, `Data Changes`, `HQ Movement`, `Repo Activity`, `Opportunities`, `Risks`, `Ready For Execution Today`, `Content Pipeline`, and `Issue Actions Taken`.
7. Stop.
   - Do not start implementation work from this skill.

## Decision Rules

- Be conservative about new issues.
- Update an existing HQ issue when it still represents the same initiative, risk, or opportunity.
- Create a new HQ issue only when no materially similar open issue exists.
- Select up to five `ready for execution today` items.
- Prefer fewer than five when work is large.
- Child issues belong in repo-specific repos only when the scope is execution-ready.

## Helper Commands

The HQ repo includes helper commands for the mechanical parts of the workflow. They are tools the skill may use, not the definition of the skill.

- Full helper run:

```bash
npm run morning-review
```

- Safe rehearsal when changing the workflow or validating credentials:

```bash
npm run morning-review -- --dry-run
```

- Manual fallback if the helper needs to be bypassed:

```bash
npm run fetch:freemius
npm run normalize:freemius
npm run fetch:ga4 -- --date-range=last30days
npm run normalize:ga4
npm run report:growth -- --range=last30days
```

Then perform the issue review and brief-writing steps directly.

## Expected Outputs

- refreshed Freemius and GA4 snapshots
- refreshed growth report
- `<hq>/reports/daily/YYYY-MM-DD-morning-review.md`
- conservative updates to parent HQ issues
- linked child repo issues only when implementation scope is already clear
- up to five items marked `ready for execution today`
- `Content Pipeline` section in the daily brief showing: queue status, next content task, published count vs target, and any GSC signals relevant to queued or draft-PR content
- `Content Pipeline` section in the daily brief showing: inventory health, queue status, next valid content task, published count vs target, and any GSC signals relevant to queued or draft-PR content
- priorities that align with the latest approved growth plan when one exists

## Stop Boundary

Do not:

- change application code
- open implementation branches
- publish content
- merge pull requests
- deploy or release anything

When the brief and issue actions are complete, stop and let the user choose what to execute next.
