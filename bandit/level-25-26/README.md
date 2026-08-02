**Bandit Level 25 → Level 26**

**Goal**: log in as `bandit26` using the private key found in the previous level, despite the connection closing immediately after login.

**Reasoning**: `bandit26`'s login shell isn't a regular interactive shell — it's configured to run a pager (`more`) on a text file, then the session closes as soon as that pager finishes. With a wide terminal window, the whole file displays at once and the session ends immediately, leaving no time to act. Shrinking the terminal window forces `more` to stop mid-way (showing a `--More--` prompt waiting for input), creating a window of opportunity before it finishes and the connection drops. From there, since `more` didn't accept the usual `!command` shell escape, an alternative route was needed: pressing `v` opens the currently displayed file in an editor (`vi` by default) — and `vi` itself supports launching a real shell from inside it via `:shell`.

**Solution**:
1. Copy the private key from `bandit25` to the local machine: `scp -P 2220 bandit25@bandit.labs.overthewire.org:bandit26.sshkey ./bandit26.sshkey`
2. Shrink the terminal window (few visible lines) before connecting, so the pager doesn't display everything at once
3. Log in as `bandit26` with the key: `ssh bandit26@bandit.labs.overthewire.org -p 2220 -i ./bandit26.sshkey` — the session drops into the `more` pager and stops at a `--More--` prompt
4. While at that prompt, press `v` to open the file in `vi`
5. Inside `vi`, force it to use a real shell and launch it: `:set shell=/bin/bash` then `:shell` — this drops into a real shell as `bandit26` (`bandit26@bandit:~$`), from which the password can finally be read: `cat /etc/bandit_pass/bandit26`

**Lesson**: when direct shell access is restricted, secondary features of allowed programs (a pager's "open in editor" key, an editor's own shell-escape command) can still provide a way out — this kind of restricted-shell escape is a well-known, documented pattern in security/CTF contexts (referenced on sites like GTFOBins), not something to reinvent from scratch each time.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
