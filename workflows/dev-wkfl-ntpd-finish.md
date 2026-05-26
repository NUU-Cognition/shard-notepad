> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Finish Notepad

End a notepad session by extracting artifacts and archiving.

# Input

- The notepad to finish

# Actions

## Stage 1: Review

1. Read the notepad
2. Glob for any artifact derivatives: `(Notepad) XXX Topic . (*) *.md` in `Mesh/Types/Notepads/`
3. Read all derivatives

## Stage 2: Extract

1. Identify extractable items from the conversation:

| Type | Destination | Format |
|------|-------------|--------|
| Tasks/specs | `(Task) Name.md` | Links back to notepad |
| Ideas | Ideas Board | With notepad reference |
| Decisions/facts | Memories (if exists) | With notepad reference |
| Others | Any | Whatever fits |

2. For artifact derivatives: determine if each should be **promoted** (moved/renamed to standalone) or **absorbed** (content summarized in Session Output)

## Stage 3: Session Output

1. Add Session Output section at the top of the notepad (after frontmatter):

```markdown
# Session Output

**Summary:**
[1-2 paragraph summary of the entire notepad session — what was explored, what was decided]

**Artifacts:**
- (Type) Name — what it is and why it matters
- (continued)

**Archived:** YYYY-MM-DD
```

2. **Coherence rule:** the Session Output must read as standalone — someone reading it should understand the full outcome without needing to read every section.
3. Present to user for review and confirmation

## Stage 4: Archive

1. Update notepad status to `archived`
2. Update all derivative statuses to `archived`
3. Promote standalone artifacts (rename/move out of notepad namespace if appropriate)
4. Report what was created, promoted, and archived

# Output

- Archived notepad with Session Output summary
- Artifacts promoted or absorbed
- Dashboard reflects updated status
