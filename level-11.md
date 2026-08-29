# Level 10 🡒 11: Decoding Base64

## 🎯 Level Goal / Objective
The password for level 11 is stored in a single file called **data.txt** in the bandit10 home directory. The file contains data encoded in base64, so it needs to be decoded before the password is readable.

## 🛠️ Commands You May Need
- `ls` - List directory contents
- `file` - Determine file type
- `cat` - Display file contents
- `base64` - Encode or decode base64 data

## 📝 Steps Taken

1. **Initial exploration:**
   ```bash
   ls -la
   file data.txt
   ```
   Confirms there is only one file in the home directory, and that `file` reports it as ASCII text (base64 output only ever uses printable characters, which is why it shows up as text rather than data).

2. **Finding the solution:**
   - `base64` : the command used to encode or decode base64 data
   - `-d` : flag that switches base64 from its default behavior (encoding) to decoding
   - `data.txt` : the file to decode, passed as the final argument

3. **Getting the password:**
   - Combine the flag and the filename with the `base64` command to decode the file and print the password straight to the terminal.

## 💡 Explanation

### Key Concepts Learned:
- **Base64 encoding**: a scheme that represents binary data using a set of 64 printable ASCII characters, commonly used to safely move data through text based channels
- **Encoding vs encryption**: base64 is not encryption. There's no key involved, so anyone can reverse it, it's purely a formatting layer
- **Single letter flags**: coreutils commands like `base64` use short flags such as `-d` to change their default behavior

### Why This Solution Works:
Because base64 output is just printable ASCII text, `file` correctly identifies data.txt as a text file rather than binary data. Running that same text back through `base64` with the decode flag reverses the encoding and returns the original bytes, which in this case is the plaintext password.

| Command/Flag | Description |
|---|---|
| `base64` | encodes or decodes data, printing the result to stdout |
| `-d`, `--decode` | tells base64 to decode instead of encode |
| `-i`, `--ignore-garbage` | when decoding, ignores non-alphabet characters (not needed here, but useful if a file has stray line breaks or junk mixed into the base64 data) |

### Alternative Approaches:
- Pipe the file into base64 instead of passing it as an argument, using `cat` and a `|` before `base64 -d`
- Use the long form of the flag, `--decode`, instead of `-d`

### Pro Tip:
Don't mistake base64 for security. It's reversible by design and meant for safe data transport, not for hiding anything from a determined reader.

---
**Next:** [Level 11 🡒 12](level-12.md)