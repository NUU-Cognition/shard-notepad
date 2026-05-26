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

const notepads = dv.pages('#ntpd/notepad');

// Active Notepads (Mesh/Types/Notepads/)
dv.header(1, "Active");
const active = notepads.where(p => p.status === 'active' && p.file.path.startsWith('Mesh/Types/Notepads/'))
  .array().sort((a, b) => b.file.name.localeCompare(a.file.name));
if (active.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Notepad", "Artifacts"],
    active.map(p => [
      dv.fileLink(p.file.path, false, formatName(p)),
      p["artifacts-created"] ? (Array.isArray(p["artifacts-created"]) ? p["artifacts-created"].join(", ") : p["artifacts-created"]) : "—"
    ])
  );
}

// Archived Notepads (Mesh/Archive/Notepads/)
dv.header(1, "Archived");
const archived = notepads.where(p => p.status === 'archived' || p.file.path.startsWith('Mesh/Archive/Notepads/'))
  .array().sort((a, b) => b.file.name.localeCompare(a.file.name));
if (archived.length === 0) {
  dv.paragraph("*None*");
} else {
  dv.table(["Notepad", "Artifacts"],
    archived.map(p => [
      dv.fileLink(p.file.path, false, formatName(p)),
      p["artifacts-created"] ? (Array.isArray(p["artifacts-created"]) ? p["artifacts-created"].join(", ") : p["artifacts-created"]) : "—"
    ])
  );
}
```
