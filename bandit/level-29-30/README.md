**Bandit Level 29 → Level 30**

**Goal**: find `bandit30`'s password, which turns out not to be on the repository's main branch at all.

**Reasoning**: the same approach as the previous level — checking the current README, then comparing commits with `git diff` — only reveals a placeholder password (`<no passwords in production!>`) and a username change, a dead end. Git repositories aren't limited to a single line of history, though: branches let separate lines of work exist in parallel, isolated from the main one until merged. Since both obvious angles (current content, commit history on the current branch) were exhausted, checking what other branches exist is the natural next thing to rule in or out — and branch names like `dev` are a common place for content not meant for the "production" branch.

**Solution**:
1. Confirm the current branch's history doesn't contain a real password: `git log` → `git diff <commit1> <commit2>`
2. List all branches, including remote ones: `git branch -a` → reveals `dev` and `sploits-dev` alongside `master`
3. Switch to the `dev` branch: `git checkout dev`
4. Read the README there: `cat README.md` — this time it holds the real password

**Lesson**: exhausting the "obvious" places to look (current file, commit history on the checked-out branch) doesn't mean a Git repository has nothing left to reveal — checking for other branches is a basic but easy-to-forget step when investigating a repo's full content.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
