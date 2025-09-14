# Level 1 🡒 2: Handling Files with Spaces

## 🎯 Level Goal / Objective
The password for the next level is stored in a file called **spaces in this filename** located in the home directory. The challenge here is dealing with spaces in filenames, which require special handling in the command line.

## 🛠️ Commands You May Need
- `cat` - Display file contents
- `ls` - List directory contents
- `pwd` - Print working directory
- `tab completion` - Auto-complete filenames

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   pwd
   ```

2. **Attempting to read the file (this won't work):**
   ```bash
   cat spaces in this filename
   # This treats each word as a separate filename
   ```

3. **Getting the password using backslash escapes:**
   ```bash
   cat spaces\ in\ this\ filename
   ```

4. **Alternative method using quotes:**
   ```bash
   cat "spaces in this filename"
   ```

## 💡 Explanation

### Key Concepts Learned:
- **Whitespace handling**: Spaces in filenames need special treatment in shell commands
- **Escape characters**: Using backslash (`\`) to escape special characters
- **Quoting**: Using quotes to group words as a single argument
- **Tab completion**: A practical way to handle complex filenames

### Why This Solution Works:
The shell normally treats spaces as argument separators. When you type `cat spaces in this filename`, the shell interprets this as trying to cat four separate files: "spaces", "in", "this", and "filename". By escaping each space with `\` or wrapping the entire filename in quotes, we tell the shell to treat it as a single filename.

### The Problem Explained:
- Spaces are word delimiters in shell commands
- `cat spaces in this filename` = `cat "spaces" "in" "this" "filename"` (4 separate files)
- `cat spaces\ in\ this\ filename` = treat as one filename with spaces
- `cat "spaces in this filename"` = treat everything in quotes as one filename

### Alternative Approaches:
```bash
# Using single quotes
cat 'spaces in this filename'

# Using tab completion (most practical)
cat spa<TAB>
# This will auto-complete to: cat spaces\ in\ this\ filename

# Using wildcards (if unique enough)
cat spa*
cat *filename
```

### Best Practices:
- **Tab completion** is often the easiest method - just type the first few characters and press Tab
- **Double quotes** preserve the filename while allowing variable expansion
- **Single quotes** preserve everything literally (no variable expansion)
- **Backslash escaping** is precise but tedious for long filenames with many spaces

### Pro Tip:
When dealing with files that have spaces, tab completion is your friend! Just type the first few characters of the filename and press Tab - the shell will automatically add the necessary escape characters.

---
**Next:** [Level 3 🡒 4](level-4.md)