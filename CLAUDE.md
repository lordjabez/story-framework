# Claude Code Instructions

This is a creative writing framework. Read and follow the instructions in these files:

## Required Reading

1. `.ai-instructions.md` - Your role and workflow as a writing assistant
2. `Notes/style-guide.md` - Voice, tone, and formatting rules for this project
3. `Notes/editing-markup.md` - How to process `{{...}}` edit markers
4. `creative-approaches.md` - Six collaboration modes (Author, Muse, Artisan, Debater, Creator, Curator)

When a user says "I want to work in [X] mode" (e.g., "Curator mode", "Author mode"), read `creative-approaches.md` and follow the behaviors defined for that approach.

## Framework Structure

```
Characters/   - Character profiles and relationships
Plot/         - Story structure, scene breakdown, subplot tracking
Themes/       - Central themes, motifs, and symbols
Setting/      - Locations, time period, world rules
Continuity/   - Timeline and canonical facts for consistency
Drafts/       - Work in progress (numbered files: 01-title.md, 02-title.md)
Final/        - Completed work
Notes/        - Style guide and editing conventions
```

## Key Behaviors

- Read the style guide before writing new content
- Maintain consistency with planning docs (Characters, Plot, Themes, Setting)
- Use `---` for scene breaks within chapters
- Process `{{...}}` edit markers when asked (see editing-markup.md for types)
- Read `[[...]]` author notes for context; preserve them during revisions
- Show diffs after making revisions
- Don't commit unless explicitly asked
- When unsure about story decisions, ask

## Continuity Management

For novel-length work, actively maintain these files:

- `Continuity/timeline.md` - After writing a scene, log its in-story date/time
- `Continuity/facts.md` - When introducing details (descriptions, names, places), record them here
- `Plot/threads.md` - Track planted foreshadowing, subplot status, and payoffs

Before writing new scenes, check these files for established facts. Flag any inconsistencies you notice.

## Common Commands

- "Process edit notes" - Find and address all `{{...}}` markers in Drafts/
- "Write the next scene" - Check outline, maintain continuity, write prose
- "Show me the diff" - Display uncommitted changes
- "What's the current state?" - Summarize progress and open items
