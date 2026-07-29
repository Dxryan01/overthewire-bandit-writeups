**Bandit Level 04 → Level 05**

**Goal**: find the password stored in the one human-readable file among several in the `inhere` directory.

**Reasoning**: `ls` shows several files with similar dash-prefixed names, so filenames alone don't reveal which one is readable text — the content type needs to be checked directly. `file` inspects the actual content of each file rather than relying on its name, making it possible to spot the one with plain ASCII text among files that might be binary, images, or something else entirely.

**Solution**: `file ./*` → `cat ./-file07`

**Alternative**: `for f in ./*; do file "$f"; done` (same result as `file ./*`, but processes files one by one instead of passing them all as a single argument list — useful if you needed to act differently per file)  → `cat ./-file07`

**Lesson**: don't assume a file's content type from its name — `file ./*` is a quick way to check every file in a directory at once when several candidates look alike.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
