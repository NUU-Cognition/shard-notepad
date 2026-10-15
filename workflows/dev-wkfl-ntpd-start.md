> [!important] THIS FILE IS AN INSTRUCTION. WHEN REFERENCED IT IS MEANT TO BE TAKEN AS AN ACTION.

This workflow belongs to the Notepad shard. Ensure you have @init-ntpd.md in context before continuing.

# Workflow: Start Notepad

Create a new notepad and begin brainstorming.

# Invocation

You can run this workflow as a shard invocation. The invocation is a durable record of the notepad: its steps, its output, and the tasks that start inside it. The stages below do not change.

- Start the workflow with `flint shard invoke ntpd start --input topic="<topic>"`.
- After Stage 1, set the output: `flint shard invocations set-output <id> notepad="(Notepad) NNN Title"`. The hint after each write prints the command with the id of the invocation.
- Mark each step when it is done: `flint shard step done <step> --evidence "<…>"`. The steps are `create`, `gather`, `converse`, and `finish`. `flint shard step` shows the current step.
- Each turn of the conversation stays inside the `converse` step. The step repeats: mark it done only when the person ends the conversation.
- When a turn asks for work, the work runs as a child invocation: `flint shard invoke proj create_and_do_task`. The task opens inside the notepad, with no flag. When the task closes, the notepad is the current frame again.
- When no invocation is open, follow the stages with no record.

# Input

- Topic for the notepad
- Initial message/question (optional)

# Actions

## Stage 1: Create Notepad

1. Get the next notepad number with `flint helper type newnumber Notepad`
2. Create the notepad using [[dev-tmp-ntpd-notepad-v1.0]] with:
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

1. Respond to the topic/initial message using [[dev-sk-ntpd-respond]]
2. The response goes under `# 1` as a `>[!example] Agent Response` callout
3. Create the `# 2` section making it ready for user to respond
4. The workflow remains active — any subsequent terminal messages are appended to the notepad under the next section heading before the agent responds

## Stage 4: Finish

1. When the person ends the conversation, run [[dev-wkfl-ntpd-finish]] on the notepad
2. With an open invocation, close it after the finish: `flint shard invocations close <id> --outcome done`

# Terminal Integration

While this workflow is active:
- User messages typed in the terminal are appended to the notepad under the next `# N` heading
- The agent then responds using [[dev-wkfl-ntpd-continue]]
- This continues until the user explicitly ends the conversation or runs `dev-wkfl-ntpd-finish`

# Output

- New notepad in `active` state
- First section (`# 1`) with topic and initial response
- Workflow active for continued conversation
