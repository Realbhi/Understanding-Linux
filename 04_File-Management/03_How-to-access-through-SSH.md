### Connecting to Linux Servers via SSH

In real-world workplaces, you typically connect remotely to Linux servers or virtual machines hosted on cloud platforms like AWS or Azure.
SSH (Secure Shell) is the standard protocol enabling secure remote login.
Linux servers run an SSH daemon (sshd) by default.

On local machines, SSH clients like Git Bash (Windows), Terminal (macOS), or WSL (Windows) allow users to connect to servers.

**The SSH connection command format: ssh @**

Password authentication may be disabled on cloud servers for security reasons; alternative authentication methods like SSH keys are used instead.
Password authentication can be enabled or disabled by modifying the file /etc/ssh/sshd_config or files under /etc/ssh/sshd_config.d/, followed by restarting the SSH service using systemctl restart sshd.

![IMG_7064](https://github.com/user-attachments/assets/2a65d231-6e69-4f37-9ae0-a60b78141580)
