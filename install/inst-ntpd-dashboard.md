---
id: 5b0ecac0-a83d-430e-a42d-62c43b97b01c
tags:
  - "#dashboard"
  - "#ntpd/dashboard"
  - "#managed/shard/ntpd"
  - "#read-only"
---

```dataviewjs
function formatName(p) {
  return p.file.name.replace(/^\(Notepad\)\s*/, '');
}

// Only look in Mesh/Types/Notepads/ — exclude branches and artifacts (derivatives)
const notepads = dv.pages('#ntpd/notepad').where(p => p.file.path.startsWith('Mesh/Types/Notepads/') && !p.file.name.includes(' . '));

// Active Notepads
dv.header(1, "Active");
const active = notepads.where(p => p.status === 'active')
  .array().sort((a, b) => b.file.name.localeCompare(a.file.name));
if (active.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Notepad"],
    active.map(p => [
      dv.fileLink(p.file.path, false, formatName(p))
    ])
  );
}

// Archived Notepads
dv.header(1, "Archived");
const archived = notepads.where(p => p.status === 'archived')
  .array().sort((a, b) => b.file.name.localeCompare(a.file.name));
if (archived.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Notepad"],
    archived.map(p => [
      dv.fileLink(p.file.path, false, formatName(p))
    ])
  );
}
```
