Parent: jwtpro/jwt-hq#{hq_issue}

# Write: {title}

## Targeting

- Cluster: {cluster_name} (`{cluster_id}`)
- Primary keyword: {primary_keyword}
- Secondary keywords: {secondary_keywords}
- Search signal: {search_signal}

## Why This Post Exists

{rationale}

## Overlap Guardrails

- Do not turn this into a tutorial or setup walkthrough.
- Do not duplicate existing published coverage such as `{overlap_posts}`.
- Keep the article in the decision-stage lane unless the brief explicitly says otherwise.

## Article Angle

{angle}

## Required Outline

{outline}

## Internal Links

- Blog posts: {blog_links}
- Product pages: {product_links}

## Product-Link Constraints

- Keep product mentions natural.
- Use one CTA at most, near the end.
- Do not force pricing or upgrade links into sections where they do not help the reader.

## Acceptance Criteria

- Write the post directly in `content/blog/{slug}.mdx`
- Use `author: "tmeister"` and valid categories from `content/blog/categories.json`
- Open a draft PR in `jwt-site` that links both this issue and `jwtpro/jwt-hq#{hq_issue}`
- Update `jwt-hq` tracking and the content queue when the draft PR opens
