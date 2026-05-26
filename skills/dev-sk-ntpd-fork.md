> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

# Skill: Fork

Fork a notepad into a new standalone notepad. The fork is a full copy that starts its own life.

# Input

- The notepad to fork from
- New topic name (optional — defaults to original topic with "(Fork)" suffix)

# Actions

1. Read the source notepad
2. Get the next notepad number with `flint helper type newnumber Notepad`
3. Copy the entire source file content (frontmatter + body)
4. Create the new notepad file:
   - Filename: `(Notepad) XXX [New Topic Name].md`
   - Generate a new UUID for the `id` field
   - Set `forked-from: "[[source notepad link]]"` in frontmatter
   - Set status to `active`
   - Update `claude-sessions` with the current session ID
   - Clear `forks:` and `artifacts:` lists (the fork starts fresh for derivatives)
   - Keep all conversation content from the source
5. Append the fork wikilink to the source notepad's `forks:` frontmatter list

# Guidelines

- Forks are fully independent — editing one does not affect the other
- The `forked-from` field is a historical reference, not an active link
- Forks keep the full conversation history so they're self-contained
- After forking, both notepads continue independently with sequential `# N` numbering

# Output

- New notepad file in `Mesh/Types/Notepads/`
- Fork link appended to source's `forks:` frontmatter
