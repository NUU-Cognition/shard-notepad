# 0.3.0

- The workflow Start Notepad has an invocation file of the format `shard-invocation/0.2` (NUU Orbh Task 744). `flint shard invoke ntpd start --input topic="<topic>"` starts one. The steps are `create`, `gather`, `converse` (it repeats for each turn), and `finish`. The output is `notepad`.
- The `converse` step calls the Projects shard: work that a turn asks for runs as a child invocation (`flint shard invoke proj create_and_do_task`).
- Start Notepad has a new Stage 4: Finish, which runs `wkfl-ntpd-finish`.
- The behaviour `notepad-open-hint` says before a session close that the notepad is still open.
- This version needs a Flint CLI with shard invocations 0.2 (NUU Orbh Task 744).

# 0.2.4

- The dependency on the Flint shard accepts any version (`"@nuucognition/flint": ""`), so the shard works with Flint 0.3.x and with Flint 0.4.0 (NUU Flint Task 1129).

# 0.1.0

- Initial shard scaffold
