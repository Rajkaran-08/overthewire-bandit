# Level 7 🡒 8: Finding a Word in a Text File

## 🎯 Level Goal / Objective
The password for the next level is stored in the file `data.txt`, sitting right next to the word `millionth`.

## 🛠️ Commands You May Need
- `cat` - Display file contents
- `grep` - Search for a pattern within input or a file
- `|` (pipe) - Send the output of one command into another

## 📝 Steps Taken

1. **Initial exploration:**
   - `ls -la` to see what's in the home directory

2. **Method 1: cat piped to grep**
   - `cat` the file `data.txt`
   - pipe `|` that output into `grep`
   - search for the word `millionth`

3. **Method 2: grep directly on the file**
   - `grep` for the word `millionth`
   - pass `data.txt` as the file argument instead of piping into it

## 💡 Explanation

### Key Concepts Learned:
- **grep**: scans its input line by line and prints every line that matches a pattern
- **pipes**: `|` feeds the stdout of one command in as the stdin of the next
- grep doesn't need `cat` at all, it can read a file directly

### Why This Solution Works:
Since the password sits on the same line as the word `millionth`, grep matching that word prints the whole line, password included. Piping `cat` into `grep` and pointing `grep` at the file directly both end up scanning the same content, one just has an unnecessary extra step.

### Command Reference:
| Command / Option | Description |
|---|---|
| `cat <file>` | prints the entire file to stdout |
| `\|` | pipes the output of the command on the left into the command on the right |
| `grep <pattern>` | filters piped input for lines matching pattern |
| `grep <pattern> <file>` | greps a file directly, no piping needed |

### Alternative Approaches:
- `grep -i` if unsure about the case of the search word
- Open the file with `less data.txt` and search inside it with `/millionth`

### Pro Tip:
grep can take a filename as an argument, `cat file | grep word` and `grep word file` do the same job. Skip the `cat` when you don't actually need to see the whole file.

---
**Next:** [Level 8 🡒 9](level-9.md)