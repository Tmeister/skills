name: seo-weekly-planning
description: Use when planning the week's JWT Auth Pro blog slate and needing the approved page inventory, current queue state, and fresh SEO signals before creating the HQ tracker issue and the child repo execution issue.
---

# SEO Weekly Content Planning

## Overview

Weekly content planning session for the JWT Auth Pro blog. It selects from the approved page inventory, gets approval, queues the chosen items, and creates the HQ tracker issue plus the canonical child-repo execution brief.

## When to Use

- Monday after the SEO data refresh (GSC + keyword research)
- When the user says "let's plan this week's content", "what should we write", or "content planning"
- When the content queue is empty

## Required Read Order

1. `../shared/jwt-estate.json`
2. `<hq>/scripts/seo/configs/editorial-scope.json`
3. `<hq>/data/seo/page-inventory.json`
4. `<hq>/data/seo/content-queue.json`
5. Latest GSC snapshot in `<hq>/data/seo/gsc/`
6. Latest keyword snapshot in `<hq>/data/seo/keywords/`
7. Latest approved growth plan in `<hq>/reports/quarterly/`
8. Existing blog posts in `<jwt-site>/content/blog/`

Resolve `<hq>` and `<jwt-site>` from `../shared/jwt-estate.json`.

## Workflow

1. **Load the inventory and current queue.**
   - Read the editorial scope contract.
   - Read the approved page inventory.
   - Read the active queue and history so you do not re-queue live or superseded work.
   - Read fresh GSC and keyword data for timing and prioritization, not for freehand topic invention.
2. **Filter eligible items.**
   - Only consider inventory items with `pageType = blog`.
   - Only consider inventory items with `status = new` or `status = refresh`.
   - Skip anything already active in the queue.
   - Prefer `productFit = high`; use `medium` only when the weekly slate needs breadth.
   - Skip any item marked `humanWriteCandidate` unless the user explicitly promotes it.
3. **Propose 2-3 topics** for the week. For each topic, present:
   - inventory item id
   - title
   - main question
   - primary intent
   - supporting keyword(s) and search signal
   - why now
   - overlap decision
   - estimated effort
4. **Get approval.**
   - Present all topics together.
   - The user approves, modifies, or replaces topics.
   - If a topic is rejected, propose a replacement.
5. **Update the queue.**
   - Write approved topics to `<hq>/data/seo/content-queue.json` with status `queued`.
   - Set the `week` field to the Monday date of the current week.
   - Assign priority order.
   - Store `inventoryItem`, `pageType`, and `primaryIntent` on each queue entry.
6. **Create issues.**
   - For each approved topic, create TWO linked issues:
     1. **jwt-hq tracking issue** using `templates/hq-content-tracker.md`
     2. **jwt-site execution issue** using `templates/jwt-site-write-post.md`
   - The jwt-site issue body is the canonical execution brief. It must include:
     - inventory item id and main question
     - parent HQ issue link
     - target keywords, primary intent, and product fit
     - rationale and overlap guardrails
     - article angle and required outline
     - internal link targets and product-link constraints
     - acceptance criteria for the MDX file and draft PR
   - Update the jwt-hq tracker issue body to include the jwt-site issue link and explicitly state that execution happens from the child issue.
   - Add all new issues to the "SEO & Content" GitHub project when that project is in use.
7. **Stop.**
   - Do not start content production from this skill.
   - The next execution step is `write-post <jwt-site-issue-number>`.

## Decision Rules

- Maximum 3 topics per week.
- Prefer items backed by first-party pain or GSC evidence.
- If GSC shows a quick win that aligns with an existing page, recommend a `refresh` item instead of a net-new page.
- Do not plan two topics that answer materially the same question in one week.
- `clusters.json` may inform keyword coverage, but it is not a valid reason to create a topic by itself.
- Do not create issues for `reject` items or `humanWriteCandidate` items unless the user explicitly says to.

## Output

- Updated `<hq>/data/seo/content-queue.json`
- jwt-hq tracking issues created for each approved topic
- jwt-site execution issues created as the canonical content briefs
- Summary of the week's content plan printed to the user

## Stop Boundary

Do not write HQ brief files, drafts, or blog content from this skill. This is the planning pass only.
