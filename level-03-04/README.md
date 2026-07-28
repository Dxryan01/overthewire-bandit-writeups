**Bandit Level 03 → Level 04**

**Goal**: find the password stored in a hidden file inside the `inhere` directory.

**Reasoning**: `ls` in the home directory shows a directory called `inhere`, but a plain `ls` inside it comes up empty — a sign the file(s) in there are hidden (dotfiles), since `ls` doesn't show hidden files by default. `ls -la` reveals hidden entries, including the one holding the password.

**Solution**: `ls -la` (inside `inhere`) → `cat ./'FILENAME_HERE'`

**Lesson**: an "empty-looking" directory is a common signal to check for hidden files with `ls -la` before assuming there's nothing there.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
