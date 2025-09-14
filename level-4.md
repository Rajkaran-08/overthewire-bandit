# Level 2 🡒 3: Handling Files with Spaces

## 🎯 Level Goal / Objective
The password for the next level is stored in a file called **spaces in this filename** located in the home directory. The challenge here is dealing with spaces in filenames, which require special handling in the command line.

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `cat` - Display file contents
- `pwd` - Print working directory
- Tab completion for auto-completing filenames

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

5. **Use the password to connect to bandit3:**
   ```bash
   exit
   ssh bandit3@bandit.labs.overthewire.org -p 2220
   ```

## 💡 Explanation

### Key Concepts Learned:
- **Whitespace handling**: Spaces in filenames need special treatment in shell commands
- **Escape characters**: Using backslash (`\`) to escape special characters
- **Quoting**: Using quotes to group words as a single argument
- **Tab completion**: A practical way to handle complex filenames

### Why This Solution Works:
The shell normally treats spaces as argument separators. When you type `cat spaces in this filename`, the shell interprets this as trying to cat four separate files: "spaces", "in", "this", and "filename". The spaces in the name can be escaped using \, another approach is to enclosing the filename in "..." (quotes)

### The Problem Explained:
- Spaces are word delimiters in shell commands
- `cat spaces in this filename` = trying to cat 4 separate files: "spaces", "in", "this", "filename"
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

# Using backslash escapes (as mentioned in your notes)
cat spaces\ in\ this\ filename
```

### Best Practices:
- **Tab completion** is often the easiest method - just type the first few characters and press Tab
- **Double quotes** preserve the filename while allowing variable expansion
- **Single quotes** preserve everything literally (no variable expansion)
- **Backslash escaping** is precise but can be tedious for long filenames with many spaces

### Understanding Shell Argument Parsing:
There's basically two ways you can read a file whose name contains spaces. Both ways ensure that your shell does not interpret the words in the file name as command arguments.

1. **Escape the spaces** with backslashes (`\`)
2. **Quote the filename** with single or double quotes

### Pro Tip:
When dealing with files that have spaces, tab completion is your friend! Just type the first few characters of the filename and press Tab - the shell will automatically add the necessary escape characters.

### Common Mistakes:
- Forgetting that spaces separate arguments
- Not using quotes or escapes when needed  
- Mixing quote types inconsistently

---
**Next:** [Level 4 🡒 5](level-5.md)