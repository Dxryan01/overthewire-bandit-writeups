**Bandit Level 02 → Level 03**

**Goal**: find the password stored in a file whose name contains spaces and starts/ends with double dashes, in the home directory.

**Reasoning**: two problems combine here. Spaces in the filename break the usual `cat filename` syntax, since the shell treats each space as a separator between arguments — the name needs to be quoted or escaped. On top of that, the name starts with `--`, which gets misread as the start of a command option rather than part of a filename — same issue as the previous level, solved by prefixing with `./`.

**Solution**: `cat ./'--spaces in this filename--'`

**Alternative**: `cat ./"--spaces in this filename--"` (double quotes work the same way here)

**Lesson**: when a filename combines multiple "shell traps" (leading dashes AND spaces), the fixes stack — `./` to neutralize the dashes, quotes to handle the spaces. Quoting alone or `./` alone isn't enough on its own here.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
