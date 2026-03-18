---
name: seo-discovery
description: Use when jwtauth.pro needs fresh content discovery and you need to turn first-party pain, GSC signals, keyword research, and current site coverage into an approved inventory of canonical page ideas before weekly planning.
---

# SEO Discovery

## Overview

This workflow maintains the JWT editorial inventory. It discovers candidate pages, collapses duplicates into canonical page ideas, classifies each idea, and updates the source-of-truth inventory in `jwt-hq`.

This skill does discovery only. It does not create issues or queue work for the week.

## Required Read Order

1. `../shared/jwt-estate.json`
2. `<hq>/scripts/seo/configs/editorial-scope.json`
3. `<hq>/data/seo/page-inventory.json`
4. Latest GSC snapshot in `<hq>/data/seo/gsc/`
5. Latest keyword snapshot in `<hq>/data/seo/keywords/`
6. `<hq>/data/seo/content-queue.json`
7. Existing posts in `<jwt-site>/content/blog/`
8. First-party pain sources that are available locally: support issues, GitHub issues, docs gaps, or recurring operator notes

Resolve `<hq>` and `<jwt-site>` from `../shared/jwt-estate.json`.

## Workflow

1. **Load the editorial contract.**
   - Read `editorial-scope.json` before looking at candidate topics.
   - Treat product fit as the primary gate.
   - Treat tutorials as excluded by default unless they should be marked `humanWriteCandidate`.
2. **Collect evidence.**
   - Pull first-party pain from support/issues/docs-gap signals.
   - Pull GSC queries and action items.
   - Pull keyword demand and competitor-style opportunities from the latest keyword snapshot.
   - Read existing site coverage and the current content queue.
3. **Normalize candidates into canonical page ideas.**
   - One inventory item equals one page.
   - If the same page could satisfy multiple keywords, merge them into one item.
   - Do not create one item per keyword variation.
4. **Classify each item.**
   - `pageType`: `blog`, `product-page`, or `reject`
   - `status`: `existing`, `refresh`, `new`, or `reject`
   - `primaryIntent`: `decision`, `troubleshooting`, `deep-dive`, `security-ops`, or `product`
   - `productFit`: `high`, `medium`, or `low`
   - `humanWriteCandidate: true` when the best answer is a tutorial or full build-out that should not be auto-queued
5. **Run the duplication gate.**
   - What exact question does this page answer?
   - Which existing page already answers most of it?
   - Is this a refresh instead of a new page?
   - If the overlap is too high, mark the item `reject`.
6. **Update the inventory.**
   - Write the resulting items to `<hq>/data/seo/page-inventory.json`.
   - Keep notes concise but explicit about why an item is `new`, `refresh`, or `reject`.
7. **Stop.**
   - Present the inventory changes to the user.
   - The next downstream step is `seo-weekly-planning`, which selects from approved inventory items only.

## Decision Rules

- First-party pain outranks GSC demand.
- GSC demand outranks tool or competitor demand.
- Evergreen beats timely by default.
- Timely topics are allowed only when they have unusually strong developer relevance or commercial pull.
- Docs are out of scope for discovery on `jwtauth.pro`.
- `clusters.json` is legacy research input only. It may inform keyword coverage, but it must not generate topics by itself.
- A `blog` item must solve a distinct developer problem. If it does not, reject it.
- A tutorial-shaped opportunity should usually become `reject` plus `humanWriteCandidate: true`, not a queued blog task.

## Output

- Updated `<hq>/data/seo/page-inventory.json`
- Clear classifications for `existing`, `refresh`, `new`, and `reject`
- Notes showing overlap decisions and why each item survives or is rejected

## Stop Boundary

Do not:

- create HQ or child repo issues
- update the weekly queue directly
- start drafting content
- create docs pages
