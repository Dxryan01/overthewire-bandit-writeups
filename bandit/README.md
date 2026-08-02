# OverTheWire: Bandit — Writeups

Personal writeups for the [Bandit](https://overthewire.org/wargames/bandit/) wargame by OverTheWire, written as part of my ongoing cybersecurity self-study (1st-year CS student, cybersecurity track, IFRI/UAC).

> Out of respect for the challenge, passwords/flags found are not published here. The goal is to document the reasoning and tools used, not to spoil the solution for others.

## About

Bandit is a series of levels that teach the fundamentals of the Linux command line (permissions, file searching, encoding, basic networking, etc.). Each writeup here follows the same structure: the level's Goal, the Reasoning behind the approach, the Solution command(s), and a short Lesson taken from it. For levels involving a genuine multi-step process, the Solution section may list numbered steps instead of a single command.

## Levels

| Level | Main topic | Writeup |
|-------|------------|---------|
| Level 0 | SSH connection basics | [→](./level-00/README.md) |
| Level 0 → Level 1 | Reading a plain file | [→](./level-00-01/README.md) |
| Level 1 → Level 2 | Reading a dash-named file | [→](./level-01-02/README.md) |
| Level 2 → Level 3 | Reading a file with spaces | [→](./level-02-03/README.md) |
| Level 3 → Level 4 | Hidden files | [→](./level-03-04/README.md) |
| Level 4 → Level 5 | Identifying file content types | [→](./level-04-05/README.md) |
| Level 5 → Level 6 | Searching by criteria (find) | [→](./level-05-06/README.md) |
| Level 6 → Level 7 | Searching the whole filesystem (find) | [→](./level-06-07/README.md) |
| Level 7 → Level 8 | Searching text with a known keyword (grep) | [→](./level-07-08/README.md) |
| Level 8 → Level 9 | Finding the unique line in duplicated data (sort/uniq) | [→](./level-08-09/README.md) |
| Level 9 → Level 10 | Extracting readable text from binary data (strings) | [→](./level-09-10/README.md) |
| Level 10 → Level 11 | Decoding Base64 data | [→](./level-10-11/README.md) |
| Level 11 → Level 12 | Decoding ROT13 (tr) | [→](./level-11-12/README.md) |
| Level 12 → Level 13 | Multi-format decompression chain (file/gzip/bzip2/tar) | [→](./level-12-13/README.md) |
| Level 13 → Level 14 | Key-based SSH authentication (scp/chmod) | [→](./level-13-14/README.md) |
| Level 14 → Level 15 | Submitting data to a local port (nc) | [→](./level-14-15/README.md) |
| Level 15 → Level 16 | SSL/TLS connection to a local port (openssl s_client) | [→](./level-15-16/README.md) |
| Level 16 → Level 17 | Scanning a port range for SSL services (nmap) | [→](./level-16-17/README.md) |
| Level 17 → Level 18 | Comparing two files (diff) | [→](./level-17-18/README.md) |
| Level 18 → Level 19 | Running a single remote command over SSH | [→](./level-18-19/README.md) |
| Level 19 → Level 20 | Setuid binaries | [→](./level-19-20/README.md) |
| Level 20 → Level 21 | Two-way communication over a local port (nc/suconnect) | [→](./level-20-21/README.md) |
| Level 21 → Level 22 | Investigating a cron job's privileges | [→](./level-21-22/README.md) |
| Level 22 → Level 23 | Simulating another user's script logic (md5sum) | [→](./level-22-23/README.md) |
| Level 23 → Level 24 | Exploiting a cron job's execution privileges | [→](./level-23-24/README.md) |
| Level 24 → Level 25 | Parallel brute-forcing (xargs -P) | [→](./level-24-25/README.md) |
| Level 25 → Level 26 | Escaping a restricted shell (more/vi)  | [→](./level-25-26/README.md) |
| Level 26 → Level 27 | Setuid binary (again)  | [→](./level-26-27/README.md) |

*(Table updated as I progress through the levels)*

## Tools / commands covered so far

`man`, `ssh`, `whoami`, `pwd`, `ls`, `cat`, `file`, `find`, `grep`, `wc`, `sort`, `uniq`, `strings`, `base64`, `tr`, `xxd`, `gunzip`, `bunzip2`, `tar`, `scp`, `chmod`, `nc`, `openssl`, `nmap`, `diff`, `md5sum`, `seq`, `xargs`, `watch`

## Shell concepts covered so far

- Quoting/escaping (`"..."`, `\ `)
- Relative path prefixing (`./`)
- stderr redirection (`2>/dev/null`)
- Negation in `find` (`-not` / `!`)
- Setuid binaries
- `nc` in listening/server mode (`-l`) vs. client mode
- Cron jobs running with elevated privileges (`/etc/cron.d/`)
- Parallel execution with `xargs -P`
- `for` loops for iterating over a list of values
- Restricted-shell escape via a pager/editor (`more` → `v` → `vi` → `:shell`)

*(list expanded level by level)*

## Why this repo

I built this project during a self-directed study period between semesters, using the time to strengthen my Linux and security fundamentals ahead of my coursework. I think it's worth being upfront about that: it shows I take initiative to keep learning outside of class, and hopefully it's a useful reference for others who are just starting out and want proof that you don't need to wait until you're "advanced" to build something concrete.

Next steps after Bandit: Natas, TryHackMe rooms, and beginner-friendly CTFs.
