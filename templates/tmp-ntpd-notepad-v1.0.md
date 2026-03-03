# Filename: Mesh/Types/Notepads/(Notepad) XXX [Topic Name].md

/* XXX is a 3-digit number. Get it with: flint helper type newnumber Notepad */

```markdown
---
id: [generate-uuid4]
tags:
  - "#ntpd/notepad"
status: [active|archived]
branches:
artifacts:
[agent]-sessions: 
template: "[[tmp-ntpd-notepad-v1.0]]"
---

# 1

[User writes topic/initial message here. Agent responds with callout below.]

>[!example] Agent Response
>[Agent responds in callout format]


# 2

[Conversation continues with # 2, # 3, etc.]
```

/* Notes:
   - branches: and artifacts: are appended to by [[sk-ntpd-branch]] and [[sk-ntpd-attach]]
   - Section headings (# 1, # 2, ...) are auto-incremented by the agent
   - Branch markers (# Branched: `[[link]]`) are inserted by [[sk-ntpd-branch]]
   - State transitions: active → archived (via [[wkfl-ntpd-finish]])
*/
