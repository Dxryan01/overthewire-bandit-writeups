**Bandit Level 18 → Level 19**

**Goal**: find the password stored in a `readme` file in the home directory, despite normal interactive login being disabled.

**Reasoning**: a regular SSH login drops straight into a shell that's set up to log you out immediately (a modified `.bashrc`), making a normal interactive session unusable for browsing files. SSH doesn't require dropping into a shell first, though — it can run a single command remotely and return its output directly, bypassing whatever runs on interactive login entirely.

**Solution**: `ssh bandit18@bandit.labs.overthewire.org -p 2220 "ls"` → `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`

**Lesson**: SSH can execute a single remote command non-interactively by passing it as an argument, without ever opening a full interactive shell — a useful way around restrictions that only kick in on interactive login.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
