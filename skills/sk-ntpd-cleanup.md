This skill belongs to the Notepad shard. Ensure you have [[init-ntpd]] in context before continuing.

# Skill: Cleanup Notepads

Scan all notepads, identify stale or broken artifacts, and tidy them up with user approval.

# Input

- (Optional) Specific notepads to check — defaults to all in `Mesh/Types/Notepads/`

# Actions

1. **Read template.** Read [[tmp-ntpd-notepad-v1.0]] to understand the canonical frontmatter schema, required tags, and valid status values.

2. **Scan.** Read the YAML frontmatter (only) of every file in `Mesh/Types/Notepads/` matching `(Notepad) *.md`.

3. **Detect issues.** Compare each notepad's frontmatter against the template. Flag notepads with any of these problems:
   - **Status mismatch:** terminal status (e.g. `archived`) but file still in `Mesh/Types/Notepads/` instead of `Mesh/Archive/Notepads/`
   - **Invalid status:** status value not in the template's enum (check template for valid values)
   - **Duplicate IDs:** same `id` value used by multiple notepads
   - **Non-UUID IDs:** `id` is not a valid UUID v4
   - **Missing/wrong tags:** tags don't match what the template requires
   - **Empty fields:** fields that exist but have no value (e.g. `increment:` with nothing after it) — either populate or remove
   - **Missing template field:** no `template: "[[tmp-ntpd-notepad-v1.0]]"` in frontmatter

4. **Report.** Present findings to the user as a table:
   ```
   | Notepad | Issue | Suggested Action |
   ```
   Group by issue type. If no issues found, say so and stop.

5. **Ask.** Ask the user which items to fix and which to archive. Wait for confirmation.

6. **Fix.** For each confirmed action:
   - **Archive:** Add `#archived` to tags, then move file to `Mesh/Archive/Notepads/`
   - **Fix ID:** Generate a new UUID v4 and replace the invalid one
   - **Fix tags:** Update tags to match the template
   - **Fix status:** Replace invalid status with a valid value from the template
   - **Fix empty fields:** Remove empty field lines, or populate if user specifies

# Output

- List of changes made
- Count of archived / fixed notepads
