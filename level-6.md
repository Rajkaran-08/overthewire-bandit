# Level 5 🡒 6: Finding Human-Readable Files

## 🎯 Level Goal / Objective
The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the "reset" command.

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `cd` - Change directory
- `cat` - Display file contents
- `file` - Determine file type
- `du` - Display directory usage
- `find` - Search for files

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   cd inhere
   ls -la
   ```

2. **Check what files are in the directory:**
   ```bash
   ls
   # You'll see multiple files named -file00, -file01, -file02, etc.
   ```

3. **Determine file types using the file command:**
   ```bash
   file ./-file*
   # This gives file types of all files in the directory
   ```

4. **Alternative approach (from original notes):**
   ```bash
   file ./-f*
   # All files are named -file0* so we use this pattern
   ```

5. **Identify the ASCII text file and read it:**
   ```bash
   # Look for the file that shows "ASCII text" in the output
   cat ./-file07
   # (or whatever file number is the ASCII text file)
   ```

6. **Use the password to connect to bandit5:**
   ```bash
   exit
   ssh bandit5@bandit.labs.overthewire.org -p 2220
   ```

## 💡 Explanation

### Key Concepts Learned:
- **File type identification**: Using the `file` command to determine file contents
- **Human-readable vs binary files**: Understanding different file formats
- **Wildcard patterns**: Using `*` to match multiple files
- **ASCII text files**: Recognizing human-readable text format

### Why This Solution Works:
As noted in the original documentation: "The directory includes a couple of key files, data files and ASCII text file. ASCII text file is the file that you need. Get the file types using 'file' command." The `file` command analyzes the content and structure of files to determine their type, helping us identify which file contains readable text.

### The Problem Explained:
- Multiple files exist with similar names (-file00, -file01, etc.)
- Only one contains human-readable text (ASCII)
- Others contain binary data, executables, or other non-readable formats
- The `file` command reveals which file type each one is

### File Command Output Examples:
```bash
./inhere/-file00: data
./inhere/-file01: ELF 32-bit LSB executable
./inhere/-file02: data  
./inhere/-file03: data
./inhere/-file04: data
./inhere/-file05: data
./inhere/-file06: data
./inhere/-file07: ASCII text
./inhere/-file08: data
./inhere/-file09: data
```

### Why We Need the ./ Prefix:
The files are cleverly named starting with a dash (-file00, -file01, etc.), which creates a problem. If we try to use `file -file*`, the command interprets the `-f` as a command flag and gives an error. By using `file ./-file*`, we explicitly tell the command that we're referring to files in the current directory, not command options.

### Alternative Approaches:
```bash
# Check individual files
file ./-file00
file ./-file01
# ... and so on

# Use find with file command
find . -name "-file*" -exec file {} \;

# Check all files and grep for ASCII
file ./-file* | grep "ASCII"

# Loop through all files
for f in ./-file*; do echo "$f: $(file "$f")"; done
```

### Understanding File Types:
- **ASCII text**: Human-readable text file (what we want)
- **data**: Binary data, not human-readable
- **ELF executable**: Linux executable binary
- **UTF-8 text**: Another form of human-readable text
- **Empty**: File with no content

### Pro Tip:
The `file` command is incredibly useful for identifying file contents when you can't rely on file extensions. It examines the actual file content and magic numbers to determine the true file type, regardless of the filename.

---
**Next:** [Level 6 🡒 7](Level-7.md)