---
name: vault-today
description: Morning planning from Obsidian vault. Pulls recent daily notes, priorities, and calendar context into a focused plan for the day. Use when starting your day or when feeling overwhelmed and need clarity.
---

# Vault Today — Morning Planning

## Routing

**Use when:**
- User says "today", "morning plan", "what should I focus on"
- Start of day planning session
- User feels overwhelmed and needs clarity

**Don't use when:**
- End of day (use vault-closeday)
- Looking for specific ideas (use vault-ideas)

## Vault Location

**Default:** `~/Documents/vault-notes`

**Before running:** Check if the default path exists. If not, ask the user:
> "I couldn't find your vault at ~/Documents/vault-notes. What's the path to your Obsidian vault?"

Store the path for the session once confirmed.

Daily notes: `02. Area/Daily Notes/`

## Workflow

1. **Read last closeday entry**

   Find the most recent daily note with an "End of Day" section. On Mondays (or after a gap), this may be Friday's or older — look back up to 4 days.

   Extract:
   - **Tomorrow →** section — these are explicit carry-overs the user already committed to
   - **Blocked 🚧** section — unresolved blockers that may still apply
   - **Reflection** — energy/mood context from last session

2. **Read recent context**
   - Last 7 days of daily notes (beyond the closeday entry already read)
   - Any files tagged with `#priority` or `#focus`
   - Check for incomplete tasks (`- [ ]`) from recent days that weren't already in the closeday Tomorrow section

3. **Identify priorities**

   Start with the Tomorrow carry-overs from the last closeday — these are the user's own stated intentions. Then layer in:
   - New items from tagged/priority notes
   - Incomplete tasks from other daily notes
   - Any deadlines mentioned recently

4. **Generate today's plan**
   
   Output format:
   ```markdown
   ## Today's Focus — {{date}}
   
   ### Top 3 Priorities
   1. [Most important thing based on vault context]
   2. [Second priority]
   3. [Third priority]
   
   ### Carrying Over
   - [ ] [Incomplete task from previous days]
   
   ### Context
   [Brief summary of relevant recent notes/themes]
   
   ### Time Blocks (suggested)
   - Morning: [deep work suggestion]
   - Afternoon: [lighter work suggestion]
   ```

5. **Offer to save**

   Ask if the user wants this added to today's daily note:
   > "Want me to save this to today's journal?"

   If yes, prepend to or create: `02. Area/Daily Notes/{{YYYY-MM-DD}}-journal.md`

## Example

**User:** `/today`

**Output:**
```markdown
## Today's Focus — Monday, Feb 24

### Top 3 Priorities
1. Finish JWT Auth Pro dashboard refactor (mentioned 3x this week)
2. Review PR from contributor (tagged urgent yesterday)
3. Write newsletter draft (deadline tomorrow)

### Carrying Over
- [ ] Update documentation for v2.0
- [ ] Reply to support ticket #142

### Context
You've been deep in the JWT Auth codebase. Yesterday you noted feeling "close to done" on the refactor. Energy seems good based on recent journal entries.

### Time Blocks
- Morning: JWT refactor (your best focus hours)
- Afternoon: Newsletter + PR review (lighter cognitive load)
```

## Rules

- Keep it actionable, not overwhelming
- Max 3 priorities (force focus)
- Start from the last closeday's Tomorrow section — honor the user's own stated intentions
- On Mondays or after gaps, look back up to 4 days for the last closeday entry
- Reference specific notes when relevant
- Match the user's voice/energy from recent entries
