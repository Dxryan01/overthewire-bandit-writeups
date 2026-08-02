**Bandit Level 26 → Level 27**

**Goal**: find `bandit27`'s password, from a real shell as `bandit26`.

**Reasoning**: same setuid pattern already seen with `bandit20-do` — a binary owned by the target account that runs whatever command is passed to it with that account's privileges, regardless of who calls it.

**Solution**: `ls` (reveals `bandit27-do` in `bandit26`'s home directory, from the shell obtained in the previous level) → `./bandit27-do cat /etc/bandit_pass/bandit27`

**Lesson**: this setuid pattern keeps reappearing across levels — once recognized, an unfamiliar executable sitting in a home directory is worth checking with `ls`/`file` as a likely candidate for the same trick.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
