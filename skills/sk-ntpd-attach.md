# Skill: Attach

Create an artifact derivative of a notepad.

# Input

- The notepad to attach to
- Artifact type (e.g., Spec, Sketch, Diagram, Draft, Snippet — any `(Type)`)
- Artifact name
- Artifact content

# Actions

1. Create the artifact file:
   - Filename: `(Notepad) XXX Topic . (Type) [Artifact Name].md`
   - Location: `Mesh/Types/Notepads/` (same folder as the parent notepad)
2. Set frontmatter:
   - Use the existing template for the artifact type (e.g., `tmp-proj-task` for tasks, `tmp-f-spec` for specs, etc.)
   - Add `parent: "[[parent notepad link]]"` to the frontmatter
3. Write the artifact content
4. Append the artifact wikilink to the parent notepad's `artifacts:` frontmatter list

# Guidelines

- Artifacts are any typed output that deserves its own file
- Use descriptive types: `(Spec)`, `(Sketch)`, `(Draft)`, `(Diagram)`, `(Snippet)`, `(List)`, etc.
- Artifacts don't have the numbered section / callout conversation format — they're just documents
- On `wkfl-ntpd-finish`, artifacts may be promoted to standalone files or absorbed into Session Output

# Output

- New artifact file in `Mesh/Types/Notepads/`
- Artifact link appended to parent's `artifacts:` frontmatter
