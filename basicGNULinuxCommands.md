### File and Directory Management
- `ls` - List directory contents.
- `cd` - Change directory.
- `pwd` - Print working directory.
- `mkdir` - Create a new directory.
- `rmdir` - Remove an empty directory.
- `rm` - Remove files or directories.
- `cp` - Copy files or directories.
- `mv` - Move or rename files or directories.
- `touch` - Create an empty file or update the timestamp of an existing file.
- `cat` - Concatenate and display file content.
- `less` - View file content one screen at a time.
- `head` - Display the beginning of a file.
- `tail` - Display the end of a file.
- `find` - Search for files and directories.

### File Permissions and Ownership
- `chmod` - Change file permissions.
- `chown` - Change file owner and group.
- `chgrp` - Change group ownership.

### System Information
- `uname` - Print system information.
- `df` - Report file system disk space usage.
- `du` - Estimate file and directory space usage.
- `top` - Display dynamic real-time information about running processes.
- `htop` - Interactive process viewer (requires installation).
- `free` - Display memory usage.
- `uptime` - Show how long the system has been running.

### Networking
- `ping` - Check connectivity to a host.
- `ifconfig` - Display network interface configuration (deprecated, use `ip` instead).
- `ip` - Show/manipulate routing, devices, policy routing, and tunnels.
- `curl` - Transfer data from or to a server (supports many protocols).
- `wget` - Download files from the web.

### Package Management (Varies by Distribution)
- `apt` - Package manager for Debian-based distributions (e.g., Ubuntu).
  - Example: `sudo apt update`, `sudo apt install package_name`
- `yum` - Package manager for RPM-based distributions (e.g., CentOS, Fedora).
  - Example: `sudo yum install package_name`
- `dnf` - Next-generation version of `yum` for Fedora.
  - Example: `sudo dnf install package_name`
- `pacman` - Package manager for Arch Linux.
  - Example: `sudo pacman -S package_name`

### User Management
- `useradd` - Add a new user.
- `usermod` - Modify a user account.
- `userdel` - Delete a user account.
- `passwd` - Change user password.

### System Control
- `shutdown` - Shut down or restart the system.
- `reboot` - Restart the system.
- `systemctl` - Control the systemd system and service manager.
  - Example: `systemctl start service_name`, `systemctl status service_name`

### Text Processing
- `grep` - Search text using patterns.
- `awk` - Pattern scanning and processing language.
- `sed` - Stream editor for filtering and transforming text.

### Archive and Compression
- `tar` - Archive files.
  - Example: `tar -czvf archive.tar.gz /path/to/directory`
- `gzip` - Compress files.
- `unzip` - Extract compressed files.

### Miscellaneous
- `echo` - Display a line of text.
- `man` - Display the manual for a command.
- `history` - Show command history.
- `clear` - Clear the terminal screen.
