# Bandit Level 00

## 🎯 Objective

Connect to the Bandit server via SSH using the credentials provided on the game's introduction page, and get comfortable with the connection itself before the real challenges start.

## 🧠 Concepts covered

- SSH (Secure Shell) as a protocol for remote command-line access
- Specifying a non-default port with SSH
- Basic terminal login flow

## 🔍 Approach

The Bandit intro page gives the host, port, username, and initial password needed to connect. On Linux, SSH is available by default from the terminal, so no extra client is needed.

```bash
# -p specifies the port (2220 instead of the default 22)
# the username is given directly via user@host syntax
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
```

After accepting the host key on first connection and entering the given password, I land in a shell as `bandit0`. From here, the actual challenge begins: exploring the home directory to find what's needed to move on to the next level.

## 💡 Takeaway

Nothing complex at this stage, but it's a good reminder that most SSH connections outside of default setups need the port explicitly specified — something I hadn't paid attention to before, since I'm used to just doing `ssh user@host` on default configs.

---
🔒 No password to redact at this level — the challenge starts once you're logged in. Try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/).
