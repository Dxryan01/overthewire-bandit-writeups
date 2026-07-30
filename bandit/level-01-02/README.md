**Bandit Level 01 → Level 02**

**Goal**: find the password stored in a file called `-` in the home directory.

**Reasoning**: `cat -` on its own doesn't work as expected — the shell reads `-` as an option flag rather than a filename. The file still needs to be referenced by its literal name, so it has to be pointed to explicitly as a path.

**Solution**: `cat ./-`

**Lesson**: prefixing a dash-named file with `./` forces it to be read as a relative path instead of being misinterpreted as a command flag.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
