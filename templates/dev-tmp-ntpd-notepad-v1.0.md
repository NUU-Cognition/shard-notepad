# Filename: Mesh/Types/Notepads/(Notepad) XXX [Topic Name].md

/* XXX is a 3-digit number. Get it with: flint helper type newnumber Notepad */

```markdown
---
id: [generate-uuid4]
tags:
  - "#ntpd/notepad"
status: [active|archived]
forked-from:
forks:
artifacts:
[agent]-sessions:
template: "[[dev-tmp-ntpd-notepad-v1.0]]"
authors: /* from flint whoami (the machine-global Name); omit if no Name is set */
  - "[[@Person Name]]"
---

# 1

[User writes topic/initial message here. Agent responds with callout below.]

>[!example] Agent Response
>[Agent responds in callout format]


# 2

[Conversation continues with # 2, # 3, etc.]
```

/* Notes:
   - forked-from: populated by sk-ntpd-fork when this notepad is a fork (wikilink to source)
   - forks: appended to by sk-ntpd-fork when this notepad is forked from (list of wikilinks)
   - artifacts: appended to by sk-ntpd-attach
   - Section headings (# 1, # 2, ...) are auto-incremented by the agent (sequential integers only)
   - State transitions: active → archived (via wkfl-ntpd-finish)
   - Inline edits: user text between a callout and the next # N triggers in-place revision
   - Action execution: pre/post callouts within the same section for external work
*/
