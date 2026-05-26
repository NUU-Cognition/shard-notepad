# Notepad Shard

Document-based brainstorming with individual notepad files. Persistent, editable conversations with forking, inline editing, and action execution.

## Install

```bash
flint shard install NUU-Cognition/shard-notepad
```

## Structure

```
shard.yaml                        # Manifest
init-ntpd.md                      # Init file — shard context
skills/
  sk-ntpd-respond.md              # Continue conversation (new turn, inline edit, action)
  sk-ntpd-fork.md                 # Fork notepad into a new standalone notepad
  sk-ntpd-attach.md               # Create an artifact derivative
  sk-ntpd-cleanup.md              # Scan and tidy notepads
workflows/
  wkfl-ntpd-start.md              # Create new notepad
  wkfl-ntpd-continue.md           # Continue conversation
  wkfl-ntpd-finish.md             # Archive and extract artifacts
templates/
  tmp-ntpd-notepad-v1.0.md        # Notepad file template
```

## How It Works

1. Start a notepad with `dev-wkfl-ntpd-start`
2. User writes, agent responds with `>[!example] Agent Response` callouts
3. Write between a response and the next heading to trigger an inline edit
4. Fork with `dev-sk-ntpd-fork` to explore a tangent in a separate notepad
5. When done, run `dev-wkfl-ntpd-finish` to extract artifacts and archive

## Lifecycle

```
active → archived
```
