**Bandit Level 30 → Level 31**

**Goal**: find `bandit31`'s password, hidden somewhere in a Git repository that has almost nothing going for it at first glance — a single commit, a placeholder README, and only one branch.

**Reasoning**: the usual checks come up empty one after another: the README itself is just a joke placeholder, `git log` shows a single commit with nothing to compare against, and `git branch -a` reveals only `master` — no alternate branch to switch to this time. Branches aren't the only way Git can point to a commit, though: **tags** are another kind of reference, often used to mark specific points in history, and they don't have to be reachable through any branch's normal history at all. `git show-ref` lists every reference the repository knows about — branches, remotes, *and* tags — together with the commit hash each one points to, making it possible to spot a tag pointing somewhere unexpected.

**Solution**:
1. Clone the repo and inspect the obvious places first: `git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo` → `ls` → `cd repo` → `cat README.md` → `git log` → `git branch -a` (all dead ends)
2. List every reference in the repository, not just branches: `git show-ref` — reveals a tag named `secret`, pointing to a commit hash different from the one `master` points to
3. Inspect that specific commit directly: `git show <secret_tag_commit_hash>`

**Alternative**: `git tag` (lists just the tag name, `secret`) → `git show secret` (Git accepts the tag name directly, no need to look up its commit hash first)

**Lesson**: tags are a Git reference type separate from branches, and a repository can hold a tag pointing to a commit that's otherwise invisible from `git log`/`git branch` alone — `git show-ref` (or `git tag`) is what surfaces them.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
