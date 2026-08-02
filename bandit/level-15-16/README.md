**Bandit Level 15 → Level 16**

**Goal**: submit `bandit15`'s password to port 30001 on localhost, this time over an encrypted connection instead of plain text.

**Reasoning**: plain `nc`, as used in the previous level, sends everything unencrypted — this port instead expects an SSL/TLS-wrapped connection, so a tool that can negotiate that handshake is needed instead of raw netcat. `openssl s_client` acts as an SSL/TLS client, connecting to a server and setting up the encrypted channel before any data is exchanged.

**Solution**: `openssl s_client -connect localhost:30001`, then paste `bandit15`'s password and press Enter — after the certificate/handshake details print out, the service responds with `Correct!` followed by `bandit16`'s password

**Alternative**: `openssl s_client -connect localhost:30001 -quiet` (same result, but suppresses the certificate chain and handshake details, showing only the actual data exchanged)

**Lesson**: the connection being self-signed (`verify error: self-signed certificate`) is expected and not an error to fix here — this is a local training service, not a real-world certificate that needs to be trusted.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
