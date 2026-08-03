**Bandit Level 22 → Level 23**

**Goal**: find `bandit23`'s password, leaked by a cron job into a file whose name is a computed MD5 hash rather than a fixed one.

**Reasoning**: like the previous level, a script runs periodically as `bandit23` and copies that account's password to `/tmp`. This time, though, the destination filename isn't fixed — it's built from `$(whoami)`, so the script computes a different hash depending on which account actually runs it. Running the script's commands manually while logged in as `bandit22` would compute the hash for `bandit22` instead (since `whoami` reflects whoever is currently executing it), not for `bandit23` — the account the cron job actually runs as. What's needed is to simulate what the script would compute *as if* it were running as `bandit23`, by manually substituting that name instead of relying on `whoami`.

**Solution**:
1. Read the cron entry and the script to understand the naming logic: `cat /etc/cron.d/cronjob_bandit23` → `cat /usr/bin/cronjob_bandit23.sh`
2. Reproduce the script's hash computation, substituting `bandit23` directly instead of using `whoami`: `echo I am user bandit23 | md5sum | cut -d ' ' -f 1`
3. Read the resulting file: `cat /tmp/<computed_hash>`

**Alternative**: `cat /tmp/$(echo I am user bandit23 | md5sum | cut -d ' ' -f 1)` (combines steps 2 and 3 into a single line — the `$(...)` substitution computes the hash inline and feeds it directly as the filename to `cat`, instead of storing it in an intermediate variable first)

**Lesson**: a script that uses `whoami` to build a path behaves differently depending on who runs it — reading such a script only tells you the *logic*, not the actual value it produces; the value still has to be computed for the *specific account the script actually runs as*, not the account inspecting it.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
