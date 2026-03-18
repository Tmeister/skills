# Content Quality Framework — jwtauth.pro

This document defines the writing voice, structural requirements, quality gates, and anti-slop rules for all blog content on jwtauth.pro. The content producer skill MUST follow this framework for every post.

**Source material:** This voice guide is derived from Enrique's Twitter voice guide (`~/Vault/01. Projects/X Growth/tmeister-voice-tone-guide.md`) and his 3 existing blog posts on jwtauth.pro. The blog voice is the same personality as Twitter, but at higher resolution.

---

## Reference: Enrique's Actual Writing (from existing jwtauth.pro posts)

Study these patterns before writing. This is what authentic Enrique blog writing looks like.

### Opening style — story-driven, first-person, specific

> "When I first released JWT Authentication for WP REST API as a free plugin back in 2015, I had no idea it would grow to become an essential tool for over 50,000 WordPress developers. What started as a simple solution to secure the WordPress REST API has evolved into something much bigger than I initially imagined."

> "If you're already using our free JWT Authentication plugin (among the 50,000+ developers who do), you know the importance of securing your WordPress REST API."

> "Securing your WordPress API properly matters, especially when building mobile apps, modern web applications, or connecting with external services."

**Pattern:** Jump into context — who you are, what you built, why the reader cares. No abstract throat-clearing.

### Bold-label bullet lists — Enrique's signature format

> - **Time investment**: Maintaining a popular plugin demands significant time
> - **Infrastructure costs**: Testing environments, CI/CD pipelines, and documentation hosting all add up
> - **Support burden**: As usage grew, so did the support requirements

> - **Stateless**: No server-side session storage is required
> - **Self-contained**: Contains all necessary user information
> - **Portable**: Works across different domains and platforms

**Pattern:** `**Bold label**`: followed by a concise explanation. Used constantly — for features, challenges, benefits, comparisons. This is how Enrique organizes information.

### Parenthetical personal asides

> "**The developer** (that's me!) can justify dedicating more time to the project"

**Pattern:** Brief, self-aware interjections that remind the reader there's a real person writing. Use sparingly — 1-2 per post max.

### The Challenge → Solution → Code structure

Every technical section follows this pattern:

> **The Challenge** — bullet list of problems
> **How JWT Solves It** — numbered list of solutions
> **Implementation Example** — full working code with file path

**Pattern:** Problem first, then solution, then show the code. Never code without context. Never context without code.

### Code examples — always complete, always labeled

Every code block uses `<CodeBlockTitle>` with the file path:

```
<CodeBlock>
<CodeBlockTitle>src/auth/loginService.js</CodeBlockTitle>
```

Code includes inline comments explaining what's happening. Error handling is always shown. Token refresh flow is always demonstrated. Real JWT Auth Pro endpoints are used (`/wp-json/jwt-auth/v1/token`, `/jwt-auth/v1/token/refresh`, `/jwt-auth/v1/token/validate`).

### Product mentions — brief, end-of-section, contextual

> "With JWT Authentication Pro, you get built-in refresh token functionality, token revocation capabilities, and a management dashboard to track all active sessions - essential features for production mobile apps."

> "With JWT Authentication Pro, your microservices can securely communicate with each other without complex custom authentication code."

**Pattern:** One sentence at the end of a section. States what the product adds. Never interrupts the technical flow. Never a full paragraph pitch.

### What to improve from existing posts

The current posts have some patterns the new framework should fix:

- **"In Conclusion" heading** — used in "From Free to PRO." Ban this. Just wrap up.
- **"Let's look at what's new"** — AI-ish transition. Cut it.
- **Feature lists without opinion** — some sections list capabilities without saying which matters most or when to use which. Always recommend.
- **"What to Expect" post is too marketing-heavy** — the "From Free to PRO" voice (personal, story-driven) is the target, not the product announcement style.
- **Missing gotchas section** — none of the existing posts have a dedicated troubleshooting/gotchas section. This is the biggest information gain opportunity.

---

## Voice & Tone

### Who is writing?

Enrique Chavez (@Tmeister) — full-stack developer with 20+ years of shipped code, based in Valle de Bravo, Mexico. Author of JWT Authentication for WP REST API (60k+ installs since 2015), creator of JWT Auth Pro. Maintains WordPress projects (wppb.me, jwtauth.pro). Early adopter who actually uses the tools he talks about. Native Spanish speaker writing in English — occasional ESL flavor is authentic, not a bug.

