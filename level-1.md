# Level 0 🡒 1: Reading Files with Cat Command

## 🎯 Level Goal / Objective
The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `cat` - Display file contents
- `pwd` - Print working directory
- `whoami` - Display current username
- `ssh` - Secure shell for connecting to remote servers

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   pwd
   whoami
   ```

2. **List files in the home directory:**
   ```bash
   ls
   # You should see a file named "readme"
   ```

3. **Read the contents of the readme file:**
   ```bash
   cat readme
   # This will display the password for bandit1
   ```

4. **Use the password to connect to bandit1:**
   ```bash
   exit
   ssh bandit1@bandit.labs.overthewire.org -p 2220
   # Enter the password you found in the readme file
   ```

## 💡 Explanation

### Key Concepts Learned:
- **File reading**: Using `cat` command to display file contents
- **Directory listing**: Using `ls` to see what files are available
- **Basic navigation**: Understanding your current location in the filesystem
- **SSH progression**: Moving from one level to the next using discovered passwords

### Why This Solution Works:
This is the most straightforward level in Bandit. As noted in the original documentation: "Get the password using the CAT command on README". The `cat` command simply reads and displays the entire contents of a file to the terminal, making it perfect for reading password files.

### The Cat Command Explained:
- `cat` stands for "concatenate" but is commonly used to display file contents
- `cat filename` reads and displays the entire file at once
- It's one of the most fundamental Linux commands for file operations
- Perfect for small files like password files

### Basic File Operations:
```bash
# Display file contents
cat filename

# Display file contents with line numbers
cat -n filename

# Display multiple files
cat file1 file2

# Display file contents with non-printing characters visible
cat -A filename
```

### Alternative Approaches:
```bash
# Using less for paginated viewing (good for larger files)
less readme

# Using more for paginated viewing
more readme

# Using head to see first few lines
head readme

# Using tail to see last few lines
tail readme

# Using nano/vim to open in editor (overkill for this level)
nano readme
vim readme
```

### Understanding the File System:
- **Home directory**: Where you start when you log in (represented by `~`)
- **Current directory**: The directory you're currently in (shown by `pwd`)
- **File listing**: `ls` shows files and directories in your current location
- **Hidden files**: Files starting with `.` (not relevant for this level but good to know)

### Pro Tips:
- Always use `ls` first to see what files are available
- `cat` is perfect for small files - for larger files, consider `less` or `more`
- The readme file contains exactly what you need - no tricks or hidden content
- Make sure to copy the password exactly as shown (case-sensitive)

### Common Mistakes:
- Forgetting to use `cat` and just typing the filename
- Not copying the full password (missing characters)
- Typing the password incorrectly when SSH'ing to the next level

---
**Next:** [Level 1 🡒 2](level-2.md)