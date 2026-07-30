**Bandit Level 11 → Level 12**

**Goal**: find the password stored in `data.txt`, where every lowercase and uppercase letter has been rotated by 13 positions (ROT13).

**Reasoning**: ROT13 is a simple substitution cipher — each letter is shifted 13 places through the alphabet, wrapping back to the start after Z. Since applying the same rotation a second time cancels the first (13 + 13 = 26, a full cycle), the same shift used to encode the text also decodes it.

**Solution**: `cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'`

**Lesson**: `tr` maps each character in the first set to the character at the same position in the second set — writing out the alphabet shifted by 13 (`n-za-m` for lowercase, `N-ZA-M` for uppercase) reproduces ROT13 without needing a dedicated tool.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
