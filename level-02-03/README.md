**Bandit Level 02 → Level 03**

**Goal**: find the password stored in a file whose name contains spaces, in the home directory.

**Reasoning**: a filename with spaces breaks the usual `cat filename` syntax, since the shell treats each space as a separator between arguments. The whole name needs to be treated as a single argument, either by quoting it or escaping each space individually.

**Solution**: `cat "spaces in this filename"`

**Alternative** : `cat spaces\ in\ this\ filename` (escaping each space individually instead of quoting the whole name)

**Lesson**: quoting the full filename is cleaner than escaping every space one by one, espacially as filenames get longer.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