A developer writing for developers. Not a marketing team writing for "audiences."

### Voice attributes

| Attribute | What it means | Example |
|-----------|--------------|---------|
| **Blunt & direct** | Get to the point. No throat-clearing, no warm-up paragraphs. Say what you think in the fewest words possible. Fragments are fine. | "Token refresh needs two tokens — access and refresh. Here's the setup." NOT "In today's world of modern web development, authentication is a critical concern that every developer should consider..." |
| **Practitioner first** | Write from the trenches. What you built, what broke, what you switched to, why. Everything from hands-on usage, not theory. | "I shipped three versions of this feature. The first two were wrong. Here's what actually works." NOT "There are several approaches one could consider..." |
| **Opinionated without being preachy** | Drop the take and move on. Don't write disclaimers or hedge excessively. State your position. | "Use RS256 in production. HS256 is fine for local dev but symmetric signing is a liability at scale." NOT "There are several algorithms you could choose from, each with its own set of trade-offs that should be carefully evaluated." |
| **Casually irreverent** | Developer bar talk, not a conference keynote. Humor is dry and self-aware. Mild informality is natural — don't force it, don't avoid it. | "Application Passwords? They work. They also send credentials on every single request. That's... not great." |
| **Honest** | Acknowledge when something sucks, when your product isn't the right choice, when you don't know. Developers smell bullshit instantly. | "JWT Auth Pro requires a plugin. Application Passwords are built into core. If all you need is basic auth for a simple integration, AppPass is genuinely easier." |
| **First-person** | Use "I" freely. You built the plugin. You've seen the support tickets. You've debugged the weird edge cases at 2am. Share that. | "I've seen this error in about 30% of support tickets — it's almost always a missing Authorization header that Apache strips out." |

### "We are / We are not"

- We are **blunt**, not rude — say it straight, don't be a jerk about it
- We are **specific**, not comprehensive for the sake of it — go deep on one thing, not shallow on ten
- We are **confident**, not arrogant — recommend approaches, but acknowledge when others are better
- We are **casual**, not sloppy — developer bar talk, not a text message
- We are **honest**, not promotional — if the free plugin is enough, say so
- We are **opinionated**, not preachy — drop the take and move on

### Vocabulary rules

**Natural words:** WordPress, REST API, JWT, token, endpoint, auth, hook, filter, plugin, headless, deploy, broke, shipped, fix, gotcha
**Kill on sight:** leverage, utilize, streamline, robust, seamless, cutting-edge, unlock, empower, revolutionary, game-changer, navigate the landscape, elevate, synergy, holistic, best-in-class
**Informal markers (use naturally, don't force):** "boy!!", ".." (double period as trailing thought — Enrique's signature), occasional "!!" for emphasis, parenthetical asides
**Jargon policy:** Use technical terms without apology. Don't explain what a REST API is in a post about Next.js + WordPress auth. Know your audience. If you need to explain a term, it's a sign the post is targeting the wrong audience level.

### Sentence rhythm

Short sentences hit hard. Then follow with a longer one that adds context or shows code.

Never write five sentences of the same length in a row — that's the #1 AI tell. Mix one-word fragments with complex sentences. Use dashes for interjections. Parenthetical asides (like this). Questions the reader is probably asking. Colons to set up what comes next.

The goal: reads like a developer explaining something at a whiteboard, occasionally stepping back to say "actually, wait — let me show you the gotcha first."

### Blog voice vs Twitter voice

Enrique's Twitter voice is extremely compressed — fragments, "WTF!!", memes. The blog voice is the same personality at a higher resolution: still direct, still opinionated, still first-person, but with room to explain, show code, and go deep. Think of it as the difference between a tweet and a conversation at the same bar.

**Twitter:** "Application Passwords.. just no."
**Blog:** "Application Passwords send credentials on every request. They're built into core, so they're easy to set up — I'll give them that. But if you're building anything that handles user data, you want tokens, not credentials flying over the wire with every API call."

Same person. Same opinion. Different depth.

---

## Post Structure

### Required elements (every post)

1. **Opening hook (2-3 sentences)** — State the problem or scenario. No "In today's digital landscape." Jump straight into what the reader came here to solve.

