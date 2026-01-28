# Skills Hub

These are my personal skills used in my projects and day-to-day work. They are public as references, and I may change, delete, or add to them as my needs evolve.

Portable agent skills for multiple coding assistants. Each skill follows the SKILL.md standard so it can be used across Claude Code, OpenCode, Codex, and Amp.

## What is a skill?

Skills are markdown files that describe a repeatable workflow. Agents can auto-apply them or you can call them directly with `/skill-name`.

## Available skills

| Skill | Description |
| --- | --- |
| [bug-issue](skills/bug-issue/) | Diagnose and fix a GitHub issue with a reproduction-first workflow. |
| [commit](skills/commit/) | Generate a conventional commit message from staged changes and commit safely. |
| [draft-issue](skills/draft-issue/) | Research and draft a high quality GitHub issue before creating it. |
| [empower-sync](skills/empower-sync/) | Sync a commit from the gemini remote into sync-upstream for empower-site. |
| [feature-issue](skills/feature-issue/) | Implement a feature from a GitHub issue with a structured, review-first workflow. |
| [git-branch-cleanup](skills/git-branch-cleanup/) | Safely clean merged and stale git branches with explicit confirmations. |
| [laravel-simplifier](skills/laravel-simplifier/) | Simplify and refine PHP/Laravel code for clarity and maintainability without changing behavior. |
| [pr-review](skills/pr-review/) | Review a GitHub pull request, run targeted checks, and provide a decision-ready summary. |
| [prd-discovery](skills/prd-discovery/) | Interview the user and write a PRD for Ralph in .prd/prd-<feature>.md. |
| [prd-to-json](skills/prd-to-json/) | Convert .prd PRD markdown into .prd/prd.json with validation. |
| [wp-plugin-changelog](skills/wp-plugin-changelog/) | Generate a WordPress plugin changelog focused on user value and update readme.txt when requested. |
| [wp-plugin-tag](skills/wp-plugin-tag/) | Create, verify, list, or delete WordPress plugin version tags safely. |
| [wp-plugin-version](skills/wp-plugin-version/) | Analyze changes and update WordPress plugin version references safely. |

## Structure

```
skills/
  <skill-name>/
    SKILL.md
    templates/
    scripts/
```

## Installation

Recommended: symlink into each agent's skills directory.

```bash
# Claude Code
ln -s /path/to/skills/skills ~/.claude/skills

# OpenCode
ln -s /path/to/skills/skills ~/.config/opencode/skills

# Codex
ln -s /path/to/skills/skills ~/.codex/skills

# Amp
ln -s /path/to/skills/skills ~/.config/agents/skills
```

## Usage

Invoke directly:

```
/commit
/feature-issue 123
/pr-review 456
```

## Guidelines

General behavior guidance is stored in `GUIDELINES.md`.
