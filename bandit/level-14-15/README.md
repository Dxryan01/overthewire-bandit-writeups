**Bandit Level 14 → Level 15**

**Goal**: submit `bandit14`'s own password to port 30000 on localhost to receive the password for `bandit15`.

**Reasoning**: this level isn't about finding a hidden file — the password is already known (retrieved from `/etc/bandit_pass/bandit14`, as covered in the previous level). The task here is submitting it to a listening service on a specific local port. `nc` (netcat) opens a raw connection to a host and port, letting text be sent and received directly — exactly what's needed to talk to a service without a dedicated client for it.

**Solution**: `nc localhost 30000`, then paste `bandit14`'s password and press Enter — the service responds with `Correct!` followed by `bandit15`'s password

**Alternative**: `nc 127.0.0.1 30000` (same result — `127.0.0.1` is the explicit loopback IP address that `localhost` resolves to)

**Lesson**: `nc` is a generic way to interact with any text-based network service by hand — useful whenever there's no specific client for a custom port, just plain text exchanged over a connection.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
