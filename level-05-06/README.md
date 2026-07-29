**Bandit Level 05 → Level 06**

**Goal**: find the password stored in a file somewhere under the `inhere` directory, described as human-readable, exactly 1033 bytes in size, and non-executable.

**Reasoning**: `inhere` contains 20 subdirectories (`maybehere00` to `maybehere19`), each with several files — too many to check by hand. Since the target file has known, specific properties (type, size, non-executable), `find` can search recursively and filter on those criteria at once instead of opening each candidate manually. The "human-readable" property wasn't filtered by `find` itself — it was confirmed afterwards, simply by running `cat` on the single match the other three criteria narrowed it down to.

**Solution**: `find . -type f -size 1033c -not -executable` → `cat ./maybehere07/.file2`

**Alternative**: `find . -type f -size 1033c ! -executable` → `cat ./maybehere07/.file2` (same result, using `!` as shorthand for `-not` — note that in some shells `!` needs to be escaped as `\!` since it has a special meaning to bash)

**Lesson**: when a file is buried among many similar-looking candidates, combining several `find` criteria (type, size, permissions) at once narrows down the search far faster than checking each one by hand.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
