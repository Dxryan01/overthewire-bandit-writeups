**Bandit Level 08 → Level 09**

**Goal**: find the password stored in `data.txt`, on the one line that appears exactly once — every other line appears multiple times.

**Reasoning**: `wc -l data.txt` confirmed the file has 1001 lines, too many to compare by eye for duplicates. Sorting the file groups identical lines next to each other, and `uniq -u` then keeps only the lines that have no adjacent duplicate — exactly the "appears once" property being searched for.

**Solution**: `sort data.txt | uniq -u`

**Lesson**: `uniq` only detects duplicates that are directly adjacent, which is why sorting first is essential — without it, two identical lines far apart in the file wouldn't be recognized as duplicates.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
