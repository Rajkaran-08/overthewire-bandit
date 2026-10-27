# Level 11 🡒 12: ROT13 with the tr Command

## 🎯 Level Goal / Objective
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## 🛠️ Commands You May Need
- `cat` - Display file contents
- `echo` - Print a test string (handy for checking a mapping)
- `tr` - Translate characters from one set to another
- `|` (pipe) - Feed the output of one command into another

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls
   cat data.txt
   # Readable shape ("Gur cnffjbeq vf ..."), but the letters are shifted
   ```

2. **Understanding the tool:**
   - `tr` reads only from stdin, so the file has to be piped or redirected in (it doesn't accept a filename)
   - `tr SET1 SET2` replaces the 1st character of SET1 with the 1st of SET2, the 2nd with the 2nd, and so on

3. **Building the mapping (combine these yourself):**
   - **SET1:** `a-zA-Z` (all 52 letters, lowercase first, then uppercase)
   - **SET2, part 1:** lowercase, starting 13 letters after `a`, running to `z`
   - **SET2, part 2:** the lowercase letters that wrap around from `a` up to just before part 1
   - **SET2, part 3 and 4:** the same two ranges again, in uppercase
   - Order matters: SET2 must have all lowercase ranges first, then all uppercase ranges, to line up with SET1

4. **Testing before the real run:**
   - Pipe a short word (`echo`) into your `tr` command and check it comes out as real English
   - The file starts with `Gur`, which should decode to a common English word

5. **Getting the password:**
   - Pipe `cat data.txt` into your tested `tr` command

## 💡 Explanation

### Key Concepts Learned:
- **`tr` works by position**: characters in SET1 and SET2 are paired up one to one, so both sets must be the same length
- **Ranges can't wrap**: a range like `m-a` errors out ("reverse collating sequence order"), so a wrap-around has to be split into two forward ranges
- **`tr` only reads stdin**: `echo data.txt | tr ...` transforms the text "data.txt", not the file's contents
- **ROT13 is its own inverse**: 13 is half of 26, so running text through the same mapping twice gives back the original

### Why This Solution Works:
ROT13 shifts every letter 13 places, wrapping from `z` back to `a`. Writing SET2 as the same alphabet started 13 letters later makes each letter in SET1 line up with its shifted partner, so `tr` can undo the rotation in one pass. Lowercase and uppercase are separate alphabets, so each needs its own pair of ranges.

### Reference:

| Command / Syntax | What it does |
|---|---|
| `tr SET1 SET2` | replaces each character in SET1 with the one at the same position in SET2 |
| `a-z` | range shorthand for every letter from `a` to `z` |
| `cat file \| tr ...` | feeds a file into `tr` through stdin |
| `tr ... < file` | same idea using input redirection |

### Mistakes Along the Way:
- Writing a wrapping range like `m-a` (not allowed, split it in two)
- Lowercase-only mapping left uppercase letters untouched, giving `Ghe` instead of `The`
- Putting uppercase ranges before the lowercase wrap-around range broke the position pairing and scrambled the text
- Using `echo data.txt` instead of `cat data.txt` transformed the filename, not the file

### Alternative Approaches:
- `tr ... < data.txt` instead of `cat` with a pipe
- Character classes like `[:lower:]` and `[:upper:]` exist, but they don't express a rotation on their own

### Pro Tip:
Always test a `tr` mapping on a short known string before running it on the real file. If a short word doesn't decode, the sets are misaligned, and it's much easier to debug on three letters than on a whole file.

---
**Next:** [Level 12 🡒 13](level-13.md)