---
name: commit
description: Semantically groups changed files and creates focused git commits automatically. Use when user says "/autocommit", "auto commit", or wants to commit multiple changes as logically grouped commits.
---

# Auto Commit

Follow these steps to create semantically grouped commits:

## 1. Analyze Current State

Run these commands to understand the changes:
- `git status` to see all changes (staged and unstaged)
- `git diff` to see unstaged changes
- `git diff --staged` to see staged changes
- `git log -5 --oneline` to understand the commit message style

## 2. Semantic Analysis

Analyze all changes and classify each file into semantic groups based on purpose:

When analyzing:

- Infer purpose from filenames, function names, and change patterns
- Group related files together (e.g., struct definition and files that use it)
- Look at the actual diff content to understand the intent

## 3. Decide: Single or Grouped Commits

- Use single commit when: 4 or fewer changed files or All changes have one clear, unified intent
- Use grouped commits when: 5+ changed files and 2+ independent semantic groups exist

## 4. Create Commits

For each semantic group:

1. Stage files in a **separate** Bash call: `git add <file1> <file2> ...`
2. Commit in a **separate** Bash call (never chain with `&&`):
   ```bash
   git commit -m "$(cat <<'EOF'
   Summary line here
   EOF
   )"
   ```
   - **Prefer summary-line only** (no body) when the summary is self-explanatory
   - Add a body **only** when the summary alone would be misleading or ambiguous
   - Maximum **3** bullet points in the body
   - Each bullet should describe *why*, not *what* (the diff shows what)
3. Run `git status` to verify the commit succeeded

## 5. Final Verification

After all commits:
- Run `git status` to check for any missed changes
- If uncommitted changes remain, analyze and commit them appropriately

Do not push to remote unless explicitly requested.
