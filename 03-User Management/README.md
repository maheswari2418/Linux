# 👥 Linux User Management Guide

> Complete guide to managing users and groups in Linux

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What is user management and why it matters |
| [Why User Management?](#why-user-management) | Benefits and use cases |
| [User Types](#user-types) | Different types of users in Linux |
| [How Users Work](#how-users-work) | Understanding user system internals |
| [User Management Commands](#user-management-commands) | Creating, modifying, deleting users |
| [Group Management](#group-management) | Managing user groups |
| [Password Management](#password-management) | Password policies and commands |
| [User Information](#user-information) | Viewing and checking user details |
| [Permission Management](#permission-management) | File permissions and ownership |
| [Sudo Access](#sudo-access) | Granting administrative privileges |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What is User Management?

| Concept | Description |
|---------|-------------|
| **User Management** | Process of creating, modifying, and controlling user accounts on a Linux system |
| **Multi-user System** | Linux allows multiple users to work on the same system simultaneously |
| **Security** | Users are isolated from each other - one user cannot access another's files without permission |
| **Access Control** | Each user has specific permissions determining what they can and cannot do |

### Linux as Multi-User System

| Feature | Description |
|---------|-------------|
| **Simultaneous Users** | Multiple users can log in and work at the same time |
| **Isolated Environments** | Each user has their own home directory and environment |
| **Shared Resources** | System resources (CPU, memory, disk) are shared among users |
| **Centralized Management** | Administrators control all user accounts from one place |

---

## Why User Management?

### Benefits of User Management

| Benefit | Description | Example |
|---------|-------------|---------|
| **Security** | Prevent unauthorized access to system and data | Only admin can install software |
| **Organization** | Keep user files and settings separate | John's files in `/home/john`, Alice's in `/home/alice` |
| **Accountability** | Track who did what on the system | Logs show which user ran which command |
| **Resource Control** | Limit what users can do or access | Restrict disk space, CPU usage per user |
| **Collaboration** | Multiple people can work on same system safely | Developers can share a server without interfering |

### Use Cases

| Scenario | Why User Management Matters |
|----------|----------------------------|
| **Web Server** | Different users for web admin, database admin, application owner |
| **Development Team** | Each developer has their own account with appropriate access |
| **Company Workstation** | Employee accounts prevent unauthorized access to company data |
| **Home Computer** | Separate accounts for family members with different privileges |
| **Educational Institution** | Students get limited accounts, teachers get more access |

### Security Reasons

| Security Aspect | How User Management Helps |
|-----------------|--------------------------|
| **Principle of Least Privilege** | Users only get permissions they need for their work |
| **Damage Control** | If one account is compromised, others remain safe |
| **Audit Trail** | Track actions to specific users for security investigations |
| **Prevent Accidents** | Normal users can't accidentally delete system files |

---

## User Types

### Types of Users in Linux

| User Type | UID Range | Purpose | Home Directory | Can Login? |
|-----------|-----------|---------|----------------|------------|
| **Root (Superuser)** | 0 | System administrator with all privileges | `/root` | Yes |
| **System Users** | 1-999 | Run system services and daemons | `/var/lib/service` or `/nonexistent` | No |
| **Normal Users** | 1000+ | Regular human users | `/home/username` | Yes |

### Root User

| Attribute | Description |
|-----------|-------------|
| **UID** | 0 (always zero) |
| **Username** | `root` |
| **Home Directory** | `/root` |
| **Permissions** | Unlimited - can do anything on the system |
| **Shell** | Usually `/bin/bash` |
| **When to Use** | Only for administrative tasks, not daily work |

### System Users

| Attribute | Description |
|-----------|-------------|
| **Purpose** | Run system services without root privileges |
| **Examples** | `www-data` (web server), `mysql` (database), `sshd` (SSH daemon) |
| **Login Shell** | Usually `/usr/sbin/nologin` or `/bin/false` |
| **Security** | If service is compromised, attacker doesn't get root access |

### Normal Users

| Attribute | Description |
|-----------|-------------|
| **Purpose** | Human users who log in and work on the system |
| **UID** | Starts from 1000 (configurable) |
| **Home Directory** | `/home/username` |
| **Permissions** | Limited to their own files and explicitly granted access |

---

## How Users Work

### User Account Components

| Component | Description | Location |
|-----------|-------------|----------|
| **Username** | Unique identifier for the user | Used for login |
| **UID (User ID)** | Numeric ID assigned to user | System uses this internally |
| **GID (Group ID)** | Primary group ID | Determines default file ownership |
| **Home Directory** | User's personal directory | `/home/username` |
| **Login Shell** | Command interpreter user gets after login | `/bin/bash`, `/bin/zsh`, etc. |
| **Password** | Encrypted authentication credential | Stored separately for security |

### User Information Files

| File | Purpose | Readable By | Example Entry |
|------|---------|-------------|---------------|
| `/etc/passwd` | User account information | Everyone (world-readable) | `john:x:1001:1001:John Doe:/home/john:/bin/bash` |
| `/etc/shadow` | Encrypted passwords and password policies | Root only | `john:$6$encrypted...:19000:0:99999:7:::` |
| `/etc/group` | Group information | Everyone | `developers:x:1002:john,alice` |
| `/etc/gshadow` | Secure group information | Root only | `developers:!::john,alice` |

### /etc/passwd Format

| Field | Description | Example |
|-------|-------------|---------|
| **Username** | Login name | `john` |
| **Password** | `x` means password in `/etc/shadow` | `x` |
| **UID** | User ID number | `1001` |
| **GID** | Primary group ID | `1001` |
| **GECOS** | User description/full name | `John Doe` |
| **Home Directory** | Path to user's home | `/home/john` |
| **Shell** | Login shell | `/bin/bash` |

### /etc/shadow Format

| Field | Description | Example |
|-------|-------------|---------|
| **Username** | Login name | `john` |
| **Password** | Encrypted password | `$6$salt$hash...` |
| **Last Changed** | Days since 1970-01-01 password was changed | `19000` |
| **Minimum** | Days before password can be changed | `0` |
| **Maximum** | Days before password must be changed | `99999` |
| **Warning** | Days before expiry to warn user | `7` |
| **Inactive** | Days after expiry before account is disabled | Empty |
| **Expire** | Date when account expires | Empty |

---

## User Management Commands

### Creating Users

| Command | Description | Example |
|---------|-------------|---------|
| `useradd` | Create a new user (basic) | `sudo useradd john` |
| `adduser` | Create a new user (interactive, Debian/Ubuntu) | `sudo adduser john` |
| `useradd -m` | Create user with home directory | `sudo useradd -m john` |
| `useradd -m -s` | Create user with specific shell | `sudo useradd -m -s /bin/bash john` |
| `useradd -m -G` | Create user and add to groups | `sudo useradd -m -G sudo,developers john` |
| `useradd -u` | Create user with specific UID | `sudo useradd -u 1500 john` |
| `useradd -c` | Create user with comment/full name | `sudo useradd -m -c "John Doe" john` |

### useradd Options

| Option | Description | Example |
|--------|-------------|---------|
| `-m` | Create home directory | `useradd -m john` |
| `-d` | Specify home directory | `useradd -m -d /custom/home john` |
| `-s` | Set login shell | `useradd -s /bin/zsh john` |
| `-g` | Set primary group | `useradd -g developers john` |
| `-G` | Add to supplementary groups | `useradd -G sudo,www-data john` |
| `-u` | Set specific UID | `useradd -u 2000 john` |
| `-c` | Add comment (full name) | `useradd -c "John Doe" john` |
| `-e` | Set expiration date | `useradd -e 2025-12-31 john` |

### Modifying Users

| Command | Description | Example |
|---------|-------------|---------|
| `usermod -l` | Change username | `sudo usermod -l newname oldname` |
| `usermod -d` | Change home directory | `sudo usermod -d /new/home -m john` |
| `usermod -s` | Change login shell | `sudo usermod -s /bin/zsh john` |
| `usermod -g` | Change primary group | `sudo usermod -g newgroup john` |
| `usermod -G` | Set supplementary groups | `sudo usermod -G sudo,developers john` |
| `usermod -aG` | Add to group (append) | `sudo usermod -aG docker john` |
| `usermod -u` | Change UID | `sudo usermod -u 2000 john` |
| `usermod -L` | Lock user account | `sudo usermod -L john` |
| `usermod -U` | Unlock user account | `sudo usermod -U john` |

### Deleting Users

| Command | Description | Example |
|---------|-------------|---------|
| `userdel` | Delete user (keeps home directory) | `sudo userdel john` |
| `userdel -r` | Delete user and home directory | `sudo userdel -r john` |
| `userdel -f` | Force delete (even if logged in) | `sudo userdel -f john` |

---

## Group Management

### What are Groups?

| Concept | Description |
|---------|-------------|
| **Group** | Collection of users who share access to files and resources |
| **Primary Group** | Every user has one primary group (usually same as username) |
| **Supplementary Groups** | Additional groups a user can belong to |
| **Purpose** | Simplify permission management for multiple users |

### Group Commands

| Command | Description | Example |
|---------|-------------|---------|
| `groupadd` | Create a new group | `sudo groupadd developers` |
| `groupmod -n` | Rename a group | `sudo groupmod -n newname oldname` |
| `groupmod -g` | Change group GID | `sudo groupmod -g 2000 developers` |
| `groupdel` | Delete a group | `sudo groupdel developers` |
| `gpasswd -a` | Add user to group | `sudo gpasswd -a john developers` |
| `gpasswd -d` | Remove user from group | `sudo gpasswd -d john developers` |
| `gpasswd -M` | Set group members | `sudo gpasswd -M john,alice developers` |

### Viewing Group Information

| Command | Description | Example |
|---------|-------------|---------|
| `groups` | Show groups for current user | `groups` |
| `groups user` | Show groups for specific user | `groups john` |
| `id` | Show UID, GID, and groups | `id john` |
| `getent group` | Display all groups | `getent group` |
| `cat /etc/group` | View group file directly | `cat /etc/group` |

---

## Password Management

### Setting Passwords

| Command | Description | Example |
|---------|-------------|---------|
| `passwd` | Change your own password | `passwd` |
| `passwd user` | Change another user's password (as root) | `sudo passwd john` |
| `passwd -l` | Lock user password | `sudo passwd -l john` |
| `passwd -u` | Unlock user password | `sudo passwd -u john` |
| `passwd -d` | Delete user password (passwordless login) | `sudo passwd -d john` |
| `passwd -e` | Force password change on next login | `sudo passwd -e john` |

### Password Policies

| Command | Description | Example |
|---------|-------------|---------|
| `chage` | Change password aging information | `sudo chage john` |
| `chage -l` | List password aging info | `sudo chage -l john` |
| `chage -M` | Set maximum password age | `sudo chage -M 90 john` |
| `chage -m` | Set minimum password age | `sudo chage -m 7 john` |
| `chage -W` | Set password expiration warning | `sudo chage -W 14 john` |
| `chage -E` | Set account expiration date | `sudo chage -E 2025-12-31 john` |

### chage Options

| Option | Description | Example |
|--------|-------------|---------|
| `-l` | List current settings | `chage -l john` |
| `-M days` | Maximum password age | `chage -M 90 john` |
| `-m days` | Minimum password age | `chage -m 7 john` |
| `-W days` | Warning before expiration | `chage -W 14 john` |
| `-I days` | Inactive period after expiration | `chage -I 30 john` |
| `-E date` | Account expiration date | `chage -E 2025-12-31 john` |
| `-d date` | Last password change date | `chage -d 0 john` (force change) |

---

## User Information

### Viewing User Details

| Command | Description | Example Output |
|---------|-------------|----------------|
| `whoami` | Show current username | `john` |
| `id` | Show UID, GID, and groups | `uid=1001(john) gid=1001(john) groups=1001(john),27(sudo)` |
| `who` | Show logged-in users | `john pts/0 2025-11-15 10:30` |
| `w` | Show who is logged in and what they're doing | Detailed activity list |
| `users` | List logged-in usernames | `john alice root` |
| `last` | Show login history | Last logins with timestamps |
| `lastlog` | Show last login for all users | Username, port, last login time |
| `finger` | Display user information | Detailed user info (if installed) |

### Checking User Details

| Command | Description | Example |
|---------|-------------|---------|
| `id username` | Show user's UID, GID, groups | `id john` |
| `getent passwd user` | Get user info from `/etc/passwd` | `getent passwd john` |
| `grep username /etc/passwd` | View user's passwd entry | `grep john /etc/passwd` |
| `groups username` | List user's groups | `groups john` |

---

## Permission Management

### Understanding Permissions

| Permission | Symbol | Numeric | On Files | On Directories |
|------------|--------|---------|----------|----------------|
| **Read** | `r` | 4 | View file contents | List directory contents |
| **Write** | `w` | 2 | Modify file | Create/delete files in directory |
| **Execute** | `x` | 1 | Run file as program | Enter directory |

### Permission Groups

| Group | Description | Example |
|-------|-------------|---------|
| **Owner (User)** | File creator/owner | `rwx` |
| **Group** | Users in file's group | `r-x` |
| **Others** | Everyone else | `r--` |

### Changing Ownership

| Command | Description | Example |
|---------|-------------|---------|
| `chown user file` | Change file owner | `sudo chown john file.txt` |
| `chown user:group file` | Change owner and group | `sudo chown john:developers file.txt` |
| `chown -R` | Change recursively | `sudo chown -R john:john /home/john` |
| `chgrp group file` | Change group only | `sudo chgrp developers file.txt` |
| `chgrp -R` | Change group recursively | `sudo chgrp -R developers /var/www` |

### Changing Permissions

| Command | Description | Example |
|---------|-------------|---------|
| `chmod 755 file` | Set permissions numerically | `chmod 755 script.sh` |
| `chmod u+x file` | Add execute for owner | `chmod u+x script.sh` |
| `chmod g-w file` | Remove write for group | `chmod g-w file.txt` |
| `chmod o-r file` | Remove read for others | `chmod o-r secret.txt` |
| `chmod -R 755 dir` | Change recursively | `chmod -R 755 /var/www` |

### Common Permission Combinations

| Numeric | Symbolic | Description | Use Case |
|---------|----------|-------------|----------|
| `777` | `rwxrwxrwx` | Full access for everyone | ⚠️ Dangerous - avoid! |
| `755` | `rwxr-xr-x` | Owner full, others read/execute | Scripts, public directories |
| `644` | `rw-r--r--` | Owner read/write, others read | Regular files, documents |
| `600` | `rw-------` | Owner read/write only | Private files, SSH keys |
| `700` | `rwx------` | Owner full access only | Private directories |

---

## Sudo Access

### What is Sudo?

| Concept | Description |
|---------|-------------|
| **sudo** | "Superuser do" - run commands with root privileges |
| **Purpose** | Allow specific users to run administrative commands |
| **Security** | Better than giving root password - actions are logged |
| **Temporary** | Elevated privileges only for that one command |

### Granting Sudo Access

| Method | Command | Description |
|--------|---------|-------------|
| **Add to sudo group** | `sudo usermod -aG sudo john` | User can run any command with sudo (Ubuntu/Debian) |
| **Add to wheel group** | `sudo usermod -aG wheel john` | User can run any command with sudo (RHEL/CentOS) |
| **Edit sudoers** | `sudo visudo` | Manually edit sudo configuration |

### Sudoers File Configuration

| Entry | Description | Example |
|-------|-------------|---------|
| `user ALL=(ALL:ALL) ALL` | User can run any command | `john ALL=(ALL:ALL) ALL` |
| `user ALL=(ALL) NOPASSWD: ALL` | User doesn't need password for sudo | `john ALL=(ALL) NOPASSWD: ALL` |
| `user ALL=(ALL) /path/to/command` | User can only run specific command | `john ALL=(ALL) /usr/bin/systemctl` |
| `%group ALL=(ALL:ALL) ALL` | All members of group can sudo | `%developers ALL=(ALL:ALL) ALL` |

### Using Sudo

| Command | Description | Example |
|---------|-------------|---------|
| `sudo command` | Run command as root | `sudo apt update` |
| `sudo -u user command` | Run command as specific user | `sudo -u www-data ls /var/www` |
| `sudo -i` | Open root shell | `sudo -i` |
| `sudo su` | Switch to root user | `sudo su` |
| `sudo su - user` | Switch to another user | `sudo su - john` |
| `sudo -l` | List allowed commands | `sudo -l` |

---

## Practical Examples

### Example 1: Create New Employee Account

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create user | `sudo useradd -m -s /bin/bash -c "John Doe" john` | Create with home and bash shell |
| 2. Set password | `sudo passwd john` | Set initial password |
| 3. Add to groups | `sudo usermod -aG developers,docker john` | Add to work groups |
| 4. Force password change | `sudo passwd -e john` | User must change password on first login |

### Example 2: Create Web Server User

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create group | `sudo groupadd webadmins` | Create web admin group |
| 2. Create user | `sudo useradd -m -G webadmins -s /bin/bash alice` | Create user in group |
| 3. Set password | `sudo passwd alice` | Set password |
| 4. Grant sudo | `sudo visudo` | Add `alice ALL=(ALL) /usr/sbin/nginx, /usr/sbin/apache2` |
| 5. Change ownership | `sudo chown -R alice:webadmins /var/www/mysite` | Give access to website |

### Example 3: Create Service Account

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create user | `sudo useradd -r -s /usr/sbin/nologin -d /var/lib/myapp myapp` | System user, no login |
| 2. Create directory | `sudo mkdir -p /var/lib/myapp` | Create home directory |
| 3. Change ownership | `sudo chown -R myapp:myapp /var/lib/myapp` | Give ownership |
| 4. Set permissions | `sudo chmod 700 /var/lib/myapp` | Restrict access |

### Example 4: Temporary Contractor Access

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create user | `sudo useradd -m -s /bin/bash contractor` | Create user |
| 2. Set password | `sudo passwd contractor` | Set password |
| 3. Set expiration | `sudo chage -E 2025-12-31 contractor` | Account expires end of year |
| 4. Limited access | `sudo usermod -G projectteam contractor` | Only access to project files |
| 5. Check expiration | `sudo chage -l contractor` | Verify expiration date |

### Example 5: Remove User Safely

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check processes | `ps -u john` | See if user has running processes |
| 2. Kill processes | `sudo pkill -u john` | Kill user's processes |
| 3. Backup home | `sudo tar -czf john-backup.tar.gz /home/john` | Backup user data |
| 4. Lock account | `sudo usermod -L john` | Lock before deletion |
| 5. Delete user | `sudo userdel -r john` | Remove user and home |

### Example 6: Grant Developer Access

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create group | `sudo groupadd developers` | Create developers group |
| 2. Add users | `sudo usermod -aG developers john` | Add John to group |
| 3. Add more users | `sudo usermod -aG developers alice` | Add Alice to group |
| 4. Create project dir | `sudo mkdir -p /var/projects` | Create shared directory |
| 5. Set ownership | `sudo chown -R root:developers /var/projects` | Give group ownership |
| 6. Set permissions | `sudo chmod -R 775 /var/projects` | Group can read/write |
| 7. Set sticky bit | `sudo chmod +t /var/projects` | Users can't delete others' files |

---

## Quick Reference Tables

### User Management Quick Reference

| Task | Command |
|------|---------|
| Create user | `sudo useradd -m username` |
| Create user (interactive) | `sudo adduser username` |
| Delete user | `sudo userdel -r username` |
| Change password | `sudo passwd username` |
| Lock account | `sudo usermod -L username` |
| Unlock account | `sudo usermod -U username` |
| Add to group | `sudo usermod -aG groupname username` |
| Change shell | `sudo usermod -s /bin/bash username` |

### Information Quick Reference

| Task | Command |
|------|---------|
| Current user | `whoami` |
| User details | `id username` |
| User's groups | `groups username` |
| Logged in users | `who` |
| Login history | `last` |
| Password info | `sudo chage -l username` |

### Permission Quick Reference

| Task | Command |
|------|---------|
| Change owner | `sudo chown user:group file` |
| Change permissions | `chmod 755 file` |
| Add execute | `chmod +x file` |
| Remove write | `chmod -w file` |
| Recursive change | `chmod -R 755 directory/` |
