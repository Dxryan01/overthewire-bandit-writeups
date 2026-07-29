**Bandit Level 00**

**Goal**: log into the Bandit server for the first time via SSH.

**Reasoning**: the intro page gives host, port, username and password directly — nothing to figure out yet, just applying the right SSH syntax with a non-default port.

**Solution**: `ssh bandit0@bandit.labs.overthewire.org -p 2220`

**Alternative**: `ssh -l bandit0 bandit.labs.overthewire.org -p 2220` (same result, username passed via `-l` instead of `user@host` syntax)

**Lesson**: don't forget `-p` when a server doesn't run SSH on the default port 22 — easy to overlook if you're used to default setups.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)


