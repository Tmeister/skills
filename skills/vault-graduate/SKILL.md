---
name: vault-graduate
description: Promote half-formed ideas from daily notes into standalone notes. Scans recent daily notes for ideas worth expanding and creates proper note files for them. Use weekly to turn scattered thoughts into real knowledge.
---

# Vault Graduate — Promote Ideas to Notes

## Routing

**Use when:**
- User says "graduate", "promote notes", "extract ideas", "weekly review"
- Weekly review time
- Daily notes are full of half-formed thoughts

**Don't use when:**
- Daily capture (use vault-closeday)
- Looking for patterns (use vault-ideas)

## Vault Location

**Default:** `~/Documents/vault-notes`

**Before running:** Check if the default path exists. If not, ask the user:
> "I couldn't find your vault at ~/Documents/vault-notes. What's the path to your Obsidian vault?"

Store the path for the session once confirmed.

Daily notes: `02. Area/Daily Notes/`
Output: `03. Resources/` or appropriate area folder

## Workflow

1. **Scan recent daily notes**

   Read last 14 days of daily notes. Scan all sections — including Code, Life, Wins, Learned, Ideas, etc. Look for:
   - Ideas mentioned multiple times across different days
   - Concepts that deserve expansion
   - Half-formed thoughts with potential
   - Anything tagged with `#important`, `#idea`, `#explore`, or marked with `!!` or similar emphasis
   - Recurring personal themes (e.g., a hobby or habit appearing in Life sections repeatedly)

2. **Check for existing notes**

   Before proposing candidates, check if a standalone note already exists for each idea:
   - Search `03. Resources/` and `02. Area/` for files with matching names or aliases
   - If a graduated note already exists, skip it — don't re-propose
   - If an existing note exists but the daily notes add significant new material, flag it as "update candidate" instead

3. **Identify graduation candidates**
   
   Present findings:
   ```markdown
   ## Ideas Ready to Graduate
   
   ### 1. [Idea Name]
   - **Appeared in:** 3 daily notes (Feb 10, 12, 18)
   - **Core claim:** [one sentence summary]
   - **Why it matters:** [brief context]
   
   ### 2. [Idea Name]
   ...
   ```

4. **Ask for selection**
   
   > "Which of these should I turn into standalone notes? (all / numbers / none)"

5. **Create graduated notes**
   
   For each selected idea, create a note:
   
   ```markdown
   ---
   id: {{slug}}
   aliases:
     - [Idea Name]
   tags: [idea, graduated]
   created: {{YYYY-MM-DD}}
   source: daily-notes
   ---
   
   # [Idea Name]
   
   ## Core Claim
   [One clear sentence stating the idea]
   
   ## Context
   [Where this came from, why it matters]
   
   ## Evidence / Examples
   - [Supporting point from daily notes]
   - [Another supporting point]
   
   ## Connections
   - [[Related Note 1]]
   - [[Related Note 2]]
   
   ## Open Questions
   - [What's still unclear?]
   
   ## Source Notes
   - [[{{date1}}-journal]]
   - [[{{date2}}-journal]]
   ```

6. **Insert backlinks in source daily notes**

   For each graduated note, go back to the source daily notes and add a wikilink where the idea was originally mentioned. For example, if a daily note says:
   > Token refresh keeps causing issues

   Append or inline a link:
   > Token refresh keeps causing issues → [[Token Refresh Edge Cases]]

   This strengthens the vault graph and makes it easy to navigate from daily notes to graduated notes.

7. **Report what was created**

   List the new files with paths and which daily notes were updated with backlinks.

## Example

**User:** `/graduate`

**Agent scans 14 days of daily notes...**

**Output:**
```markdown
## Ideas Ready to Graduate

### 1. Token Refresh Edge Cases
- **Appeared in:** 4 daily notes (Feb 10, 15, 20, 24)
- **Core claim:** Token refresh during active requests causes auth failures
- **Why it matters:** Keep hitting this bug, need documented solution

### 2. Onboarding Flow Redesign  
- **Appeared in:** 2 daily notes (Feb 22, 24)
- **Core claim:** Current onboarding is too technical for non-dev users
- **Why it matters:** Support tickets mention confusion

### 3. Weekly Review Habit
- **Appeared in:** 3 daily notes (Feb 12, 18, 23)
- **Core claim:** Need consistent weekly review to process notes
- **Why it matters:** Meta — helps the whole system work
```

> Which of these should I turn into standalone notes? (all / 1,2 / none)

**User:** `1,2`

**Creates:**
- `03. Resources/Token Refresh Edge Cases.md`
- `03. Resources/Onboarding Flow Redesign.md`

## Rules

- Only graduate ideas that appear 2+ times OR are tagged `#important` / `#idea` / `#explore` / marked with `!!`
- Never re-graduate an idea that already has a standalone note — flag as update candidate instead
- Scan all daily note sections (Code, Life, Wins, Learned, Ideas, etc.)
- Preserve links back to source daily notes
- Insert backlinks in source daily notes pointing to the new graduated note
- Don't over-polish — keep the user's original framing
- Ask before creating (don't auto-generate)
- Include "Open Questions" to prompt future thinking
