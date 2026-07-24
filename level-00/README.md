**Bandit Level 00 → Level 01**

**Key Takeaway**: connecting to a remote server via SSH, specifying a non-default port.

**Command**: `ssh bandit0@bandit.labs.overthewire.org -p 2220`

**Alternatives**: `ssh -l bandit0 bandit.labs.overthewire.org -p 2220` (same result, username passed via `-l` instead of `user@host` syntax)

**File**: none — credentials for this first level are given directly on the game's intro page

**Note**: most SSH connections I'd done before were on default setups (no port specified). Worth remembering that `-p` is needed whenever the server doesn't use port 22.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
