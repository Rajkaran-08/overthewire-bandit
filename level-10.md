# Level 9 🡒 10: Extracting Strings from a Binary File

## 🎯 Level Goal / Objective
The password for the next level is stored in the file `data.txt`, in one of the few human readable strings, preceded by several '=' characters.

## 🛠️ Commands You May Need
- `file` - determine a file's type
- `strings` - extract printable text from a binary file
- `grep` - search text using patterns

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls
   ```

2. **Checking what kind of file data.txt is:**
   ```bash
   file data.txt
   # confirms it's not plain ASCII, just reported as "data" (binary)
   ```

3. **Pulling readable text out of the binary:**
   - Run `strings` on the filename
   - This dumps every printable character sequence embedded in the file, still a lot of noise

4. **Filtering down to the line with the password:**
   - Pipe (`|`) the output of `strings` into `grep`
   - Search pattern: two or more `=` characters in a row, since the level goal says the password line is preceded by several `=`

## 💡 Explanation

### Key Concepts Learned:
- **Binary vs. text files**: `file` reported `data.txt` as generic "data", which is a sign it can't be read directly with `cat`
- **`strings` command**: scans a binary file and prints out any embedded run of printable characters long enough to count as a string, useful for pulling text out of otherwise unreadable files
- **Chaining `strings` with `grep`**: narrows a large, noisy dump down to the one relevant line

### Why This Solution Works:
Binary files can still contain small chunks of plain text embedded inside them, like markers or debug output. `strings` walks through the file byte by byte and prints out any sequence of printable characters, regardless of the surrounding binary data. Piping that into `grep`, searching for the repeated `=` characters mentioned in the level goal, isolates the password line from everything else.

### Reference:

| Command / Flag | What it does |
|---|---|
| `file <name>` | reports the detected type of a file |
| `strings <name>` | prints printable character sequences found in a file |
| `grep "pattern"` | filters input down to lines matching a pattern |
| `grep -a` | forces grep to treat a binary file as text |
| `grep --binary-files=text` | same idea as `-a`, treats binary input as text |

### Alternative Approaches:
- Running `grep -a` or `grep --binary-files=text` directly on `data.txt` works too, but the output is messier since it still includes stray non-printable bytes
- Using `grep -E` with a repetition pattern for the `=` characters instead of a literal match, for a more precise filter

### Pro Tip:
When a file doesn't behave like plain text, check its type with `file` first. If it turns out to be binary, `strings` is usually the fastest way to see if there's anything human readable buried inside before reaching for something heavier like a hex editor.

---
**Next:** [Level 10 🡒 11](level-11.md)