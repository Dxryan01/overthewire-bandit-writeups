**Bandit Level 31 → Level 32**

**Goal**: push a specific file (`key.txt`, with an exact content) to the repository's `master` branch, as instructed by the README.

**Reasoning**: the task itself is simple — create the file with the exact content requested, then commit and push it. The one obstacle is that the repository has a `.gitignore` rule blocking this filename, so a normal `git add` silently refuses to stage it. Since the file needs to be added anyway, that block has to be overridden explicitly rather than worked around.

**Solution**:
1. Clone the repo and navigate into it: `git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo` → `cd repo`
2. Create the file with the exact required content: `echo 'May I come in?' > key.txt`
3. Force-add it despite `.gitignore` blocking it: `git add -f key.txt`
4. Commit: `git commit -m "Add key.txt file"`
5. Push: `git push origin master` — the server's pre-receive hook validates the pushed content and prints the password for the next level directly in its response, even though it then rejects the push itself (`pre-receive hook declined`)

**Lesson**: `git add` silently skips files matched by `.gitignore` by default — `-f` (force) is needed to stage them anyway when that's genuinely intended, rather than assuming the file failed to be created.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
