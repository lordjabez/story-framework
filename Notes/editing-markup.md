# Editing Markup Reference

This document defines inline markup for editing notes. Add these directly in your draft files while reading. When ready, ask your AI assistant to "process edit notes" or "revise based on markup."

---

## Markup Syntax

All edit notes use double curly braces: `{{comment}}` or `{{TYPE: comment}}`

| Markup | Purpose | Example |
|--------|---------|---------|
| `{{...}}` | Simple comment, no action needed | `{{love this line}}` |
| `{{NOTE: ...}}` | Explicit note, no action needed | `{{NOTE: great pacing here}}` |
| `{{FIX: ...}}` | Something's wrong, needs correction | `{{FIX: wrong character name}}` |
| `{{CUT: ...}}` | Delete this text | `{{CUT: too wordy}}` |
| `{{EXPAND: ...}}` | Add more here | `{{EXPAND: describe the room}}` |
| `{{REWORD: ...}}` | Rephrase this | `{{REWORD: awkward phrasing}}` |
| `{{MOVE: ...}}` | Relocate this section | `{{MOVE: should come after the intro}}` |
| `{{?: ...}}` | Question for discussion | `{{?: is this consistent with act 2?}}` |

**Note:** Any `{{comment}}` without a recognized TYPE: prefix is treated as a simple note (no action required).

---

## Placement

**Inline** (for specific words/phrases):
```markdown
She walked into the {{FIX: bar}} lounge and ordered a drink.
```

**Block** (for paragraphs/sections):
```markdown
{{CUT: this whole paragraph drags}}
Maya thought about her childhood for several long paragraphs
that don't advance the plot at all...
```

**Spanning** (mark start and end):
```markdown
{{REWORD:START - too technical}}
The cache invalidation protocol triggered a cascade failure
across the distributed node cluster.
{{REWORD:END}}
```

---

## Examples in Context

```markdown
Jordan laughed, a real one, warm and surprised. {{great moment}}

"I counted fifty-three." {{EXPAND: add her reaction to this}}

{{CUT: removes pacing}}
She thought about all the times she'd been in airports like this one,
waiting for flights that never seemed to come on time.

{{callback to act 1?}}
Maya adjusted her puffer jacket and fled.

{{?: should we mention the jacket here or wait?}}
```

---

## Processing Notes

When you ask the AI to process these notes, it will:

1. **List all notes** found in the file(s)
2. **Ask for confirmation** before making changes
3. **Address each note** in order, or as a batch
4. **Remove the markup** after resolving

You can also ask to:
- "Show me all FIX notes"
- "Process only CUT notes"
- "List questions for discussion"
- "Ignore NOTE markers, process everything else"

---

## For AI Assistants

If you're an AI assistant working with this repository and don't have prior chat context:

### Finding Edit Notes
```bash
grep -rn "{{" Drafts/
```

### Processing Workflow
1. Parse all `{{...}}` markers in the specified file(s)
2. Classify each marker:
   - Has `TYPE:` prefix (FIX, CUT, EXPAND, REWORD, MOVE, NOTE, ?) → use that type
   - No prefix → treat as simple note (no action)
3. Present a summary to the user, grouped by type
4. For each actionable note (FIX, CUT, EXPAND, REWORD, MOVE):
   - Show the surrounding context
   - Propose a specific revision
   - Wait for approval before applying
5. For NOTE markers and simple `{{comments}}`: acknowledge but take no action
6. For `?:` markers: discuss with user before proceeding
7. After processing, remove the markup from resolved notes
8. Leave unresolved notes in place

### Regex Patterns

Match all markers:
```
\{\{(.+?)\}\}
```

Check if marker has a TYPE prefix:
```
^(NOTE|FIX|CUT|EXPAND|REWORD|MOVE|\?):?\s*(.+)$
```

If no match on the TYPE pattern, treat as simple note.

For spanning markers:
```
\{\{(REWORD|CUT|MOVE):START\s*[-–—]?\s*(.+?)\}\}
([\s\S]*?)
\{\{(\1):END\}\}
```

