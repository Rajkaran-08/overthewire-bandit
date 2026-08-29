# Level 8 🡒 9: Finding the One Line That Doesn't Repeat

## 🎯 Level Goal / Objective
The password for the next level is stored in the file **data.txt**, and it is the only line in that file that occurs exactly once. Every other line appears more than once.

## 🛠️ Commands You May Need
- `sort` - arranges the lines of a file so that identical lines end up next to each other
- `uniq` - collapses or filters adjacent duplicate lines (only works correctly if the input is already sorted)
- `uniq -u` - flag that prints only the lines with no duplicates, instead of collapsing repeats

## 📝 Steps Taken

1. **Initial exploration:**
   - Looked at the file with `cat data.txt`
   - Too many lines to spot the odd one out by eye, so scrolling through manually wasn't practical

2. **Sorting the data:**
   - `sort` on `data.txt` groups every repeated phrase together, so identical lines sit next to each other instead of being scattered

3. **Filtering out the duplicates:**
   - The sorted output needs to be piped (`|`) into `uniq`
   - `uniq` only detects duplicates that are directly adjacent, which is why the sort step has to come first
   - Adding the `-u` flag tells `uniq` to print only the lines that have no duplicate at all, instead of just collapsing repeats down to one copy each

4. **Reading the result:**
   - The single line left over after this is the passphrase for bandit9

## 💡 Explanation

### Key Concepts Learned:
- **Piping**: sending the output of one command straight into another with `|`, so the two work together as a pipeline
- **`uniq` needs sorted input**: it doesn't scan the whole file for duplicates, it only compares each line to the one before it
- **Filtering vs collapsing**: plain `uniq` reduces every group of duplicates down to a single line, while `uniq -u` throws those groups away entirely and keeps only lines that never repeated

### Why This Solution Works:
Since the passphrase is defined as the only line that occurs once, sorting the file first guarantees every duplicate phrase lands next to its copies. Once that's true, `uniq -u` can do exactly what it's built for: drop every line that has a neighbor matching it, leaving just the one line with no match.

### Command / Flag Reference:
| Command / Flag | Purpose |
|---|---|
| `sort` | Reorders lines alphabetically so duplicates become adjacent |
| `uniq` | Compares adjacent lines, collapsing consecutive duplicates |
| `uniq -u` | Prints only lines that have no adjacent duplicate |
| `\|` | Pipes the output of one command into the next |

### Alternative Approaches:
- `sort` also has a `-u` flag, but that suppresses duplicates entirely rather than isolating the one line that never repeated, so it doesn't answer the same question on its own
- `grep` combined with `-c` (count) could work, but sorting the file for adjacent duplicates is the more direct route the level hints at

### Pro Tip:
Whenever a task says "find the line that doesn't repeat" (or the one that does), think `sort` first. Almost every duplicate-detection tool, `uniq` included, only compares neighboring lines rather than scanning the whole file, so getting matching lines next to each other is usually the real first step.

---
**Next:** [Level 9 🡒 10](level-10.md)