> tip: click on the topic or command for further information  


### [File and Directory Management](fileDirManagement/fileAndDirectoryManagement.md)
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

### [Networking](networking/workWithNetwork.md)
- [`ping`]() - Check connectivity to a host.
- [`traceroute`]() - Traces the route packets take to a network host
- [`mtr`]() Combines ping and traceroute for continuous network diagnostics
- [`ifconfig`]() - Display network interface configuration (deprecated, use `ip` instead).
- [`ip`]() - Show/manipulate routing, devices, policy routing, and tunnels.
- [`curl`]() - Transfer data from or to a server (supports many protocols).
- [`wget`]() - Download files from the web.
- [`nmap`](commands/nmap.md) - network scanning tool.
- [`netcat`](commands/netcat.md) - 
- [`route`]() - Shows and manipulates the IP routing table
- [`nmcli`]() - Manages NetworkManager, useful on modern Linux systems for configuring connections
- [`dhclient`]() - Configures network interfaces using DHCP
- [`netstat`]() - Displays network connections, routing tables, interface statistics, etc
- [`ss`]() - Newer tool that replaces netstat, showing socket information.
- [`arp`]() - Shows and manipulates the ARP cache
- [`dig`]() - DNS lookup tool that queries DNS servers
- [`telnet`]() - Tests connectivity to a specific port
- [`tcpdump`]() - Captures and analyzes network packets
- [`iftop`]() - Displays bandwidth usage by active connections
- [`nload`]() - Monitors incoming and outgoing network traffic in real-time.
- [`iptraf-ng`]() - Interactive, text-based network monitoring tool.
- [`bmon`]() - Bandwidth monitor that provides a graphical view in the terminal.
- [`iperf3`]() - Tests network throughput between two hosts
- [`hping3`]() - Network testing tool that sends TCP, UDP, and ICMP packets
- [`ssh`]() - Secure Shell for encrypted network connections
- [`openvpn`]() - Open-source VPN software for creating secure tunnels.
- [`stunnel`]() - Adds SSL encryption to network connections.
- [`socat`]() - Versatile utility for establishing bidirectional data transfers over various types of sockets, including TCP and UDP.
- [`scp`]() - Secure file copy over SSH
- [`rsync`]() - Synchronizes files and directories between hosts over SSH
- [`ftp and sftp`]() - Command-line FTP clients (SFTP is secure, FTP is not).
- [`ethtool`]() - Displays and modifies Ethernet device parameters.
- [`iwconfig`]() - Configures wireless network interfaces.
- [`iwlist`]() - Scans for available wireless networks

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
- [`history`](commands/miscellaneous/history.md) - Show command history.
- `clear` - Clear the terminal screen.
