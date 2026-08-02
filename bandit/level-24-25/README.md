**Bandit Level 24 → Level 25**

**Goal**: submit `bandit24`'s password together with a secret 4-digit PIN to a local port — the PIN isn't known in advance, so all 10000 possible combinations (`0000` to `9999`) need to be tried.

**Reasoning**: with 10000 combinations to test, doing this by hand is out of the question — a script is needed to generate every combination and submit each one automatically. A first attempt, testing combinations one at a time in a simple sequential loop, technically works but is far too slow (roughly 1000+ combinations per 15–20 minutes) to realistically get through all 10000:
```bash
for pin in $(seq -w 0000 9999); do
    echo "<bandit24_password> ${pin}" | nc localhost 30002 -w 1 >> /tmp/dir/results.txt
done
```
Running several submissions in parallel instead of one-by-one cuts that time down dramatically, since each individual connection no longer has to finish before the next one starts.

**Solution**:
1. Generate every 4-digit combination, zero-padded: `seq -w 0000 9999`
2. Feed that list into `xargs`, running several submissions in parallel, each in its own `bash -c` (needed because the actual submission itself involves a pipe, which `xargs` can't express directly):
   ```bash
   seq -w 0000 9999 | xargs -P 5 -I{} bash -c 'echo "<bandit24_password> {}" | nc localhost 30002 -w 1 >> /tmp/dir/results.txt'
   ```
3. While it runs, monitor progress from a second terminal without interrupting the first: `watch -n 2 wc -l /tmp/dir/results.txt` (each attempt writes 2 lines, so line count ÷ 2 ≈ combinations tried so far)
4. Once done, filter out the repeated failure messages to isolate the successful response: `grep -E -v "Wrong|I am the" /tmp/dir/results.txt`

   **Alternative**: `grep -A 2 "Correct" /tmp/dir/results.txt` (searches for the line containing "Correct" and also shows the 2 lines right after it, where the next password appears — a more intuitive way to spot the result without needing to exclude the failure messages explicitly; note that `grep` always needs a search pattern as an argument, not just a filename)

**Lesson**: pushing too many simultaneous connections at once (a first attempt used 50 in parallel) got the whole SSH session disconnected by the server's own anti-abuse protection — a much lower degree of parallelism (around 5) is safer on a shared training server like this one, even though it means accepting a longer runtime as a trade-off.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
