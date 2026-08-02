**Bandit Level 21 → Level 22**

**Goal**: find `bandit22`'s password, leaked by a scheduled task (cron job) running as that user.

**Reasoning**: `cron` is a background daemon that runs scheduled tasks automatically, independent of any user action — entries in `/etc/cron.d/` are just pointers describing *when* something runs and, crucially, *as which user*, not the actual code being executed. A cron entry running as `bandit22` means whatever script it points to runs with `bandit22`'s privileges, regardless of who inspects the cron configuration itself — the same idea as the setuid binary from the previous level, but driven by the cron daemon instead of the setuid bit. That makes the script worth inspecting specifically: it can access things `bandit21` normally can't, and if it writes anything out carelessly, that's a potential leak.

**Solution**:
1. List scheduled jobs to find one relevant to the target account: `ls /etc/cron.d/` → `cronjob_bandit22`
2. Read the cron entry to see what it runs and as whom: `cat /etc/cron.d/cronjob_bandit22` → points to `/usr/bin/cronjob_bandit22.sh`, run as `bandit22`
3. Read the actual script being run: `cat /usr/bin/cronjob_bandit22.sh` — it copies `bandit22`'s password into a file in `/tmp`, then makes that file world-readable (`chmod 644`)
4. Read the leaked file directly: `cat /tmp/<leaked_filename>`

**Lesson**: a cron job's real risk isn't the schedule itself, but what the script it points to does *with the privileges of the account it runs as* — here, a script running as `bandit22` writes that account's password to a location it then makes readable by everyone.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