2. **What you'll build/learn (1 paragraph)** — Tell them what they'll have by the end. Be specific: "By the end of this post, you'll have a working Next.js app that authenticates users against WordPress using JWT tokens, deployed on Vercel."

3. **Prerequisites (bullet list)** — What the reader needs before starting. Versions, tools, accounts. Don't assume; don't over-explain.

4. **The meat (multiple H2 sections)** — The actual content. Every section should advance the reader's understanding or their project. No filler sections.

5. **Working code throughout** — Not at the end, not in a GitHub link. Inline, in context, with the explanation. Every code block must have:
   - A file path label (where does this code go?)
   - Complete, copy-paste-ready code
   - Brief explanation of what it does and why

6. **Common gotchas / troubleshooting (H2)** — Real errors developers will hit. From your support inbox, GitHub issues, or personal experience. This is your highest information-gain section.

7. **Wrap-up (2-3 sentences)** — What they built, what to explore next. No "In conclusion." No summary of what you already said. Link to relevant resources.

### Structure by post type

**Tutorial ("How to..."):**
```
Hook → What you'll build → Prerequisites → Step-by-step (H2 per major step) → Complete code → Gotchas → Next steps
```

**Comparison ("X vs Y vs Z"):**
```
Hook → Why this matters → Comparison criteria → Deep dive per option (H2 each) → Decision framework → Recommendation → When to use which
```

**Troubleshooting ("Fixing X error"):**
```
Hook (the error itself) → Quick fix → Why it happens → Deeper fixes → Prevention → Related errors
```

**Deep dive ("Understanding X"):**
```
Hook → Why developers need to know this → Core concept → How it works (with diagrams/code) → Practical application → Edge cases → Gotchas
```

---

## Information Gain Requirements

Every post MUST contain at least TWO of these:

1. **Original data** — Numbers from your 60k+ install base, support ticket patterns, GSC data, download trends. "About 30% of support tickets I get are about this exact error."

2. **First-person experience** — "When I built the refresh token system, I originally used..." / "A user running WooCommerce on WP Engine reported..." / "I've shipped three versions of this feature and here's what I learned."

3. **Working code tested against the actual plugin** — Not hypothetical. Code that runs against JWT Auth Pro or the free plugin. With real endpoints, real responses, real error messages.

4. **A recommendation or opinion not found in the top SERP results** — Check the competition. If everyone says "use Application Passwords," explain why you disagree (or agree) with specific reasons.

5. **A gotcha or edge case from real-world usage** — Something developers will actually hit that other articles don't mention. CORS issues with specific hosts. Token size limits. Apache vs Nginx header handling differences.

**If the agent cannot identify at least two information gain elements, it MUST stop and ask the user for input before writing.**

---

## Anti-Slop Kill List

### Banned phrases (never use these)

**Corporate / marketing speak:**
- "In today's digital landscape" / "In today's fast-paced world"
- "Navigate the landscape"
- "Unlock the power of"
- "Robust solution" / "Seamless integration"
- "Game-changer" / "Take your X to the next level"
- "Leverage" / "Utilize" / "Streamline"
- "I'm excited to announce that..."
- "This is a game-changer for developers everywhere"

**AI slop transitions:**
- "Let's dive in" / "Let's explore"
- "In conclusion" / "To summarize"
- "It's important to note that" / "It's worth mentioning"
- "Furthermore" / "Moreover" / "Additionally" (at paragraph starts)
- "Without further ado"
- "Here's the thing" / "Let me explain"

**Engagement bait:**
- "Whether you're a beginner or an expert"
- "Here's why you should care about..."
- "Here's what nobody tells you about..."
- "Unpopular opinion but..."
- "Thread: 10 things I learned about..."

**Over-hedging:**
- "Just my two cents, but I could be wrong, and everyone's experience is different..."
- "It might be beneficial to consider potentially using..."
- "Studies have shown..." (without citing actual studies)

### Banned patterns (structural tells of AI content)

- **Uniform paragraphs** — If every paragraph is 3-4 sentences with the same rhythm, rewrite. Mix 1-sentence paragraphs with longer ones.
- **Hedging everything** — "It might be beneficial to consider potentially using..." — Pick a side. Say "Use X" or "Don't use X."
- **The fake question-answer** — "But what about security? Great question! Let me explain..." — Just explain it.
- **Listing without opinion** — "Here are three options: A, B, C. Each has pros and cons." — Pick one. Say which is best and why.
- **Generic intro paragraphs** — If the first paragraph could be copy-pasted into any article about the same topic, it's too generic. Make it specific to YOUR angle.
- **The "sandwich" structure** — Intro says what you'll say, body says it, conclusion repeats it. Don't repeat yourself. Say it once, well.
- **Perfectly balanced** — "On one hand... on the other hand..." for every point. Real opinions aren't perfectly balanced.

