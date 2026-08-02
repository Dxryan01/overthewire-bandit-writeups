**Bandit Level 19 → Level 20**

**Goal**: find `bandit20`'s password, using a provided binary (`bandit20-do`) that runs commands as another user.

**Reasoning**: reading `/etc/bandit_pass/bandit20` directly (`cat /etc/bandit_pass/bandit20`) fails with a permission error when run as `bandit19` — that file is only readable by `bandit20` itself, the same pattern seen with every account's password file so far. What's different here is `bandit20-do`, a **setuid** binary: a program that, when executed, runs with the permissions of the user who *owns* the file (here, `bandit20`) rather than the permissions of whoever launched it. Running it without arguments (`./bandit20-do`) shows it expects a command to execute — it responds with `Run a command as another user. Example: ./bandit20-do whoami` — one that then runs as `bandit20`, regardless of who called `bandit20-do`.

**Solution**: `./bandit20-do whoami` (confirms the command runs as `bandit20`, not `bandit19`) → `./bandit20-do cat /etc/bandit_pass/bandit20`

**Lesson**: a setuid binary is what makes it possible for a lower-privileged user to perform a specific, controlled action as a different (often higher-privileged) user — the permission boundary is enforced by which command the binary allows, not by who is running it.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
