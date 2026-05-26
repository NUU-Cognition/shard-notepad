> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Continue Notepad

Continue an active notepad conversation. This is the entry point for the `continue` keyword.

# Input

- The notepad to continue (or auto-detect from context)
- Mode: `continue` (default) or `continue --confirm`

# Actions

1. Read the notepad file
2. Identify new content since the last `>[!example] Agent Response` callout
3. Determine the response mode (see [[dev-sk-ntpd-respond]] for the three modes):
   - **New Turn** — new user text after the last heading
   - **Inline Edit** — user text between an existing callout and the next heading
   - **Action Execution** — user requests external work
4. Respond using [[dev-sk-ntpd-respond]] in the appropriate mode
5. If `--confirm` mode: present the intended response/action, wait for approval, then write

# Terminal Integration

While a notepad session is active:
- User messages typed in the terminal are appended to the notepad under the next `# N` heading
- Then this workflow is triggered to respond

# Output

- Response appended to the notepad (or existing response revised for inline edits)
- Section headings auto-added where missing
