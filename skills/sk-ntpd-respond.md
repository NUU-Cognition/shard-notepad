# Skill: Respond

Respond to a single notepad file or branch. Called by [[wkfl-ntpd-continue]] for each thread with new content.

# Input

- The notepad file (or branch) to respond to
- The new content to address

# Actions

1. Read the file (and the parent up to `branched-at` if this is a branch)
2. Identify the last section heading number in the file
3. If the user wrote new text without a `# N` heading, add the next heading first
4. If the user already wrote a heading, use it
5. Append the `>[!example] Agent Response` callout below the user text
6. Always leave two blank lines after the response
7. If the response requires internal actions (creating files, running commands, etc.), execute them as nested operations — do the action, then report in the response

# Section Ordering

Each section follows this order:
1. `# N` heading
2. Human text (always immediately after the heading)
3. `>[!example] Agent Response` callout
4. Two blank lines
5. `# N+1` heading (next section, ready for the user's next input)

If the agent responds twice with no new human text in between, skip the heading — just append another callout under the same section.

# Section Numbering

- **Main notepad:** `# 1`, `# 2`, `# 3`... (sequential integers)
- **Branch (1st from main):** `# N.1`, `# N+1.1`, `# N+2.1`... (`.1` suffix)
- **Branch (2nd from main):** `# N.2`, `# N+1.2`... (`.2` suffix)
- **Nested branch:** adds another dot level: `# N.B.C`
- The heading number is auto-added by the agent, not the user

# Guidelines

- Address the new content directly
- Be conversational but substantive
- Ask clarifying questions when needed
- Engage deeply — be comprehensive, not lazy
- If user typed in terminal while workflow was active, that content should already be in the notepad — respond to it
