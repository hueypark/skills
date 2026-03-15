---
name: english-improvement
description: Translates Korean commands from the session into natural English and corrects awkward expressions. Use when user says "/english-improvement", "english improvement", or wants to review their English usage.
---

# English Improvement

Translate Korean commands from this session into natural English expressions and correct awkward English.

## Procedure

### 1. Find Current Session Log

Session logs are stored at `~/.claude/projects/<project-slug>/<session-uuid>.jsonl`.

Find the current session's log file:

```
Glob(pattern="*.jsonl", path="~/.claude/projects/-Users-ab180-go-src-github-com-hueypark-skills/")
```

Pick the **most recently modified** `.jsonl` file (this is the current session). Ignore files in `subagents/` subdirectories.

### 2. Parse and Extract User Messages

Read the JSONL file. Each line is a JSON object. Focus on:

- `type: "user"` → User messages (`message.content` has the prompt text)

Extract all user-written text: commands, requests, chat messages, and plan-mode feedback.

### 3. Analyze English Usage

From the extracted user messages:

1. Collect all Korean commands/requests and provide natural English equivalents
2. Review and correct awkward or incorrect English expressions
3. Suggest useful expression patterns

### 4. Large Logs

If the log file is too large to read at once, use the `offset` and `limit` parameters to read in chunks. Focus on the most recent portion first.

## Output Format

### Korean → English

| Korean | English | Notes |
|--------|---------|-------|
| [Korean command] | [English expression] | [Usage tip] |

### English Corrections

| Original | Corrected | Explanation |
|----------|-----------|-------------|
| [Awkward expression] | [Natural expression] | [Why it's better] |

### Useful Patterns

- [Pattern]: [Example usage]

## Common Issues to Check

- Grammar errors (subject-verb agreement, tense, articles)
- Unnatural phrasing or word order
- Incorrect prepositions
- Overly literal translations from Korean
- Technical terminology misuse

## Guidelines

- Focus on expressions commonly used in development contexts
- Prefer concise and clear English expressions
- Provide multiple ways to express the same intent
- When correcting, explain the reason briefly for learning purposes
