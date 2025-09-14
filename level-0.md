# Bandit Level 0: SSH Connection

## 🎯 Level Goal / Objective
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0.

## 🛠️ Commands You May Need
- `ssh` - Secure Shell protocol for connecting to remote servers

## 📝 Steps Taken

1. **Connecting to the Bandit server:**
   ```bash
   ssh bandit0@bandit.labs.overthewire.org -p 2220
   ```
   - When prompted for password, enter: `bandit0`

2. **Successful connection confirmation:**
   ```bash
   # You should see a welcome banner and be logged into the server
   # Your prompt should change to something like: bandit0@bandit:~$ 
   ```

## 💡 Explanation

### Key Concepts Learned:
- **SSH (Secure Shell)**: A cryptographic network protocol for operating network services securely over an unsecured network
- **SSH syntax**: `ssh username@hostname -p port`
- **Remote server access**: Connecting to servers over the internet securely

### Why This Solution Works:
The `ssh` command establishes a secure encrypted connection to the remote Bandit server. The components of the command are:
- `bandit0` - Username for this level
- `@bandit.labs.overthewire.org` - The server hostname  
- `-p 2220` - Specifies port 2220 instead of default SSH port 22
- Password: `bandit0` (same as username for Level 0)

### SSH Connection Breakdown:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
│   │       │                           │
│   │       │                           └── Port number
│   │       └── Server hostname
│   └── Username
└── SSH command
```

### What Happens Next:
Once successfully connected, you'll be logged into the Bandit server and can proceed to Level 0→1 to start solving the actual password challenges.

### Common Issues & Troubleshooting:
- **Connection refused**: Check that you're using port 2220, not the default SSH port 22
- **Host key verification**: If prompted about host key verification, type `yes` to continue
- **Password prompt**: The password is case-sensitive and exactly `bandit0`
- **Network issues**: Ensure you have internet connectivity and no firewall blocking the connection

### Alternative Connection Methods:
```bash
# If your SSH client requires explicit host key checking
ssh -o StrictHostKeyChecking=no bandit0@bandit.labs.overthewire.org -p 2220

# Some systems might need the full command format
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

---
**Next:** [Level 0 🡒 1](level-1.md)