**Bandit Level 17 → Level 18**

**Goal**: find the password, which is the one line that changed between `passwords.old` and `passwords.new`.

**Reasoning**: `wc -l passwords.new && wc -l passwords.old` confirms both files are large lists of similar-looking strings, with only a single line differing between them — comparing them by eye would be slow and error-prone. `diff` is built exactly for this: it compares two files line by line and reports only what changed, ignoring everything identical.

**Solution**: `diff passwords.new passwords.old`

`diff` marks the differing line from the first file with `<` and the one from the second file with `>` — so with this argument order, the password (the new value) is the line starting with `<`. Running it the other way around (`diff passwords.old passwords.new`) would still work, but the password would then be the line starting with `>` instead, since the file order — and therefore which symbol points to `passwords.new` — is reversed.

**Lesson**: when two versions of a file need to be compared, `diff` isolates the actual differences instead of requiring a manual line-by-line read-through.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
