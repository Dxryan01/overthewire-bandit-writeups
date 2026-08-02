**Bandit Level 16 → Level 17**

**Goal**: find, among the ports in the 31000–32000 range on localhost, the one that both is active and uses SSL/TLS, then submit `bandit16`'s password there to receive a private SSH key for `bandit17`.

**Reasoning**: with a whole port range to check instead of one known port, `nmap` is the right tool to scan for what's actually listening rather than testing each port by hand. The scan turned up five open ports, three plain `echo` services and two SSL-wrapped ones — `echo` services just reflect back whatever is sent, so they're not relevant here. Of the two SSL ports, one was fingerprinted as `ssl/echo` (same irrelevant behavior, just wrapped in SSL), while the other returned data `nmap` couldn't recognize as a known service — a strong sign that it's the custom one built for this level. Connecting to it with `openssl s_client` and submitting the current password confirms it, replying with a private key for the next level instead of just a plain password.

**Solution**:
1. Scan the port range for active, version-identified services: `nmap -sV -n -p 31000-32000 localhost`
2. Connect to the SSL port that returned unrecognized data (as opposed to the other SSL port, fingerprinted as a plain echo service): `openssl s_client -connect localhost:31790 -quiet`
3. Submit `bandit16`'s password — the service replies with `Correct!` followed by a full private SSH key
4. Copy the entire key output, including the `-----BEGIN OPENSSH PRIVATE KEY-----` and `-----END OPENSSH PRIVATE KEY-----` lines
5. Exit back to the local machine's terminal: `exit`
6. Create a local file and paste the copied key into it, e.g. with `nano sshkey17.private`, then save
7. Restrict the file's permissions, since SSH requires this for private keys: `chmod 600 sshkey17.private`
8. Log in as `bandit17` using the key: `ssh bandit17@bandit.labs.overthewire.org -p 2220 -i sshkey17.private`
9. Once logged in, `bandit17`'s own password (for direct reconnection later, without needing the key again) can be retrieved with `cat /etc/bandit_pass/bandit17` — same pattern as with `bandit14`

**Lesson**: `nmap -sV` doesn't just say a port is open — it tries to identify the service running on it, and a result it can't recognize is itself a useful clue when several ports look superficially similar (here, two SSL ports, only one of which is actually part of the challenge).

---
🔒 Password/key not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
