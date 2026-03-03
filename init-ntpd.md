# Notepad Shard

Document-based brainstorming. Persistent, editable conversations with branching and derivatives.

## Rules

1. **Sections are numbered.** Every exchange gets a `# N` heading. Responses auto-increment the heading. This enables `[[notepad#3]]` linking.
2. **Responses use callout format.** Always `>[!example] Agent Response` followed by `>content`. Leave two blank lines after.
3. **Terminal messages are appended.** While a notepad workflow is active, any user messages typed in the terminal are appended to the current notepad/branch under the next section heading.
4. **Branches reference the parent.** Branches don't copy the parent content. They link back via the `parent` field and start fresh from the branch point. The agent reads the parent for context when working in the branch. Dotted section numbering (`N.B`).
5. **Derivatives use dot naming.** Branches: `(Notepad) 035 Topic . (Branch) 1 Name.md`. Artifacts: `(Notepad) 035 Topic . (Type) Name.md`. All live in `Mesh/Types/Notepads/`.
6. **Continue is the keyword.** `continue` responds to all active threads. `continue --confirm` presents the intended response/action for approval first.
7. **Selective responding.** By default, respond to all active threads. If a branch is obviously inactive or specific branches are declared, only respond to the active ones.

## Lifecycle

```
active → archived
```

| Status | Meaning |
|--------|---------|
| `active` | Notepad in use |
| `archived` | Session complete, artifacts extracted, tree flattened |

## Conversation Flow

1. `wkfl-ntpd-start` — creates notepad, gathers context, writes first response under `# 1`
2. User writes, then `wkfl-ntpd-continue` responds with auto-numbered sections
3. Branch with `sk-ntpd-branch`, attach artifacts with `sk-ntpd-attach`
4. `wkfl-ntpd-finish` — flattens derivatives, promotes artifacts, archives the tree

## Branching

Branches diverge the conversation into a side-thread.

- **Branch marker in parent:** `# Branched: [[link]]` inserted at the branch point (dead heading, no content)
- **Branch numbering:** 1st branch = `(Branch) 1 Name`, 2nd = `(Branch) 2 Name`, sub-branch of 1 = `(Branch) 1.1 Name`
- **Section numbering:** 1st branch uses `.1` suffix (`# 4.1`, `# 5.1`...), 2nd branch `.2`, etc.
- **Nested branching:** adds another dot level (`# 4.1.1`, `# 4.1.2`...)
- **Branch frontmatter:** adds `parent` field

## Derivatives

Branches and artifacts are tracked in the parent's frontmatter (`branches:` and `artifacts:` lists). When you branch or attach, append the wikilink to the parent's YAML.

| Type | Pattern | Purpose |
|------|---------|---------|
| Branch | `... . (Branch) B Name.md` | Side-thread conversation (B = branch number) |
| Artifact | `... . (Type) Name.md` | Any typed output (spec, sketch, diagram, etc.) |

## File Structure

- Location: `Mesh/Types/Notepads/`
- Archive: `Mesh/Archive/Notepads/`
- Format: `(Notepad) XXX Topic Name.md`
- Dashboard: `(Dashboard) Notepads.md`

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Respond | `sk-ntpd-respond.md` | Continue conversation with auto-numbered sections |
| Branch | `sk-ntpd-branch.md` | Create a branch from the current notepad |
| Attach | `sk-ntpd-attach.md` | Create an artifact derivative |

## Workflows

| Workflow | File | Purpose |
|----------|------|---------|
| Start | `wkfl-ntpd-start.md` | Create notepad and begin conversation |
| Continue | `wkfl-ntpd-continue.md` | Continue conversation with auto-numbered sections |
| Finish | `wkfl-ntpd-finish.md` | Flatten tree, extract artifacts, archive |
