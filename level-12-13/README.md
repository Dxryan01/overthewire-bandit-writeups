**Bandit Level 12 → Level 13**

**Goal**: find the password stored in `data.txt`, which contains a hexdump of data that has been compressed repeatedly, through several different formats.

**Reasoning**: since the file is hex-encoded, the first step is reversing that with `xxd -r` to get back real binary data. Rather than working directly in the home directory, it's cleaner to create a dedicated temporary folder (e.g. `/tmp/temp`) to extract everything into — this avoids cluttering the home directory with a growing pile of intermediate files as the chain of decompression unfolds. From there, each `file` check reveals what kind of archive/compression is currently wrapping the data — but the true content is hidden several layers deep, so the process has to be repeated: identify the format, rename the file with the matching extension, decompress/extract, then check the result again. Renaming matters because tools like `gunzip`, `bunzip2`, and `tar` decide how to handle a file based on its **extension** (`.gz`, `.bz2`, `.tar`), not its actual content — unlike `file`, which inspects the real content regardless of the name. So even though `file` already tells us the true format, the file still needs to be renamed accordingly before the matching tool will accept it. This continues until `file` finally reports plain ASCII text instead of another compressed format.

**Solution**:
0. Create a working directory to keep things clean: `mkdir /tmp/temp`
1. Reverse the hexdump into real binary data: `xxd -r data.txt > /tmp/temp/data`
2. Move into the working directory: `cd /tmp/temp`
3. Check the file type: `file data`
4. Rename the file with `mv <current_name> <new_name>`, choosing `<new_name>` to match the detected format's expected extension (e.g. `data.gz`, `data.bz2`, `data.tar` — `data` here is just the name chosen back in step 1, nothing forces it; what matters is the extension matching the format, since tools rely on that, not the real content, to know what to do), then decompress/extract with the matching tool (`gunzip`, `bunzip2`, `tar xvf`)
5. Repeat steps 3–4 on the resulting file, since each decompression reveals another layer wrapped in a different format
6. Once `file` reports plain ASCII text instead of a compressed/archive format, read it directly: `cat <final_file>`

In this case, the chain went through gzip → bzip2 → gzip → tar → tar → bzip2 → tar → gzip, before reaching plain text.

**Lesson**: a file can be compressed through multiple different formats stacked on top of each other — there's no way to know in advance how many layers there are, so `file` has to be re-checked after every single decompression step rather than assuming one pass is enough.

---
🔒 Password not disclosed — try it yourself on [overthewire.org](https://overthewire.org/wargames/bandit/)
