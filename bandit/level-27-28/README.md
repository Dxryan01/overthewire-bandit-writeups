**Bandit Level 27 → Level 28**

**Goal**: find the password stored in a `README` file inside a Git repository hosted on the server, accessible via `bandit27-git`.

**Reasoning**: cloning over SSH with a non-default port needs the port specified inside the URL itself — `git clone` doesn't accept a separate `-p`/`-P` flag the way `ssh` or `scp` do. The port goes right after the hostname, before the first `/` of the path.

**Solution**: `git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo` → `cat repo/README`

**Lesson**: SSH-based tools aren't all consistent in how they take a custom port — `ssh`/`scp` use a `-p`/`-P` flag, while a `ssh://` URL (as used by `git clone`) embeds the port directly after the hostname with a `:`.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
