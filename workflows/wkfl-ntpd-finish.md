This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Finish Notepad

End a notepad session by flattening the derivative tree, extracting artifacts, and archiving.

# Input

- The notepad to finish

# Actions

## Stage 1: Discover Derivative Tree

1. Read the main notepad
2. Glob for all derivatives: files matching `(Notepad) XXX Topic * . (*) *.md` in `Mesh/Types/Notepads/`
3. Categorize:
   - **Branches** — `(Branch)` derivatives, may contain conversation content to consolidate
   - **Artifacts** — all other typed derivatives, candidates for promotion

## Stage 2: Review and Extract

1. Read all branches and the main notepad
2. Identify extractable items across the entire tree:

| Type | Destination | Format |
|------|-------------|--------|
| Tasks/specs | `(Task) Name.md` | Links back to notepad |
| Ideas | Ideas Board | With notepad reference |
| Decisions/facts | Memories (if exists) | With notepad reference |
| Others | Any | Whatever fits |

3. For artifact derivatives: determine if each should be **promoted** (moved/renamed to standalone) or **absorbed** (content merged into Session Output)

## Stage 3: Flatten and Draft

1. Consolidate branch content into the main notepad's Session Output
2. **Coherence rule:** the Session Output must read as a standalone summary — someone reading it should understand the full outcome without needing to open any branches or derivatives. Write it as prose/bullets that flow naturally, not just a list of links.
3. Structure:
   - Summarize each branch's key conclusions (not just "key points" — what was decided, what was built, what was learned)
   - For promoted artifacts, explain what they are and why they matter
   - For absorbed artifacts, inline their essential content
4. Add Session Output section at the top of the notepad (after frontmatter):

```markdown
# Session Output

**Summary:**
[1-2 paragraph summary of the entire notepad session — what was explored, what was decided]

**Branches:**
- (Branch) 1 Name — what was concluded
- (continued)

**Archived:** YYYY-MM-DD
```

5. Present to user for review and confirmation

## Stage 4: Archive

1. Update main notepad status to `archived`
2. Update all derivatives status to `archived`
3. Promote standalone artifacts (rename/move out of notepad namespace if appropriate)
5. Report what was created, promoted, and archived

# Output

- Archived notepad with Session Output summary
- All branches archived
- Artifacts promoted or absorbed
- Dashboard reflects updated status
