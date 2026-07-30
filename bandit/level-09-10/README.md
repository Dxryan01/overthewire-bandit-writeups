**Bandit Level 09 → Level 10**

**Goal**: find the password stored in `data.txt`, described as one of the few human-readable strings in the file, preceded by several `=` characters.

**Reasoning**: `data.txt` this time isn't purely plain text — it contains a mix of binary data and a few readable strings mixed in, so a plain `cat` or `grep` on raw content wouldn't reliably isolate the human-readable parts. `strings` extracts only the printable text sequences from a file, binary or not, and combining it with `grep` for the known `===` marker narrows it down to the exact line needed.

**Solution**: `strings data.txt | grep '==='`

**Lesson**: when a file mixes binary and readable content, `strings` is the tool to pull out just the human-readable text — `cat` or `grep` alone on the raw file wouldn't filter out the binary noise first.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
