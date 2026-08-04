**Bandit Level 28 → Level 29**

**Goal**: find `bandit29`'s password, hidden by a later commit in a Git repository whose current README shows it masked out.

**Reasoning**: the current `README.md` only reflects the repository's latest state — Git keeps the full history of every previous version of a file, regardless of what a later commit changed or removed. `git log` shows three commits: an initial one, one titled "add missing data", and a final one titled "fix info leak" — a strong hint that a real value was accidentally committed at some point, then masked afterwards, without erasing it from history. Comparing the diffs between successive commits confirms this exactly: the password appears in cleartext between the first and second commit, then gets replaced with `xxxxxxxxxx` between the second and third.

**Solution**: `git log` (note the commit hashes shown for the "initial commit" and "add missing data" entries) → `git diff <initial_commit_hash> <"add missing data"_commit_hash>` (replacing each placeholder with the actual hash string from `git log`'s output)

**Lesson**: masking or removing a value in a new commit doesn't erase it from the repository — the old version is still fully readable through the commit history, unless that history itself is deliberately rewritten (e.g. with `git filter-repo`, as done earlier in this very repo's own README cleanup).

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
