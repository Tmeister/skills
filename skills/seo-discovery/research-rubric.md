# SEO Discovery Rubric

Use this rubric when deciding whether a candidate deserves a slot in `page-inventory.json`.

## Distinct Problem Check

- What exact developer problem or question does this page answer?
- Would one page satisfy all of the supporting keywords?
- If yes, merge them into one canonical page idea.

## Page Type Check

- Is this best solved as a `blog` post?
- Is the query clearly commercial enough that it should be a `product-page` instead?
- If neither is true, mark it `reject`.

## Product Fit Check

- Would JWT Auth Pro fit naturally in the recommendation, architecture, or troubleshooting path?
- If product fit is weak and indirect, downgrade or reject the item.

## Status Check

- `existing`: the page already exists and still fits the topic
- `refresh`: the page exists but needs substantial updating, repositioning, or consolidation
- `new`: the site does not yet have a page that answers the question well
- `reject`: too weak, too overlapping, too tutorial-heavy, or wrong for the site

## Evidence Check

- First-party pain: support tickets, GitHub issues, docs gaps, or repeated operator pain
- GSC demand: queries, declines, or clear action items
- Tool demand: keyword research or competitor gap signals
- Existing coverage: what the current site already says

## Tutorial Gate

- If the best version of this topic is a full how-to or framework build, do not auto-queue it.
- Mark `humanWriteCandidate: true` and keep it out of weekly planning unless the user explicitly promotes it.

## Duplication Gate

- Which published page already answers most of this?
- Which queued page would overlap too heavily with it?
- Is this genuinely new, or are you just renaming the same idea?
