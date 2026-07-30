**Bandit Level 07 → Level 08**

**Goal**: find the password stored in `data.txt`, located right next to the word "millionth" among a large amount of text.

**Reasoning**: `data.txt` turned out to be a large text file — `wc -l data.txt` confirmed it, counting close to 100,000 lines, far too long to scroll through manually. Since the password sits next to a known, distinctive word, searching for that word directly is much faster than reading the whole file.

**Solution**: `cat data.txt | grep 'millionth'`

**Alternative**: `grep 'millionth' data.txt` (same result, without the unnecessary `cat` — `grep` can read the file directly, no need to pipe its content through `cat` first)

**Lesson**: when a huge text file needs to be searched for one specific, known keyword, `grep` finds the relevant line instantly instead of opening or scrolling through the whole file.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
