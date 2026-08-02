**Bandit Level 23 → Level 24**

**Goal**: find `bandit24`'s password, using a cron job that automatically executes — and then deletes — any script owned by `bandit23` dropped into a specific "spool" directory.

**Reasoning**: `cronjob_bandit24.sh` runs every minute as `bandit24`, scanning `/var/spool/bandit24/foo/` and executing any file it finds that's owned by `bandit23`, before deleting everything in that directory regardless. That directory can be written into but not listed (`ls` fails with "Permission denied" there, since `bandit23` has execute/write access but not read access on it) — files can be dropped in blind, but not directly verified by browsing. Since any file left there gets wiped within a minute either way, the approach isn't to inspect a dropped file afterwards, but to make the script itself perform a useful action *while* it's briefly executed as `bandit24` — namely, writing that account's password somewhere `bandit23` can read.

**Solution**:
1. Create a working directory to prepare the script safely: `mkdir /tmp/dir && cd /tmp/dir`
2. Create the script, having it write `bandit24`'s password into a file in that same working directory:
   ```bash
   echo '#!/bin/bash
   cat /etc/bandit_pass/bandit24 > /tmp/dir/flag.txt' > script.sh
   ```
   (the string stays open across a real line break inside the single quotes — not a literal `\n`, which plain `echo` wouldn't interpret as a newline)
3. Make sure the script and its output file are executable/writable by anyone, since it will run as `bandit24` rather than `bandit23`: `for i in *; do chmod 777 "$i"; done`
4. Copy the script into the cron-watched directory: `cp script.sh /var/spool/bandit24/foo/script.sh`
5. Wait for the next cron run (up to a minute), then read the result: `cat /tmp/dir/flag.txt`

**Lesson**: when the destination the cron job writes into is owned by a different user than the one who set it up, permissions need to be opened up in advance (`chmod 777` here) — otherwise the script, running as `bandit24`, wouldn't be able to write into a file owned by `bandit23`.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
