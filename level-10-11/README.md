**Bandit Level 10 → Level 11**

**Goal**: find the password stored in `data.txt`, which contains Base64-encoded data.

**Reasoning**: `cat data.txt` shows a single line of readable-looking but meaningless text, which is the sign of an encoded string rather than plain content. Base64 is recognizable by its alphabet (letters, digits, `+`, `/`) and especially by the `=` padding characters often found at the end of the string — a strong signal pointing to this specific encoding rather than something else. Decoding it back is the direct way to recover the original text.

**Solution**: `cat data.txt | base64 -d`

**Alternative**: `base64 -d data.txt` (same result, without the unnecessary cat — base64 can read the file directly, no need to pipe its content through cat first)

**Lesson**: Base64-encoded text is easy to spot: it only uses letters, digits, `+`, `/`, and padding `=` characters at the end, with no natural spacing or punctuation.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
