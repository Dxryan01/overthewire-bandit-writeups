**Bandit Level 20 → Level 21**

**Goal**: use the provided `suconnect` binary, which connects to a given port, reads a password sent to it, and — if it matches `bandit20`'s current password — sends back the password for `bandit21`.

**Reasoning**: `suconnect` needs something listening on the port it connects to, in order to receive the password that gets typed in. That listening role is exactly what `nc` (netcat) can do — opening a port and waiting for a connection, then letting whatever's typed in that terminal be sent through it. This means two separate terminals are needed: one acting as the listener (`nc`), and another running `suconnect` to connect to it.

**Solution**:
1. In one terminal (connected as `bandit20`), start listening on a chosen port: `nc -lvp 2222`
2. In a second terminal (also connected as `bandit20`), run `suconnect` pointing to that same port: `./suconnect 2222`
3. `suconnect` connects to the listener — back in the first terminal, type/paste `bandit20`'s current password and press Enter
4. `suconnect` reads it, confirms it matches, and sends the password for `bandit21` — which appears directly in the first terminal (the `nc` one)

**Lesson**: the choice of port number itself doesn't matter much (it just needs to be free and above 1024 to avoid needing root privileges) — what matters is that both terminals agree on using the same one.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
