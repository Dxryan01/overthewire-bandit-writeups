**Bandit Level 01 → Level 02**

**Goal**: find the password for the next level, stored somewhere in the home directory.

**Reasoning**: `ls` right after login is the natural first move to see what's there — it showed a plain file called `readme`, an obvious place to check first.

**Solution**: `cat readme`

**Lesson**: starting each level with `whoami`, `pwd`, and `ls` is a good habit to orient yourself before deciding what to do next.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
