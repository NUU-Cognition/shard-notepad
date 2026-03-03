# Skill: Branch

Create a branch from the current notepad or branch.

# Input

- The notepad (or branch) to branch from
- Branch name (descriptive short name for the side-thread)
- Branch point (optional — defaults to current last section)

# Actions

1. Read the source notepad/branch
2. Determine the branch number:
   - Glob for existing branches of this notepad: `(Notepad) XXX Topic . (Branch) *.md`
   - Next number = count of existing top-level branches + 1
   - If branching from a branch (e.g. branch 1), the sub-branch number is `1.1`, `1.2`, etc.
3. Determine the branch point section number (last `# N` heading, or user-specified)
4. Create the branch file using [[tmp-ntpd-branch-v0.1]]:
   - Filename: `(Notepad) XXX Topic . (Branch) B [Branch Name].md`
   - Examples:
     - 1st branch: `... . (Branch) 1 Future Ideas.md`
     - 2nd branch: `... . (Branch) 2 Dashboard Rework.md`
     - Sub-branch of branch 1: `... . (Branch) 1.1 Deeper Dive.md`
   - Set frontmatter: `parent`
   - Add `# Branched from [[parent]]` heading (the agent reads the parent up to `branched-at` for context when working in the branch)
   - Add first branch section heading: `# N.B` (where N = branch point, B = branch number)
5. Insert branch marker in the source file at the branch point:
   ```
   # Branched: [[(Notepad) XXX Topic . (Branch) B [Branch Name]]]
   ```
6. **Main continues** — after the branch marker, add the next section heading (`# N+1`) so the main thread keeps flowing. The branch diverges, but the parent notepad doesn't stop.
7. Append the branch wikilink to the source file's `branches:` frontmatter list

# Branch Numbering

- 1st branch from main → `(Branch) 1 Name`
- 2nd branch from main → `(Branch) 2 Name`
- Sub-branch of branch 1 → `(Branch) 1.1 Name`
- Sub-branch of branch 1.1 → `(Branch) 1.1.1 Name`
- Each level uses dotted notation matching the parent branch number

# Section Numbering Rules

- 1st branch from main → `.1` suffix: `# 4.1`, `# 5.1`, `# 6.1`...
- 2nd branch from main → `.2` suffix: `# 4.2`, `# 5.2`...
- Branch from a `.1` branch → adds level: `# 4.1.1`, `# 5.1.1`...
- Each new branch at the same level gets the next index

# Output

- New branch file in `Mesh/Types/Notepads/`
- Branch marker inserted in source
- Branch link appended to source's `branches:` frontmatter
