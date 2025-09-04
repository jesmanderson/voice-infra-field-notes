# Linux Fundamentals

If you're looking to get the most out of Linux without getting overwhelmed, start with the essentials. These key areas cover the 20% of Linux fundamentals that you'll use 80% of the time.


## Basic Linux Commands

### Navigation and File Management
- `pwd`: Print working directory  
- `ls`: List directory contents  
- `cd`: Change directory  
- `cp`, `mv`, `rm`: Copy, move, and remove files/directories  
- `mkdir`, `rmdir`: Create and remove directories  

### File Viewing and Editing
- `cat`, `more`, `less`: View file contents  
- `nano`, `vim`, `gedit`: Text editors for modifying files  



## File Permissions and Ownership

### Understanding Permissions
- `r`, `w`, `x`: Read, write, and execute permissions  
- `chmod`: Change file permissions  
- `chown`: Change file owner and group  

### Viewing Permissions
- `ls -l`: List files with detailed information, including permissions  



## Process Management

### Viewing Processes
- `ps`: Display current processes  
- `top`, `htop`: Interactive process viewer  

### Managing Processes
- `kill`, `killall`: Terminate processes by PID or name  
- `nice`, `renice`: Adjust process priority  



## Package Management

### Debian-based Systems (e.g., Ubuntu)
- `apt-get`, `apt`: Install, update, and remove packages  

### Red Hat-based Systems (e.g., CentOS)
- `yum`, `dnf`: Package management commands  

### General
- `dpkg`, `rpm`: Low-level package management commands  



## Networking

### Basic Networking Commands
- `ifconfig`, `ip`: Display and configure network interfaces  
- `ping`: Test network connectivity  
- `netstat`, `ss`: Network statistics and socket information  

### Network Configuration
- `nano /etc/network/interfaces`: Edit network interfaces file (Debian)  
- `nano /etc/sysconfig/network-scripts/ifcfg-eth0`: Edit network interfaces file (Red Hat)  



## Shell Scripting

### Writing Scripts
- Start with: `#!/bin/bash`  
- Use variables, loops, and conditionals  

### Executing Scripts
- `chmod +x script.sh`: Make the script executable  
- `./script.sh`: Run the script  



## System Monitoring and Performance

### Monitoring Commands
- `df`: Report disk space usage  
- `du`: Estimate file space usage  
- `free`: Display memory usage  

### Log Files
- `/var/log/syslog`: General system log  
- `/var/log/auth.log`: Authentication log  
- `tail -f /var/log/syslog`: Real-time log monitoring  



## User and Group Management

### User Management
- `adduser`, `useradd`: Add a new user  
- `passwd`: Change user password  
- `deluser`, `userdel`: Remove a user  

### Group Management
- `groupadd`: Create a new group  
- `usermod -aG groupname username`: Add a user to a group  



## File System Structure

### Understanding the Directory Structure
- `/home`: User home directories  
- `/etc`: Configuration files  
- `/var`: Variable files like logs  
- `/usr`: User binaries and applications  

### Mounting and Unmounting
- `mount`, `umount`: Mount and unmount filesystems  



## Security and Access Control

### Basic Security Commands
- `sudo`: Execute commands with superuser privileges  
- `ufw`: Uncomplicated Firewall (Debian-based systems)  
- `firewalld`: Dynamic firewall management tool (Red Hat-based systems)  



## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)

