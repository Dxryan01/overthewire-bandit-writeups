**Bandit Level 13 → Level 14**

**Goal**: log in as `bandit14`, using a private SSH key found in `bandit13`'s home directory instead of a password.

**Reasoning**: `ls` on `bandit13` reveals `sshkey.private`, identified by `file` as an OpenSSH private key rather than plain text — this level swaps the usual password-based login for key-based authentication. The key needs to be copied out to the local machine first (using `scp`, "secure copy", which transfers files over an SSH connection) since SSH only authenticates using a local key file, not one sitting on the remote server, and SSH is strict about the permissions of private key files: if the key is readable by anyone other than its owner, it refuses to use it at all.

**Solution**:
1. Back on your local machine (exit the `bandit13` session first), copy the private key: `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ./sshkey14.private`
2. Try connecting as `bandit14` with the key (`-i` specifies which identity/key file to authenticate with): `ssh bandit14@bandit.labs.overthewire.org -p 2220 -i ./sshkey14.private` — this first attempt fails with `bad permissions`, since the copied file is readable by more than just its owner
3. Restrict the key's permissions to the owner only: `chmod 700 ./sshkey14.private`
4. Retry the same SSH command (`ssh bandit14@bandit.labs.overthewire.org -p 2220 -i ./sshkey14.private`) — this time it succeeds and logs in as `bandit14`
5. Once logged in, `bandit14`'s own password (for direct reconnection later, without needing the key again) can be retrieved with `cat /etc/bandit_pass/bandit14` — consistent with the pattern seen in earlier levels, where each account's password is stored in a file only that account can read

**Alternative**: `chmod 600 ./sshkey14.private` (more conventional for a private key file — read/write for the owner only, no execute bit needed; `700` also works since it removes access for group/others, but `600` is the standard permission for this kind of file) → `ssh bandit14@bandit.labs.overthewire.org -p 2220 -i ./sshkey14.private`

**Lesson**: SSH enforces strict permissions on private key files as a security measure — a key file that's group- or world-readable gets silently ignored rather than used, so `chmod` is a required step here, not an optional cleanup.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
