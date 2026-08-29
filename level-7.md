# Level 6 🡒 7: Searching the Entire Filesystem by Owner, Group & Size

## 🎯 Level Goal / Objective
The password for the next level is stored somewhere on the server and has all of the following properties:
- Owned by user `bandit7`
- Owned by group `bandit6`
- 33 bytes in size

We aren't told where the file lives, so this time `find` has to search from root (`/`), not a specific directory.

## 🛠️ Commands You May Need
- `find` - Search for files across the filesystem using flexible criteria
- `cat` - Display file contents
- `grep` - Filter output for matching lines

## 📝 Steps Taken

1. **First attempt (works, but clunky):**
   ```bash
   ls -laR | grep bandit7
   ```
   Lists everything recursively and filters for `bandit7`, but doesn't give a usable path.

2. **Narrowing with `find` + `grep`:**
   ```bash
   find . -type f -size 33c | grep bandit7
   ```
   Returns a path, but it's noisy and relies on the username coincidentally showing up in the output rather than checking real ownership.

3. **Building a proper `find` command:**
   `find` can check ownership and size directly instead of piping into `grep`. Work out each piece, then combine them yourself:
   - **Starting point:** where should the search begin, given you don't know the location? (Not `.` this time.)
   - **`-type f`**: restrict to regular files.
   - **`-user <username>`**: match the owning user.
   - **`-group <groupname>`**: match the owning group.
   - **`-size 33c`**: exact size of 33 bytes.
   - **`2>/dev/null`**: redirect stderr so permission errors don't clutter the output.

4. **Reading the file:**
   Either run `find` on its own and `cat` the path it prints, or feed it straight into `cat` with command substitution: `cat $( ... )`.

5. **Use the password to connect to bandit7:**
   ```bash
   exit
   ssh bandit7@bandit.labs.overthewire.org -p 2220
   ```

## 💡 Explanation

### Key Concepts Learned:
- **`find` as a filter**: give it `-user`, `-group`, and `-size` together and it checks all three at once, no `grep` needed.
- **Searching from root**: start at `/` when you don't know where a file lives.
- **Command substitution `$(...)`**: runs the inner command first and feeds its output into the outer one, e.g. `cat $(find ...)`.
- **Redirecting stderr**: `2>/dev/null` sends error messages to file descriptor 2, discarding them so only real output shows.

### Why This Solution Works:
`find` walks the whole tree from the given path and tests every file against the conditions given. Combining `-user`, `-group`, and `-size` means only a file matching all three gets returned, which narrows a huge filesystem down to one result.

### `find` Reference:

| Option | Meaning |
|---|---|
| `-user uname` | Owned by user `uname` |
| `-group gname` | Owned by group `gname` |
| `-type f` | Regular file (`d` for directory, `l` for symlink) |
| `-size 33c` | Exact size in bytes; `+`/`-` means greater/less than |

Size suffixes: `b` (512-byte blocks, default), `c` (bytes), `w` (2-byte words), `k` (KiB), `M` (MiB), `G` (GiB).

### Alternative Approaches:
- `find` also supports `-exec cat {} \;` to run `cat` on a match directly, instead of using command substitution.
- Split into two steps: run `find` first, note the path, then `cat` it separately.

### Pro Tip:
When you don't know where a file lives, give `find` every property you know (owner, group, size, type) instead of guessing directories. The more specific the criteria, the fewer false positives.

---
**Next:** [Level 7 🡒 8](level-8.md)