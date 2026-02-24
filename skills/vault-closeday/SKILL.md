---
name: vault-closeday
description: End of day capture and reflection. Takes a brain dump of what happened and structures it into a clean daily note entry. Use at end of day to log progress, capture learnings, and clear your head for tomorrow.
---

# Vault Closeday — End of Day Capture

## Routing

**Use when:**
- User says "closeday", "end of day", "wrap up", "log today"
- Evening reflection time
- User wants to capture what happened

**Don't use when:**
- Morning planning (use vault-today)
- Weekly review (use vault-graduate)

## Vault Location

**Default:** `~/Documents/vault-notes`

**Before running:** Check if the default path exists. If not, ask the user:
> "I couldn't find your vault at ~/Documents/vault-notes. What's the path to your Obsidian vault?"

Store the path for the session once confirmed.

Daily notes: `02. Area/Daily Notes/`

## Workflow

1. **Pull today's GitHub commits**

   Run `gh` to fetch today's pushed commits across the user's repos:
   ```bash
   gh api graphql -f query='
     query {
       viewer {
         contributionsCollection(from: "{{TODAY_ISO}}T00:00:00Z", to: "{{TODAY_ISO}}T23:59:59Z") {
           commitContributionsByRepository {
             repository { nameWithOwner }
             contributions(first: 50) {
               nodes { occurredAt commitCount }
             }
           }
         }
       }
     }'
   ```

   Then for each repo with commits, get the actual messages:
   ```bash
   gh api "/repos/{owner}/{repo}/commits?author={username}&since={{TODAY_ISO}}T00:00:00Z" \
     --jq '.[] | "\(.commit.message | split("\n")[0])"'
   ```

   Summarize findings as a compact list grouped by repo:
   - `repo-name`: commit message 1, commit message 2, ...

   If no commits found, note that and move on — the user may have done non-code work.

2. **Gather input**

   Present the commit summary first, then prompt:
   > "Here's what I found from your GitHub today:
   > [commit summary]
   >
   > Now tell me about the rest of your day — work stuff, personal stuff, all of it. Wins, challenges, ideas, what you learned, anything unfinished, how you're feeling. I'll organize it."

   If no commits were found, fall back to:
   > "No GitHub commits found for today. What happened? Work, personal, all of it — wins, challenges, ideas, what you learned, anything unfinished, how you're feeling. I'll organize it."

3. **Categorize the dump**
   
   Merge the commit summary with the user's brain dump. Parse into:
   - **Wins** — Things accomplished, successes
   - **Progress** — What moved forward (even if not finished)
   - **Code** — Notable commits/repos worked on (from GitHub data)
   - **Learnings** — Insights, TILs, realizations
   - **Ideas** — Random thoughts worth capturing
   - **Blockers** — What got in the way
   - **Life** — Personal highlights, health, family, hobbies, errands
   - **Tomorrow** — What carries over

4. **Generate entry**
   
   ```markdown
   ## End of Day — {{date}}
   
   ### Wins 🎯
   - [accomplishment]
   
   ### Progress 📈
   - [what moved forward]

   ### Code 💻
   - **repo-name**: [brief summary of what was committed]

   ### Learned 💡
   - [insight or TIL]
   
   ### Ideas 💭
   - [random thought worth saving]
   
   ### Blocked 🚧
   - [what got in the way, if any]

   ### Life 🏠
   - [personal highlights, health, family, hobbies, errands]

   ### Tomorrow →
   - [ ] [carry over task]
   ```

5. **Save to daily note**
   
   Append to or create: `02. Area/Daily Notes/{{YYYY-MM-DD}}-journal.md`

## Example

**User:** `/closeday`

**Agent pulls GitHub commits:**
> Here's what I found from your GitHub today:
> - **jwt-auth-pro**: "fix token refresh race condition", "update refresh endpoint tests"
> - **personal-site**: "add dark mode toggle"
>
> Now tell me about the rest of your day — work stuff, personal stuff, all of it. Wins, challenges, ideas, what you learned, anything unfinished, how you're feeling. I'll organize it.

**User:** `took way longer than expected on the auth bug. learned that the issue was with token refresh timing. had an idea for a new onboarding flow. tomorrow need to finish tests and update docs. went for a run at lunch, felt great. kid had a school play tonight. feeling tired but satisfied.`

**Output saved to daily note:**
```markdown
## End of Day — Monday, Feb 24

### Wins 🎯
- Fixed the auth token refresh race condition (finally!)

### Progress 📈
- Auth system now working correctly
- Dark mode toggle shipped on personal site

### Code 💻
- **jwt-auth-pro**: fixed token refresh race condition, updated refresh endpoint tests
- **personal-site**: added dark mode toggle

### Learned 💡
- Token refresh timing was the root cause — need to handle edge cases where refresh happens mid-request

### Ideas 💭
- New onboarding flow concept (expand this later)

### Blocked 🚧
- Auth bug took longer than expected (scope creep)

### Life 🏠
- Lunchtime run — felt great
- Kid's school play tonight

### Tomorrow →
- [ ] Finish tests for auth fix
- [ ] Update documentation
```

### Reflection
Tired but satisfied. Good deep work day despite the debugging rabbit hole.

## Rules

- Accept messy input — that's the point
- Don't over-edit the user's words, just organize them
- Always include a brief reflection/mood if mentioned
- Create the daily note file if it doesn't exist
- Keep sections even if empty (consistency helps patterns emerge)
