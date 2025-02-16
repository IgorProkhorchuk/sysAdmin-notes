
### **File Systems and Storage Management**
   - Understanding Linux File Systems: Ext4, XFS, Btrfs
   - Mounting and Unmounting File Systems
   - Disk Management: `fdisk`, `lsblk`, `parted`
   - Logical Volume Manager (LVM) Basics
   - [Understanding RAID Levels](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/raid/RAID-owerview.md) (0, 1, 5, 6, 10)
     - Implementing RAID on Linux (mdadm)

### **Process Management, Automating Tasks and Scripting**
   - Understanding Processes in Linux
   - Monitoring Processes (`ps`, `top`, [`htop`](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/d5673d5d07fd7fc6c851e108bb6db17234edecf7/htop.md))
   - Managing Processes:
       - [`kill`,](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/d5673d5d07fd7fc6c851e108bb6db17234edecf7/kill.md), [pkill]()
       - [`nice`,]()
       - [`renice`,]()
   - Background and Foreground Jobs (`bg`, `fg`, `jobs`)
   - [Automating with `cron` and `systemd`](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/89051b89d0cc86ab906c87d52b481f488cb60adc/scriptingTools/cron-systemd.md)
       - [Scheduling Jobs with `at`](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/89051b89d0cc86ab906c87d52b481f488cb60adc/scriptingTools/at-atd.md)
   - Introduction to Bash Scripting
       - [BASH syntax](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/d5673d5d07fd7fc6c851e108bb6db17234edecf7/BASH-syntax.md)
       - [regex](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/d15f9f968d7087174efaa49b26f9ac6f529e9b29/scriptingTools/regex.md)
   - Writing Simple Scripts for Automation
       - [one-liner scripts](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/d5673d5d07fd7fc6c851e108bb6db17234edecf7/one-liner-scripts.md)
   - Introduction to Ansible for Configuration Management

### **Package Management**
   - Package Managers Overview: APT, DNF, YUM, Zypper
   - Installing, Updating, and Removing Software
   - Managing Repositories
   - Upgrading the Linux Kernel

### **Networking Essentials**
   - Introduction to Networking Concepts (IP, Subnet, Gateway, DNS)
   - Network Configuration in Linux
   - Managing Network Interfaces: `ip`, `ifconfig`, `nmcli`, `nmtui`
   - Monitoring Network Traffic: `ping`, `netstat`, `traceroute`
   - Configuring Static and Dynamic IP Addresses
   - Setting Up and Managing a Firewall (UFW, Firewalld, iptables)

### **Network Services and Protocols**
   - Common Network Services (DNS, DHCP, FTP, SSH, HTTP)
   - Setting up an SSH Server
   - Understanding HTTP/HTTPS
       - [HTTP Status codes](https://github.com/IgorProkhorchuk/sysAdmin-notes/blob/web/http-status-codes.md)
   - Configuring and Managing DNS and DHCP
   - File Transfer Protocols (FTP, SFTP, SCP)
   - Introduction to Email Servers (Postfix, Dovecot)

### **Security and Access Control**
   - User and Group Permissions Best Practices
   - Configuring SSH Keys for Secure Access
   - Using `sudo` for Privileged Access
   - Setting up and Managing Firewalls (UFW, iptables)
   - System Hardening: Removing Unnecessary Services
   - Understanding SELinux and AppArmor

### **Backup and Recovery**
   - Creating Backups with `tar`, `rsync`
   - Automating Backups with `cron`
   - Recovering from System Failures
   - Disk Imaging with `dd`
   - Configuring RAID for Data Redundancy

### **Monitoring and Logging**
   - Using `dmesg`, `journalctl`, and Log Files for Troubleshooting
   - Monitoring System Performance (`top`, `htop`, `vmstat`)
   - Disk Space Monitoring (`df`, `du`)
   - Network Monitoring (`nload`, `iftop`)
   - Setting up Alerts and Notifications

### **Virtualization and Containers**
   - Introduction to Virtualization (KVM, VirtualBox)
   - Creating and Managing Virtual Machines
   - Introduction to Containers: Docker Basics
   - Managing Containers with Docker

### **Troubleshooting and Performance Tuning**
   - Troubleshooting Boot Issues
   - Troubleshooting Network Problems
   - Analyzing Logs for System Errors
   - Performance Tuning: CPU, RAM, and I/O

### **Advanced Topics**
   - Setting up a Linux Server (Apache/Nginx)
   - Configuring Databases (MySQL, PostgreSQL)
   - Setting up a Web Hosting Environment (LAMP/LEMP stack)
   - Implementing RAID with Practical Examples

### **Miscellaneous**
   - [Basic vim commands]()

---
