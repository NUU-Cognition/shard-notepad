# Notepad Shard

Document-based brainstorming with individual notepad files. Persistent, editable conversations that can be distilled into tasks, ideas, and memories.

## Install

```bash
flint shard add NUU-Cognition/shard-notepad
```

## Structure

```
shard.yaml                        # Manifest
init-ntpd.md                      # Init file — shard context
skills/
  sk-ntpd-respond.md              # Continue conversation
  sk-ntpd-branch.md               # Create a branch
  sk-ntpd-attach.md               # Create an artifact derivative
  sk-ntpd-cleanup.md              # Scan and tidy notepads
workflows/
  wkfl-ntpd-start.md              # Create new notepad
  wkfl-ntpd-continue.md           # Continue conversation across threads
  wkfl-ntpd-finish.md             # Archive and extract artifacts
templates/
  tmp-ntpd-notepad-v1.0.md        # Notepad file template
  tmp-ntpd-branch-v0.1.md         # Branch file template
```

## How It Works

1. Start a notepad with `wkfl-ntpd-start`
2. User writes, agent responds with `>[!example] Agent Response` callouts
3. When done, run `wkfl-ntpd-finish` to extract artifacts and archive

## Lifecycle

```
active → archived
```
