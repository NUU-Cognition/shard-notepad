# Filename: Mesh/Types/Notepads/(Notepad) XXX [Topic Name] . (Branch) B [Branch Name].md

/* B is the branch number: 1, 2, 3 for top-level; 1.1, 1.2 for sub-branches */
/* Created by sk-ntpd-branch. Branch references parent — does NOT copy content. */

```markdown
---
id: [generate-uuid]
tags:
  - "#ntpd/notepad"
  - "#ntpd/branch"
status: [active|archived]
parent: "[[parent notepad link]]"
branches:
artifacts:
[agent]-sessions:
template: "[[tmp-ntpd-branch-v0.1]]"
---

# Branched from [[parent notepad]]

# N.B

[Conversation continues with dotted section numbering]

>[!example] Agent Response
>[Agent responds in callout format]


[Continues with # N+1.B, # N+2.B, etc.]
```

/* Notes:
   - Branch references parent via `parent` field — agent reads parent for context
   - Branch number in filename: 1, 2, 1.1, 1.2, etc.
   - Section numbering uses dotted format: N.B
   - branches: and artifacts: appended to if this branch gets sub-branched or artifacts attached
   - On finish, branch content is flattened back into parent's Session Output
*/
