# Story Framework

A structured approach to writing fiction with AI assistance, using markdown files and git for version control.

## Getting Started

1. Clone or copy this folder for your new project
2. Initialize git: `git init`
3. Start developing your story in the planning documents
4. Write your drafts in the `Drafts/` folder
5. Use git commits to track revisions (no need for versioned folders)

## Folder Structure

```
your-story/
├── Characters/
│   └── characters.md      # Character profiles and relationships
├── Plot/
│   └── outline.md         # Story structure and scene breakdown
├── Themes/
│   └── themes.md          # Central themes, motifs, and symbols
├── Setting/
│   └── world.md           # Locations, time period, world rules
├── Drafts/
│   └── (your story files) # One file per chapter/act, numbered: 01-chapter-one.md
├── Notes/
│   ├── style-guide.md     # Voice, tone, formatting conventions
│   └── editing-markup.md  # How to leave inline edit notes
└── Final/
    └── README.md          # Checklist for finalizing
```

## Workflow

### Planning Phase
1. Fill out character profiles in `Characters/characters.md`
2. Develop your plot structure in `Plot/outline.md`
3. Define themes and motifs in `Themes/themes.md`
4. Build your world in `Setting/world.md`
5. Establish voice and conventions in `Notes/style-guide.md`
6. **Review and approve** all planning docs before moving to drafting

These planning documents are the **source of truth** for your story. Complete them first.

### Writing Phase
1. Create one file per chapter/act in `Drafts/`: `01-title.md`, `02-title.md`, etc.
2. Commit regularly with descriptive messages
3. Use `git tag` to mark milestones: `git tag v1-first-draft`

### Revision Phase
1. Add inline edit notes using the markup in `Notes/editing-markup.md`
2. Ask your AI assistant to "process edit notes"
3. Review and approve changes
4. Commit after each revision pass

### Finalization
1. Follow the checklist in `Final/README.md`
2. Copy approved files to `Final/`
3. Tag the release: `git tag v1-final`

## Creative Collaboration Approaches

The file `creative-approaches.md` defines six distinct modes for human-AI creative collaboration, ordered by degree of human control:

| Approach | AI Role | Best For |
|----------|---------|----------|
| **Author** | Critic only | Getting feedback without AI-generated content |
| **Muse** | Pure executor | Precise control over every detail |
| **Artisan** | Scaffolder | Structure and outlines, you write prose |
| **Debater** | Adversary | Stress-testing creative choices |
| **Creator** | Generative partner | Iterative drafting with AI assistance |
| **Curator** | Option generator | Exploring many possibilities quickly |

**To use:** Tell the AI which mode you want—"Let's work in Author mode" or "Curator mode: give me options." You can switch modes mid-session.

See `creative-approaches.md` for full details on each approach's behaviors and sample prompts.

## Working with AI Assistants

This framework is designed for collaborative writing with AI. The AI can:

- Help develop characters, plot, and themes in the planning docs
- Write drafts based on your outlines
- Process edit notes you leave in the text
- Follow the style guide for consistency
- Use git to track all changes

### Key Commands
- "Process edit notes" - Find and address all `{{...}}` markers
- "Show me the diff" - See uncommitted changes
- "Revise [section] to [instruction]" - Make specific edits

## Git Basics (If New to Git)

```bash
# Start tracking your project
git init

# Save your current state
git add .
git commit -m "Description of changes"

# See what's changed
git diff

# See history
git log --oneline

# Mark a milestone
git tag v1-first-draft

# Undo uncommitted changes to a file
git checkout -- filename.md
```

### Writing Good Commit Messages

Commit messages are your revision history. Focus on **why** you made changes, not just what changed—the diff already shows what. Good commit messages let you:

- Understand your creative decisions months later
- Find when and why a passage changed
- Revert to earlier versions with confidence

**Format:**
```
Short summary (50 chars or less)

Longer explanation if needed. Describe your reasoning:
- Why did you cut that scene?
- What feedback prompted this revision?
- What problem were you solving?
```

**Examples:**
```bash
# Good - explains the why
git commit -m "Cut prologue - slowed pacing, info now woven into ch 1"
git commit -m "Rework Sarah's intro to show competence before vulnerability"
git commit -m "Add tension to cafe scene per beta reader feedback"

# Less useful - only describes what
git commit -m "Edited chapter 3"
git commit -m "Fixed typos"
git commit -m "Rewrote dialogue"
```

## Tips

- Commit often with clear messages
- Use tags for major milestones (drafts, revisions, final)
- Keep the style guide updated as you establish patterns
- The planning docs are living documents—update them as the story evolves

