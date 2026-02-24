---
name: vault-connect
description: Bridge two topics using your vault's link graph. Finds unexpected connections between seemingly unrelated ideas by tracing paths through your notes. Use when stuck or when you suspect two ideas are related but can't see how.
---

# Vault Connect — Bridge Two Topics

## Routing

**Use when:**
- User says "connect X and Y", "how are X and Y related"
- User is stuck and needs a new angle
- Brainstorming session needs cross-pollination

**Don't use when:**
- General idea generation (use vault-ideas)
- Tracing single idea evolution (that's /trace, not implemented yet)

## Vault Location

**Default:** `~/Documents/vault-notes`

**Before running:** Check if the default path exists. If not, ask the user:
> "I couldn't find your vault at ~/Documents/vault-notes. What's the path to your Obsidian vault?"

Store the path for the session once confirmed.

## Workflow

1. **Parse the two topics**
   
   User provides: `/connect [Topic A] [Topic B]`
   
   If not provided, ask:
   > "What two topics do you want to connect? Give me two ideas, domains, or concepts."

2. **Search the vault for each topic**

   For each topic, find:
   - Notes explicitly about that topic (filename or heading match)
   - Notes that mention it (grep for the term in note bodies)
   - Tags related to the topic (grep for `#tag` variations)

3. **Follow the link graph (max 2 hops)**

   From each note found in step 2, extract outgoing wikilinks:
   ```bash
   grep -oP '\[\[([^\]|]+)' note.md | sed 's/\[\[//'
   ```
   Resolve each link to a file in the vault (match by filename, case-insensitive).
   Read those linked notes and extract their wikilinks too (hop 2).

   **Stop at 2 hops.** Do not follow links beyond that — the vault can be large and deeper traversal rarely yields useful connections.

4. **Trace connection paths**

   Using the notes and links gathered above, look for:
   - Direct links: Note A links to Note B
   - One-hop: Note A → Note C → Note B
   - Two-hop: Note A → C → D → Note B
   - Shared tags or themes
   - Similar language or concepts across notes in both clusters

5. **Analyze the bridges**
   
   For each connection path found:
   - What's the bridging concept?
   - Why might this connection matter?
   - What new angle does it suggest?

6. **Generate connection report**
   
   ```markdown
   ## Connecting: [Topic A] ↔ [Topic B]
   
   ### Direct Connections
   [If any notes directly link both topics]
   
   ### Bridge Paths
   
   **Path 1:** A → [Bridge] → B
   - [Topic A] relates to [Bridge] because: [reason from notes]
   - [Bridge] relates to [Topic B] because: [reason from notes]
   - **Insight:** [What this suggests]
   
   **Path 2:** A → [Bridge1] → [Bridge2] → B
   ...
   
   ### Shared Themes
   - Both topics touch on: [theme]
   - Both appear in context of: [situation]
   
   ### Synthesis
   [2-3 sentences on what connecting these topics reveals]
   
   ### Possible Actions
   - [ ] [Specific thing to explore based on connection]
   - [ ] [Another action]
   
   ### Notes Referenced
   - [[Note 1]]
   - [[Note 2]]
   ```

7. **Offer to save**

   Ask if the user wants to save the connection report to the vault:
   > "Want me to save this to your vault?"

   If yes, save to: `03. Resources/Connections/{{Topic A}} ↔ {{Topic B}}.md`
   Create the `Connections/` folder if it doesn't exist.

## Example

**User:** `/connect filmmaking authentication`

**Output:**
```markdown
## Connecting: Filmmaking ↔ Authentication

### Direct Connections
None found (these seem unrelated at first glance)

### Bridge Paths

**Path 1:** Filmmaking → Storytelling → User Onboarding → Authentication
- Your filmmaking notes emphasize "showing not telling"
- Your onboarding notes cite this principle for UX
- Authentication is the first UX touchpoint
- **Insight:** Auth flows could use narrative structure — setup, tension (verification), resolution (access granted)

**Path 2:** Filmmaking → World Building → Mental Models → JWT Tokens
- You wrote about how films establish "rules of the world"
- Your JWT notes mention users not understanding token expiry
- **Insight:** What if auth errors explained the "rules" like a film establishes its world?

### Shared Themes
- Both involve **trust-building** (audience trust vs user trust)
- Both require **invisible complexity** (editing vs encryption)

### Synthesis
Your filmmaking knowledge about narrative structure and invisible craft could inform how you design auth UX. The "show don't tell" principle specifically applies to error messages and token expiry.

### Possible Actions
- [ ] Redesign auth error messages using storytelling principles
- [ ] Write blog post: "What Filmmaking Taught Me About Auth UX"

### Notes Referenced
- [[Filmmaking Notes]]
- [[Storytelling Principles]]  
- [[JWT Auth Pro]]
- [[Onboarding Flow Redesign]]
```

## Rules

- Try hard to find connections — that's the challenge — but don't fabricate them
- Go beyond obvious connections — dig for insight
- Cite specific notes as evidence (no connection claim without a source note)
- End with actionable suggestions
- If no connection exists in the vault, say so honestly and suggest it as a new connection worth creating
