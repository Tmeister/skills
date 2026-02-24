---
name: vault-ideas
description: Generate ideas from vault patterns. Deep scan of notes to surface tools to build, people to reach out to, topics to investigate, and things to write. Use when you want fresh ideas grounded in your actual interests and writing.
---

# Vault Ideas — Generate Ideas from Patterns

## Routing

**Use when:**
- User says "ideas", "what should I build", "what should I write"
- Creative block, need inspiration
- Want to discover patterns in your own thinking

**Don't use when:**
- Daily planning (use vault-today)
- Specific topic connection (use vault-connect)

## Vault Location

**Default:** `~/Documents/vault-notes`

**Before running:** Check if the default path exists. If not, ask the user:
> "I couldn't find your vault at ~/Documents/vault-notes. What's the path to your Obsidian vault?"

Store the path for the session once confirmed.

Scan all areas, especially:
- `02. Area/` — ongoing interests
- `03. Resources/` — collected knowledge
- `02. Area/Daily Notes/` — recent thoughts

## Workflow

1. **Parse optional focus**

   User may provide: `/ideas [focus]` (e.g., `/ideas writing`, `/ideas tools`)

   If a focus is given, scope the scan to notes related to that domain.
   If no focus, scan broadly.

2. **Check for previous idea reports**

   Look in `03. Resources/Ideas/` for past reports. If any exist, read the most recent one to avoid resurfacing the same suggestions. Prioritize new patterns that weren't in the last report.

3. **Scan the vault**

   Don't try to read every file. Use a practical strategy:
   - **Recent daily notes** (last 30 days) — freshest thinking
   - **Most-linked notes** — find files referenced by 3+ other notes (these are hub topics)
   - **Graduated notes** — tagged `graduated` in `03. Resources/`
   - **Tagged notes** — anything with `#idea`, `#project`, `#question`, `#frustration`

   If a focus was provided, filter results to notes mentioning that domain.

   Look for:
   - Recurring themes (mentioned 3+ times)
   - Problems mentioned without solutions
   - Questions asked but not answered
   - Interests that keep appearing
   - Frustrations or pain points
   - Half-formed project ideas

4. **Cross-reference patterns**
   
   Find unexpected connections:
   - Topic A + Topic B = new angle
   - Skill + Interest = project idea
   - Problem + Knowledge = solution opportunity

5. **Generate idea report**
   
   ```markdown
   ## Ideas Report — {{date}}
   
   Based on scanning your vault, here's what's emerging:
   
   ### 🛠️ Tools to Build
   Ideas for things you could create based on problems you keep mentioning.
   
   1. **[Tool Name]**
      - Problem it solves: [from your notes]
      - Why you: [your relevant knowledge/interest]
      - Evidence: [[note1]], [[note2]]
   
   ### 👥 People to Reach Out To
   Based on interests and goals you've written about.
   
   1. **[Person/Type]**
      - Why: [connection to your interests]
      - Context: [[relevant note]]
   
   ### 🔍 Topics to Investigate
   Questions and curiosities that keep appearing.
   
   1. **[Topic]**
      - Why it matters: [from your notes]
      - Starting point: [suggested resource or angle]
   
   ### ✍️ Things to Write
   Ideas with enough material to become content.
   
   1. **[Title/Topic]**
      - Core angle: [unique perspective from your notes]
      - Supporting notes: [[note1]], [[note2]], [[note3]]
   
   ### 🔗 Unexpected Connections
   Patterns across different areas of your vault.

   1. **[Connection]**
      - [Domain A] + [Domain B] = [insight]
      - *Dig deeper with:* `/connect [Domain A] [Domain B]`
   ```

6. **Offer to save**

   Ask if the user wants this saved to the vault:
   > "Want me to save this report to your vault?"

   If yes, save to: `03. Resources/Ideas/Ideas Report — {{YYYY-MM-DD}}.md`
   Create the `Ideas/` folder if it doesn't exist.

## Example

**User:** `/ideas`

**Output:**
```markdown
## Ideas Report — Feb 24, 2026

Based on scanning your vault, here's what's emerging:

### 🛠️ Tools to Build

1. **Auth Token Debugger**
   - Problem: You've written about JWT debugging pain 6 times
   - Why you: You literally maintain JWT Auth Pro
   - Evidence: [[2026-02-20-journal]], [[Token Refresh Edge Cases]]

2. **Daily Note Templater**
   - Problem: You mentioned wanting "less friction" for daily notes
   - Why you: You already have a system, just needs automation
   - Evidence: [[2026-02-15-journal]]

### 👥 People to Reach Out To

1. **WordPress headless CMS developers**
   - Why: Your JWT plugin serves this audience, but you rarely talk to them
   - Context: [[JWT Auth Pro]] product notes mention wanting user interviews

### 🔍 Topics to Investigate

1. **Agentic workflows for personal productivity**
   - Why: You keep writing about Claude/AI assistants
   - Starting point: The Vin/Obsidian video you just watched

### ✍️ Things to Write

1. **"Token Refresh Timing: The Bug That Keeps Coming Back"**
   - Core angle: Technical deep-dive from your debugging experience
   - Supporting: 4 daily notes + graduated note on the topic

### 🔗 Unexpected Connections

1. **JWT Auth + Personal Knowledge Management**
   - Both are about "state that persists across sessions"
   - Could write about auth patterns that mirror note-taking patterns?
   - *Dig deeper with:* `/connect JWT authentication knowledge-management`
```

## Rules

- Ground every idea in actual vault content (cite notes)
- Quality over quantity — 2-3 good ideas per category max
- Include "unexpected connections" — that's the magic — and point to `/connect` for deeper dives
- Check previous idea reports to avoid resurfacing stale suggestions
- Don't suggest things the user has explicitly rejected
- Match the user's interests, not generic advice
- Respect the focus filter when provided — don't wander into unrelated domains
