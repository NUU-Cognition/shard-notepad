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
workflows/
  wkfl-ntpd-start.md              # Create new notepad
  wkfl-ntpd-finish.md             # Archive and extract artifacts
templates/
  tmp-ntpd-notepad.md             # Notepad file template
```

## How It Works

1. Start a notepad with `wkfl-ntpd-start`
2. User writes, agent responds with `>[!example] Agent Response` callouts
3. When done, run `wkfl-ntpd-finish` to extract artifacts and archive

## Lifecycle

```
active → archived
```
