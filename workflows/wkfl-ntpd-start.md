This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Start Notepad

Create a new notepad and begin brainstorming.

# Input

- Topic for the notepad
- Initial message/question (optional)

# Actions

## Stage 1: Create Notepad

1. Get the next notepad number with `flint helper type newnumber Notepad`
2. Create the notepad using [[tmp-ntpd-notepad-v1.0]] with:
   - Numbered filename: `(Notepad) XXX Topic Name.md`
   - Status: `active`
   - First section heading: `# 1`
3. If initial message provided, add it under `# 1`

## Stage 2: Gather Context

1. Run parallel subagents to find context needed for this conversation:
   - Search the Flint (Mesh files, related notepads, tasks, plans)
   - Search referenced codebases (if the topic relates to code)
   - Read any linked documents from the initial message
2. Synthesize findings for the response

## Stage 3: Begin Conversation

1. Respond to the topic/initial message using [[sk-ntpd-respond]]
2. The response goes under `# 1` as a `>[!example] Agent Response` callout
3. The workflow remains active — any subsequent terminal messages are appended to the notepad under the next section heading before the agent responds

# Terminal Integration

While this workflow is active:
- User messages typed in the terminal are appended to the notepad under the next `# N` heading
- The agent then responds using [[wkfl-ntpd-continue]]
- This continues until the user explicitly ends the conversation or runs `wkfl-ntpd-finish`

# Output

- New notepad in `active` state
- First section (`# 1`) with topic and initial response
- Workflow active for continued conversation
