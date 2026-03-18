---
name: write-post
description: Use when a JWT site content issue is ready for execution and you need to draft or finalize the post directly in jwt-site, keep the same draft PR moving, and sync HQ tracking.
---

# Write Blog Post

Produce a blog post for jwtauth.pro from a `jwt-site` issue. The issue body is the canonical brief. This skill runs from any directory, writes the MDX directly in `jwt-site`, opens or updates the draft PR, and keeps `jwt-hq` tracking in sync.

## Required Read Order

1. `../shared/jwt-estate.json`
2. The target `jwt-site` issue
3. The linked `jwt-hq` tracking issue
4. `skills/write-post/voice-and-quality.md`
5. `<hq>/data/seo/content-queue.json`
6. `<hq>/scripts/seo/configs/clusters.json`
7. Existing blog posts in `<jwt-site>/content/blog/`
8. `<jwt-site>/content/blog/authors.json`
9. `<jwt-site>/content/blog/categories.json`

Resolve `<hq>` and `<jwt-site>` from `../shared/jwt-estate.json`.

## Workflow

### Phase 0: Setup and Verification

1. **Parse the issue number** from the command argument. If not provided, ask for it.
2. **Read and verify the jwt-site issue.**
   - It must be open.
   - It must have a title starting with `Write:`.
   - It must contain a `Parent:` reference to a jwt-hq issue.
   - It must contain the execution brief sections needed to draft the post.
3. **Read and verify the jwt-hq tracking issue.**
   - It must be open.
   - It must have a title starting with `[Content]`.
   - It must reference the same topic and child repo issue.
4. **Read the voice guide** at `skills/write-post/voice-and-quality.md`.
5. **Inspect existing execution state.**
   - Check whether a queue entry already exists in `<hq>/data/seo/content-queue.json`.
   - Check whether a draft PR already exists for the issue.
   - Reuse the existing branch and PR when they already exist.
6. **Create or resume the branch in jwt-site.**
   - Create the branch from `main`.
   - In Codex sessions use `codex/<site-issue>-<slug>`.
   - If a draft PR already exists, checkout its head branch instead of creating a new one.

### Phase 1: Draft the Post

1. Use the `jwt-site` issue body as the canonical brief. Do not generate or depend on HQ brief files.
2. Determine post type from the issue brief and follow the relevant structure from the voice guide.
3. Write the MDX file directly in `<jwt-site>/content/blog/<slug>.mdx`.
4. Use frontmatter with:
   - `author: "tmeister"`
   - valid categories from `content/blog/categories.json`
   - `publishedAt: "YYYY-MM-DD"`
5. Apply the voice guide quality rules.
6. Score the draft against the voice guide rubric. Minimum 32/45 before review.
7. Preview locally with `npm run dev` when needed. Draft review happens in the `jwt-site` draft PR, not in HQ markdown files.

### Phase 2: Open or Update the Draft PR

1. Commit and push the branch.
2. Create a draft PR if one does not exist yet. The PR body must include:
   - the target keywords
   - the cluster
   - `Closes #<jwt-site-issue-number>`
   - `Tracking: jwtpro/jwt-hq#<hq-issue-number>`
3. If a draft PR already exists, push additional commits to the same branch.
4. When the draft PR opens:
   - comment on the HQ tracking issue with the PR link
   - update the queue status in `<hq>/data/seo/content-queue.json` to `draft-pr`
   - do not move the topic to history yet

### Phase 3: Review Loop

1. User reviews the post via the draft PR or a local preview.
2. If changes are needed, update the same MDX file on the same branch and keep the PR open.
3. Repeat until the user says the draft is ready to merge.

### Phase 4: Finalize After Merge

1. When the PR is merged, update the queue entry in `<hq>/data/seo/content-queue.json`:
   - set status to `published`
   - add `prNumber`, `publishedAt`, and `slug`
   - move the topic from `topics` to `history`
2. Comment on the HQ tracking issue with the merged PR link and close the HQ issue.
3. Report the merged PR URL and published slug to the user.

## Stop Boundary

Do not:
- merge the PR
- deploy the site
- modify jwt-site code beyond the single blog MDX file
- create HQ brief files
