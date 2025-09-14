# Level 1 🡒 2: Reading Files with Special Names

## 🎯 Level Goal / Objective
The password for the next level is stored in a file called **-** located in the home directory. Unfortunately, when you try to use the `cat` command on this file, it doesn't work as expected because the filename starts with a dash, which is interpreted as a command-line option.

## 🛠️ Commands You May Need
- `cat` - Display file contents
- `ls` - List directory contents
- `pwd` - Print working directory
- `file` - Determine file type

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   pwd
   ```

2. **Attempting to read the file (this won't work):**
   ```bash
   cat -
   # This will hang waiting for input from stdin
   ```

3. **Getting the password using the correct approach:**
   ```bash
   cat ./-
   ```

## 💡 Explanation

### Key Concepts Learned:
- **Special characters in filenames**: Files that start with `-` are interpreted as command options
- **Relative path notation**: Using `./` to specify current directory explicitly
- **Standard input vs file reading**: Understanding why `cat -` behaves differently

### Why This Solution Works:
The issue occurs because the shell interprets `-` as a command-line option rather than a filename. By using `./−`, we explicitly tell the system that we're referring to a file named `-` in the current directory (`.`), not a command option.

### The Problem Explained:
- `cat -` tells cat to read from standard input (stdin), so it waits for you to type input
- `cat ./-` tells cat to read from a file named `-` in the current directory
- The `./` prefix disambiguates between an option and a filename

### Alternative Approaches:
```bash
# Using absolute path
cat /home/bandit1/-

# Using cat with input redirection
cat < -

# Using full path specification
cat ~/−
```

### Linux Path Concepts:
- `.` represents the current directory
- `./filename` explicitly refers to a file in the current directory
- This technique works for any file that starts with special characters that might be confused with command options

---
**Next:** [Level 2 🡒 3](level-3.md)