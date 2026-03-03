This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Continue Notepad

Continue an active notepad conversation. This is the entry point for the `continue` keyword.

# Input

- The notepad to continue (or auto-detect from context)
- Mode: `continue` (default) or `continue --confirm`

# Actions

1. Read the main notepad file
2. Glob for all active branches: `(Notepad) XXX Topic . (Branch) *.md`
3. Read all active branches
4. For each file (main + branches), identify new content since the last `>[!example] Agent Response` callout
5. Determine which threads to respond to:
   - **Default:** all threads with new content
   - **Selective:** skip obviously inactive branches (no new content), or respond only to user-declared branches
6. For each thread with new content, respond using [[sk-ntpd-respond]]:
   - If the user wrote new text without a `# N` heading, add the next heading first
   - If the user already wrote a heading, use it
   - Append the `>[!example] Agent Response` callout below the user text
   - Leave two blank lines after the response
7. If `--confirm` mode: present the intended responses/actions for all threads, wait for approval, then write

# Terminal Integration

While a notepad session is active:
- User messages typed in the terminal are appended to the notepad under the next `# N` heading
- Then this workflow is triggered to respond

# Output

- Responses appended to all active threads with new content
- Section headings auto-added where missing
