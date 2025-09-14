# Level 4 🡒 5: Finding Hidden Files

## 🎯 Level Goal / Objective
The password for the next level is stored in a hidden file in the **inhere** directory. In Linux, hidden files start with a dot (`.`) and are not displayed by default with the regular `ls` command.

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `ls -a` - List all files including hidden ones
- `ls -la` - List all files with detailed information
- `cd` - Change directory
- `cat` - Display file contents

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   cd inhere
   pwd
   ```

2. **List files in the directory (won't show hidden files):**
   ```bash
   ls
   # This shows no files or very few files
   ```

3. **List all files including hidden ones:**
   ```bash
   ls -a
   # Now we can see the hidden file(s)
   ```

4. **Getting detailed information about all files:**
   ```bash
   ls -la
   # Shows permissions, ownership, size, and timestamps
   ```

5. **Reading the hidden file:**
   ```bash
   cat .hidden
   # Or whatever the hidden file is named
   ```

6. **Use the password to connect to bandit4:**
   ```bash
   exit
   ssh bandit4@bandit.labs.overthewire.org -p 2220
   ```

## 💡 Explanation

### Key Concepts Learned:
- **Hidden files in Linux**: Files starting with `.` are hidden by default
- **ls command flags**: Different options reveal different levels of information
- **Directory navigation**: Using `cd` to change directories
- **File visibility**: Understanding what's visible vs hidden in Linux filesystems

### Why This Solution Works:
By default, the `ls` command doesn't show files that begin with a dot (`.`). These are considered "hidden" files in Unix-like systems. As mentioned in the original notes: "The password is in a hidden file, just use "-a" flag with "ls"". The `-a` flag (all) tells `ls` to show ALL files, including the hidden ones.

### The Problem Explained:
- Linux treats files beginning with `.` as hidden
- `ls` by default doesn't display hidden files
- `ls -a` shows all files including hidden ones (`.` and `..` directories plus any hidden files)
- `ls -la` combines `-l` (long format) and `-a` (all files) for detailed information

### Common ls Flag Combinations:
```bash
# Basic listing
ls

# Show all files (including hidden)
ls -a

# Long format (detailed info)
ls -l

# Long format + all files
ls -la

# Human readable file sizes
ls -lah

# Sort by modification time
ls -lat
```

### Understanding Hidden Files:
- `.` represents the current directory
- `..` represents the parent directory  
- `.filename` is a hidden file named "filename"
- `.foldername/` is a hidden directory
- Hidden files are commonly used for configuration files (like `.bashrc`, `.profile`)

### Alternative Approaches:
```bash
# Using wildcards to show hidden files
ls .*

# Using find command to locate hidden files
find . -name ".*" -type f

# List everything recursively
ls -laR

# Show only hidden files (excluding . and ..)
ls -la | grep "^\."
```

### Why Files Are Hidden:
- **Configuration files**: Many programs store settings in hidden files
- **System files**: Important files that users don't normally need to see
- **Reducing clutter**: Keeps directories looking clean for everyday use
- **Convention**: Unix tradition of hiding "dot files"

### Pro Tip:
The `-a` flag is essential when you suspect there might be hidden files. Many important system configuration files are hidden, and this convention helps keep directories uncluttered while preserving important files. Always remember to check for hidden files when exploring directories!

---
**Next:** [Level 5 🡒 6](Level-6.md)