# Notepad Shard

Document-based brainstorming. Persistent, editable conversations with forking and derivatives.

## Rules

1. **Sections are numbered.** Every exchange gets a `# N` heading (sequential integers: `# 1`, `# 2`, `# 3`...). This enables `[[notepad#3]]` linking.
2. **Responses use callout format.** Always `>[!example] Agent Response` followed by `>content`. Leave two blank lines after.
3. **Terminal messages are appended.** While a notepad workflow is active, any user messages typed in the terminal are appended to the current notepad under the next section heading.
4. **Inline edits revise in place.** If the user writes text between an existing agent response and the next `# N` heading, the agent revises the response in-place instead of creating a new turn. The edit instruction is removed after processing.
5. **Actions use pre/post callouts.** When a message triggers external work, the agent writes a pre-action callout, executes the work, then appends a post-action callout — all within the same section.
6. **Forks are full copies.** Forking duplicates the notepad as a new standalone notepad with its own number. Forks are independent — no parent/child tree, no shared state.
7. **Derivatives use dot naming.** Artifacts: `(Notepad) 035 Topic . (Type) Name.md`. All live in `Mesh/Types/Notepads/`.
8. **Continue is the keyword.** `continue` responds to the active notepad. `continue --confirm` presents the intended response/action for approval first.

## Lifecycle

```
active → archived
```

| Status | Meaning |
|--------|---------|
| `active` | Notepad in use |
| `archived` | Session complete, artifacts extracted |

## Conversation Flow

1. `dev-wkfl-ntpd-start` — creates notepad, gathers context, writes first response under `# 1`
2. User writes, then `dev-wkfl-ntpd-continue` responds with auto-numbered sections
3. Fork with `dev-sk-ntpd-fork`, attach artifacts with `dev-sk-ntpd-attach`
4. `dev-wkfl-ntpd-finish` — extracts artifacts, archives

## Response Modes

The respond skill (`dev-sk-ntpd-respond`) operates in three modes:

### New Turn (default)
User writes after the last `# N` heading → agent responds with a new callout → next heading created.

### Inline Edit
User writes between an existing agent response and the next `# N` heading → agent revises the response in-place → edit instruction removed.

This is for iterative refinement of generated content. The user can prompt the agent to edit a document draft, spec outline, or any generated response without creating a new turn.

### Action Execution
User asks for external work (create files, run commands, execute workflows) → agent writes a pre-action callout, executes, then appends a post-action callout. All within the same section.

```
# N

User asks to create a task

>[!example] Agent Response — Pre-Action
> Creating the task now...

>[!example] Agent Response — Post-Action
> Done. Created (Task) 281 at Mesh/Types/Tasks/. Status set to in-progress.


# N+1
```

## Forking

Forks create a new independent notepad from an existing one.

- **Fork copies everything** — the new notepad gets the full conversation history
- **Forks are standalone** — editing one does not affect the other
- **`forked-from` field** — historical reference linking back to the source
- **`forks` field** — source notepad tracks what was forked from it
- **Numbering continues sequentially** — forks use normal `# N` numbering, no dotted notation

## Derivatives

Artifacts are tracked in the notepad's frontmatter (`artifacts:` list). When you attach an artifact, append the wikilink.

| Type | Pattern | Purpose |
|------|---------|---------|
| Artifact | `... . (Type) Name.md` | Any typed output (spec, sketch, diagram, etc.) |

## File Structure

- Location: `Mesh/Types/Notepads/`
- Archive: `Mesh/Archive/Notepads/`
- Format: `(Notepad) XXX Topic Name.md`
- Dashboard: `(Dashboard) Notepads.md`

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Respond | `dev-sk-ntpd-respond.md` | Respond with new turn, inline edit, or action execution |
| Fork | `dev-sk-ntpd-fork.md` | Fork notepad into a new standalone notepad |
| Attach | `dev-sk-ntpd-attach.md` | Create an artifact derivative |
| Cleanup | `dev-sk-ntpd-cleanup.md` | Scan and tidy notepads |

## Workflows

| Workflow | File | Purpose |
|----------|------|---------|
| Start | `dev-wkfl-ntpd-start.md` | Create notepad and begin conversation |
| Continue | `dev-wkfl-ntpd-continue.md` | Continue conversation with auto-numbered sections |
| Finish | `dev-wkfl-ntpd-finish.md` | Extract artifacts, archive |
