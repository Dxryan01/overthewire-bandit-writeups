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
| Level 7 → Level 8 | Searching text with a whole keyword (grep) | [→](./level-07-08/README.md) |
| Level 8 → Level 9 | Finding the unique line in duplicated data (sort/uniq) | [→](./level-08-09/README.md) |
| Level 9 → Level 10 | Extracting readable text from binary data (strings) | [→](./level-09-10/README.md) |
| Level 10 → Level 11 | Decoding Base64 data | [→](./level-10-11/README.md) |
| Level 11 → Level 12 | Decoding ROT13 (tr) | [→](./level-11-12/README.md) |

*(Table updated as I progress through the levels)*

## Tools / commands covered so far

`man`, `ssh`, `whoami`, `pwd`, `ls`, `cat`, `file`, `find`, `grep`, `wc`, `sort`, `uniq`, `strings`, `base64`, `tr`

## Shell concepts covered so far

- Quoting/escaping (`"..."`, `\ `)
- Relative path prefixing (`./`)
- stderr redirection (`2>/dev/null`)
- Negation in `find` (`-not` / `!`)

*(list expanded level by level)*

## Why this repo

I built this project during a self-directed study period between semesters, using the time to strengthen my Linux and security fundamentals ahead of my coursework. I think it's worth being upfront about that: it shows I take initiative to keep learning outside of class, and hopefully it's a useful reference for others who are just starting out and want proof that you don't need to wait until you're "advanced" to build something concrete.

Next steps after Bandit: Natas, TryHackMe rooms, and beginner-friendly CTFs.
