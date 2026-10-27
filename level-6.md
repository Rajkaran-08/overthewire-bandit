# Level 5 🡒 6: Finding a File by Size and Permissions

## 🎯 Level Goal / Objective
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `cd` - Change directory
- `cat` - Display file contents
- `file` - Determine file type
- `du` - Display disk usage of files and directories
- `find` - Search for files using flexible criteria

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls
   find
   ```
   `inhere` holds 20 subdirectories (`maybehere00` to `maybehere19`), each with 9 similarly named files (some hidden, some with spaces or a leading dash). Checking them by hand isn't practical.

2. **Checking what `find` can test for:**
   ```bash
   find --help
   ```
   The help output lists the tests available, including ones for size, executable and readable status.

3. **Building the `find` command from its pieces:**
   - **Path:** where to search (`.` is the current directory). The path must come before any test.
   - **`-size 1033c`**: exactly 1033 bytes (`c` means bytes)
   - **`! -executable`**: `!` negates the test that follows, so this keeps only files that are not executable
   - **`-readable`**: keeps only files the current user can read

4. **Reading the result:**
   - Run the `find` command on its own and note the path it prints, then `cat` that file
   - Or send its output into `xargs cat`, which passes each path to `cat` as an argument

## 💡 Explanation

### Key Concepts Learned:
- **`find` tests are combined with AND**: listing several tests together means a file must satisfy all of them
- **Path before expression**: `find` expects paths first, then tests. Putting a path after a test gives a "paths must precede expression" error
- **Negation with `!`**: flips the test that follows it, handy for "not executable"
- **`xargs`**: turns lines from stdin into arguments for another command, which is what `cat` needs here (piping paths straight into `cat` only prints the paths back)

### Why This Solution Works:
Size alone narrows 180 files down a lot, and excluding executables removes the rest of the lookalikes. `find` checks every file under the path against all the tests at once, so only one file survives and no manual inspection is needed.

### Reference:

| Option | What it does |
|---|---|
| `-size Nc` | matches files of exactly N bytes (`+N`/`-N` for more/less than) |
| `-executable` | matches files the current user can execute |
| `-readable` | matches files the current user can read |
| `!` / `-not` | negates the next test |
| `-type f` | matches regular files only |

### Alternative Approaches:
- `find` with `-exec cat {} \;` runs `cat` on each match directly
- Wrap the `find` in `cat $( ... )` using command substitution (curly braces `{ }` will not work for this)
- Run `file` on the candidates afterwards to confirm the match really is ASCII text

### Pro Tip:
`-readable` checks permissions, not whether the content is human-readable. Here size plus "not executable" was enough to isolate one file, but when a search returns several candidates, use `file` to check the actual content type.

---
**Next:** [Level 6 🡒 7](level-7.md)