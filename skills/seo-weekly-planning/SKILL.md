---
name: seo-weekly-planning
description: Use when planning the week's JWT Auth Pro blog slate and needing fresh SEO data, queue state, and current site coverage before creating the HQ tracker issue and the child repo execution issue.
---

# SEO Weekly Content Planning

## Overview

Weekly content planning session for the JWT Auth Pro blog. Reviews fresh SEO data, proposes topics, gets approval, queues them, and creates the HQ tracker issue plus the canonical child-repo execution brief.

## When to Use

- Monday after the SEO data refresh (GSC + keyword research)
- When the user says "let's plan this week's content", "what should we write", or "content planning"
- When the content queue is empty

## Required Read Order

1. `../shared/jwt-estate.json`
2. Latest GSC snapshot in `<hq>/data/seo/gsc/`
3. Latest keyword snapshot in `<hq>/data/seo/keywords/`
4. `<hq>/data/seo/content-queue.json`
5. `<hq>/scripts/seo/configs/clusters.json`
6. Latest approved growth plan in `<hq>/reports/quarterly/`
7. Existing blog posts in `<jwt-site>/content/blog/`

Resolve `<hq>` and `<jwt-site>` from `../shared/jwt-estate.json`.

## Workflow

1. **Load data.**
   - Read the latest GSC snapshot for quick wins, declining queries, rising queries.
   - Read the latest keyword research for opportunities, trending topics, and cluster coverage.
   - Read the content queue history to know what has already been written.
   - Read the cluster config to know priorities and coverage gaps.
2. **Analyze opportunities.**
   Apply the decision framework in priority order:
   1. GSC quick wins
   2. Declining queries with existing content
   3. High-priority cluster gaps
   4. Trending topics
   5. Bottom-of-funnel problem searches
3. **Propose 2-3 topics** for the week. For each topic, present:
   - title
   - target cluster
   - primary keyword(s) and search volume
   - why now
   - information gain angle
   - estimated effort
4. **Get approval.**
   - Present all topics together.
   - The user approves, modifies, or replaces topics.
   - If a topic is rejected, propose a replacement.
5. **Update the queue.**
   - Write approved topics to `<hq>/data/seo/content-queue.json` with status `queued`.
   - Set the `week` field to the Monday date of the current week.
   - Assign priority order.
6. **Create issues.**
   - For each approved topic, create TWO linked issues:
     1. **jwt-hq tracking issue** using `templates/hq-content-tracker.md`
     2. **jwt-site execution issue** using `templates/jwt-site-write-post.md`
   - The jwt-site issue body is the canonical execution brief. It must include:
     - parent HQ issue link
     - target keywords and cluster
     - rationale and overlap guardrails
     - article angle and required outline
     - internal link targets and product-link constraints
     - acceptance criteria for the MDX file and draft PR
   - Update the jwt-hq tracker issue body to include the jwt-site issue link and explicitly state that execution happens from the child issue.
   - If the parent cluster issue does not exist yet, create it first using the HQ repo's `templates/issue-parent.md`.
   - Add all new issues to the "SEO & Content" GitHub project when that project is in use.
7. **Stop.**
   - Do not start content production from this skill.
   - The next execution step is `write-post <jwt-site-issue-number>`.

## Decision Rules

- Maximum 3 topics per week.
- At least 1 topic should come from a high-priority cluster.
- Avoid scheduling 2 topics from the same cluster in one week.
- If GSC shows a quick win that aligns with an existing post, recommend a content refresh instead of a new post.
- If no GSC data exists yet, prioritize cluster gaps and trending topics.

## Output

- Updated `<hq>/data/seo/content-queue.json`
- jwt-hq tracking issues created for each approved topic
- jwt-site execution issues created as the canonical content briefs
- Summary of the week's content plan printed to the user

## Stop Boundary

Do not write HQ brief files, drafts, or blog content from this skill. This is the planning pass only.