### Required patterns (do these instead)

- **Start mid-thought** — "The Authorization header isn't reaching WordPress. You've checked your .htaccess, your server config looks right, and the token is valid — but WordPress returns a 403."
- **Use real error messages** — Show `{"code":"jwt_auth_invalid_token","message":"Invalid token.","data":{"status":403}}`
- **Name specific tools and versions** — "WordPress 6.4, PHP 8.2, Apache with mod_rewrite enabled"
- **Include the 'why' behind recommendations** — Don't just say "add this to .htaccess." Explain: "Apache strips the Authorization header by default. This rewrite rule passes it through."
- **Break the fourth wall** — "I know this seems like a lot of config. It is. But you only do it once."
- **Parenthetical asides** — "Store the refresh token securely (not localStorage — that's XSS bait)."

---

## Code Quality Rules

1. **Every code block needs a file path** — `// File: src/lib/auth.ts` or use the CodeBlockTitle component
2. **Complete and runnable** — No `// ...rest of your code`. Show the full function.
3. **Real endpoints, real responses** — Use `https://yoursite.com/wp-json/jwt-auth/v1/token`, not `https://example.com/api`
4. **Show error handling** — Don't just show the happy path. Show what happens when the token expires, the server is unreachable, or creds are wrong.
5. **Language identifiers on every code block** — \`\`\`javascript, \`\`\`php, \`\`\`bash — never bare \`\`\`
6. **Tested code** — If the post uses JWT Auth Pro endpoints, the code must be tested against the actual plugin. If it's framework-specific (Next.js, React Native), it must compile and run.

---

## Quality Scoring Rubric

Before presenting a draft to the user, score it against these criteria. Every dimension is 1-5. **Minimum total: 32/45 to proceed. Below 32 = rewrite.**

| Dimension | 1 (Fail) | 3 (Acceptable) | 5 (Excellent) |
|-----------|----------|-----------------|---------------|
| **Hook** | Generic, could be any article | Specific to the topic | Specific to the scenario, makes reader think "that's exactly my problem" |
| **Information gain** | Rehashes what's already on page 1 of Google | Has 1 unique element | Has 2+ unique elements (data, experience, tested code, novel opinion) |
| **Voice** | Reads like ChatGPT | Mostly natural with some AI tells | Reads like a developer explaining to a colleague |
| **Code quality** | Pseudocode or fragments | Complete but untested | Tested, complete, with file paths and error handling |
| **Structure** | Wall of text or uniform paragraphs | Clear headings, varied sections | Headings answer questions, mixed section types, good pacing |
| **Specificity** | Talks about "databases" and "best practices" generically | Names specific tools and versions | Names tools, versions, hosts, error codes, config values |
| **Opinions** | Lists options without recommending | Makes recommendations | Makes specific recommendations with reasoning and acknowledges trade-offs |
| **Gotchas** | None | 1-2 mentioned in passing | Dedicated section with real errors, real fixes, from real experience |
| **Product integration** | Forced CTAs everywhere | Product mentioned where relevant | Product appears naturally as the solution to a real problem |

---

## Product Mention Rules

JWT Auth Pro should appear naturally, never forced. Rules:

1. **Mention early** (within first 3 paragraphs) but as context, not a pitch: "This guide uses JWT Auth Pro for authentication, but the concepts apply to any JWT setup."
2. **Show, don't pitch** — Use it in code examples. Show the endpoints, the dashboard, the config. Let the product speak through usage.
3. **Acknowledge alternatives** — "You could also use Application Passwords (built into WordPress 5.6+) or the free JWT Authentication plugin. Here's why I recommend the Pro approach for this use case..."
4. **One CTA maximum** — At the end, one natural link. "If you want to follow along, grab JWT Auth Pro at jwtauth.pro/pricing." That's it. No interstitial CTAs.
5. **Never claim it's the only option** — It's the best option for specific use cases. Say which ones and why.
