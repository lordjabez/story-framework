# Editing Markup Reference

This document defines inline markup for drafts. There are two types:

| Syntax | Name | Purpose | When Removed |
|--------|------|---------|--------------|
| `{{...}}` | Edit notes | Revision instructions | After processing |
| `[[...]]` | Author notes | Context for AI/author | At finalization |

---

## Author Notes `[[ ]]`

Author notes provide context, metadata, and reminders. They travel with the draft and are only removed when producing final text.

### Basic Syntax

```markdown
[[any note or reminder]]
[[TYPE: structured information]]
```

**Multiline notes** are supported—useful for chapter headers or complex context:

```markdown
[[
POV: Sarah, close third
TIMELINE: Tuesday morning, Day 3
MOOD: cautious optimism, underlying tension
THREADS: job interview, reconciliation with mother
NOTE: This chapter mirrors the structure of chapter 2
]]
```

You can also use multiline for longer notes:

```markdown
[[CONTEXT:
Reader knows: Sarah got the job, she's hiding it from Mom
Reader doesn't know: The company is failing, Marcus warned her
Dramatic irony: Mom is about to announce she's selling the house
]]
```

### Common Types

| Type | Purpose | Example |
|------|---------|---------|
| `[[POV: ...]]` | Point of view character | `[[POV: Sarah, close third]]` |
| `[[TIMELINE: ...]]` | When this happens | `[[TIMELINE: Day 3, morning, ~2 hours since ch 4]]` |
| `[[MOOD: ...]]` | Emotional tone/atmosphere | `[[MOOD: tense, building dread]]` |
| `[[THREADS: ...]]` | Active plot threads here | `[[THREADS: romance subplot, missing letter]]` |
| `[[CONTEXT: ...]]` | What reader knows/doesn't | `[[CONTEXT: reader doesn't know he's lying]]` |
| `[[TODO: ...]]` | Reminder for later | `[[TODO: plant the key before scene 3]]` |
| `[[RESEARCH: ...]]` | Needs fact-checking | `[[RESEARCH: verify hospital procedure]]` |
| `[[NOTE: ...]]` | General note | `[[NOTE: beta reader loved this section]]` |

### Placement

**Chapter header** (scene-level context):
```markdown
[[
POV: Sarah, close third
TIMELINE: Tuesday morning, Day 3
MOOD: cautious optimism, underlying tension
THREADS: job interview, reconciliation with mother
]]

# Chapter Five

Sarah checked her reflection one last time...
```

**Inline** (local context):
```markdown
"I never said that," he replied. [[CONTEXT: he's lying, reader should sense it]]

She walked past the old oak tree [[TODO: described differently in ch 2, check]] and up the porch steps.
```

**Scene breaks**:
```markdown
---

[[TIMELINE: 3 hours later, same day]]
[[MOOD: shift to darker tone]]

The call came at noon.
```

### For AI Assistants

- **Read** author notes to understand context, but don't act on them like edit notes
- **Preserve** author notes when revising—never remove them unless producing final text
- **Reference** them to maintain consistency (POV, timeline, mood, active threads)
- **Add** new author notes when you introduce details the author should track
- When searching: `grep -rn "\[\[" Drafts/`

---

## Edit Notes `{{ }}`

Edit notes are revision instructions. Process them when asked, then remove.

### Syntax

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

