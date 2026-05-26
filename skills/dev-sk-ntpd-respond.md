> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

# Skill: Respond

Respond to a notepad. Handles three modes: new turn, inline edit, and action execution.

# Input

- The notepad file to respond to
- The new content to address

# Actions

## 1. Detect Response Mode

Read the notepad and determine which mode applies:

**New Turn** — User text appears after the last `# N` heading with no prior agent response in that section. This is the normal case.

**Inline Edit** — User text appears between an existing `>[!example] Agent Response` callout and the next `# N` heading. The user is asking to revise the existing response, not start a new turn.

**Action Execution** — The user's message requests an external action (creating files, running commands, executing another workflow/skill). This uses the pre/post action pattern within the current turn.

## 2. New Turn (default)

1. Identify the last section heading number in the file
2. If the user wrote new text without a `# N` heading, add the next heading first
3. If the user already wrote a heading, use it
4. Append the `>[!example] Agent Response` callout below the user text
5. Leave two blank lines after the response
6. Append the next `# N+1` heading (and two blank lines) after your reply, making it ready for the user to continue

## 3. Inline Edit

1. Identify the section where the edit instruction appears (between an existing callout and the next `# N` heading)
2. Read the edit instruction — the user is telling you how to revise the response above
3. **Replace the existing `>[!example] Agent Response` callout in that section** with the revised version
4. Remove the user's edit instruction text (it was a directive, not conversation content)
5. Do NOT create a new section heading — the turn stays as-is, just with an updated response

## 4. Action Execution

When the user's message asks you to perform an external action (create a file, run a command, execute a skill/workflow, etc.):

1. Append a **pre-action callout** in the current section:
   ```
   >[!example] Agent Response — Pre-Action
   > Brief description of what you're about to do
   ```
2. **Execute the action** (create files, run commands, etc.)
3. Append a **post-action callout** in the same section:
   ```
   >[!example] Agent Response — Post-Action
   > Summary of what was done, results, links to created artifacts
   ```
4. Leave two blank lines
5. Append the next `# N+1` heading to start a new turn

If the message involves both discussion and action, combine: write the discussion response first, then the pre-action note, execute, then the post-action note.

# Section Ordering

Each section follows this order:
1. `# N` heading
2. Human text (always immediately after the heading)
3. `>[!example] Agent Response` callout (one or more — see action pattern)
4. Two blank lines
5. `# N+1` heading (next section, ready for the user's next input)

# Section Numbering

Sequential integers only: `# 1`, `# 2`, `# 3`, etc.

# Guidelines

- Address the new content directly
- Be conversational but substantive
- Ask clarifying questions when needed
- Engage deeply — be comprehensive, not lazy
- If user typed in terminal while workflow was active, that content should already be in the notepad — respond to it
- For inline edits, preserve the intent of the original response while applying the edit instruction
- For action execution, the pre-action note should be brief (one line), the post-action note should be thorough
