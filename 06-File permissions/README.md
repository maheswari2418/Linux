# 🔐 Linux File Permissions Guide

> Complete guide to understanding and managing file permissions in Linux

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What are file permissions |
| [Why Permissions?](#why-permissions) | Importance of permissions |
| [Permission Types](#permission-types) | Read, Write, Execute |
| [Permission Groups](#permission-groups) | Owner, Group, Others |
| [Understanding Permission Format](#understanding-permission-format) | Reading permissions |
| [Numeric Permissions](#numeric-permissions) | Octal notation |
| [Symbolic Permissions](#symbolic-permissions) | Letter notation |
| [chmod Command](#chmod-command) | Change permissions |
| [chown Command](#chown-command) | Change ownership |
| [chgrp Command](#chgrp-command) | Change group |
| [Special Permissions](#special-permissions) | SUID, SGID, Sticky Bit |
| [Default Permissions](#default-permissions) | umask |
| [Access Control Lists](#access-control-lists-acl) | Advanced permissions |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What are File Permissions?

| Concept | Description |
|---------|-------------|
| **File Permissions** | Rules that control who can read, write, or execute a file |
| **Security Mechanism** | Protect files from unauthorized access |
| **Multi-User System** | Linux allows multiple users; permissions keep data safe |
| **Three-Level System** | Owner, Group, Others - each has separate permissions |

### Basic Concept

| Element | Description |
|---------|-------------|
| **Every file has an owner** | User who created the file |
| **Every file has a group** | Group associated with the file |
| **Three types of access** | Read, Write, Execute |
| **Three levels of users** | Owner, Group members, Everyone else |

---

## Why Permissions?

### Importance of File Permissions

| Reason | Description | Example |
|--------|-------------|---------|
| **Security** | Prevent unauthorized access to sensitive files | Only admin can read `/etc/shadow` |
| **Privacy** | Keep personal files private | Your documents safe from other users |
| **System Protection** | Prevent accidental system damage | Regular users can't delete system files |
| **Collaboration** | Share files with specific users or groups | Team can edit project files together |
| **Compliance** | Meet security standards and regulations | Enforce access control policies |

### Use Cases

| Scenario | Permission Strategy |
|----------|-------------------|
| **Personal files** | Only owner can access (700) |
| **Shared documents** | Owner and group can edit, others read (664) |
| **Web files** | Web server can read, owner can edit (644) |
| **Executable scripts** | Owner can execute, others read (755) |
| **Sensitive configs** | Only owner can read/write (600) |

---

## Permission Types

### Three Permission Types

| Permission | Symbol | Numeric | On Files | On Directories |
|------------|--------|---------|----------|----------------|
| **Read** | `r` | 4 | View file contents | List directory contents (`ls`) |
| **Write** | `w` | 2 | Modify file contents | Create/delete files in directory |
| **Execute** | `x` | 1 | Run file as program | Enter directory (`cd`) |
| **No Permission** | `-` | 0 | No access | No access |

### Detailed Permission Effects

#### On Files

| Permission | What You Can Do | Command Examples |
|------------|----------------|------------------|
| **Read (r)** | View file contents | `cat file`, `less file`, `head file` |
| **Write (w)** | Modify, delete, rename file | `nano file`, `rm file`, `mv file` |
| **Execute (x)** | Run as program or script | `./script.sh`, `python script.py` |

#### On Directories

| Permission | What You Can Do | Command Examples |
|------------|----------------|------------------|
| **Read (r)** | List directory contents | `ls directory/` |
| **Write (w)** | Create, delete, rename files | `touch dir/file`, `rm dir/file` |
| **Execute (x)** | Enter directory, access files | `cd directory/` |

### Important Directory Permission Notes

| Permission Combo | Result |
|------------------|--------|
| `r--` | Can list files but can't access them or enter directory |
| `r-x` | Can list files and access them (most common read-only) |
| `-wx` | Can create/delete files but can't list directory (rare) |
| `--x` | Can access files if you know the name, can't list |
| `rwx` | Full access - read, write, execute |

---

## Permission Groups

### Three User Categories

| Group | Description | Who They Are |
|-------|-------------|--------------|
| **Owner (User)** | File creator/owner | The user who owns the file |
| **Group** | Group members | Users in the file's group |
| **Others** | Everyone else | All other users on the system |

### Permission Structure

| Position | Represents | Example |
|----------|------------|---------|
| **1st set (rwx)** | Owner permissions | What the owner can do |
| **2nd set (rwx)** | Group permissions | What group members can do |
| **3rd set (rwx)** | Others permissions | What everyone else can do |

---

## Understanding Permission Format

### Reading `ls -l` Output

| Output Example | Breakdown |
|----------------|-----------|
| `-rw-r--r--` | Regular file with specific permissions |
| `drwxr-xr-x` | Directory with specific permissions |

### Permission String Breakdown

| Position | Meaning | Example | Description |
|----------|---------|---------|-------------|
| **1** | File type | `-` | Regular file |
| | | `d` | Directory |
| | | `l` | Symbolic link |
| | | `c` | Character device |
| | | `b` | Block device |
| **2-4** | Owner permissions | `rwx` | Owner can read, write, execute |
| **5-7** | Group permissions | `r-x` | Group can read and execute |
| **8-10** | Others permissions | `r--` | Others can only read |

### Example Permission Strings

| Permission String | File Type | Owner | Group | Others |
|-------------------|-----------|-------|-------|--------|
| `-rw-r--r--` | File | rw- (read, write) | r-- (read) | r-- (read) |
| `drwxr-xr-x` | Directory | rwx (full) | r-x (read, execute) | r-x (read, execute) |
| `-rwx------` | File | rwx (full) | --- (none) | --- (none) |
| `lrwxrwxrwx` | Link | rwx (full) | rwx (full) | rwx (full) |
| `-rw-------` | File | rw- (read, write) | --- (none) | --- (none) |

### Full `ls -l` Output

| Column | Description | Example |
|--------|-------------|---------|
| **1** | Permissions | `-rw-r--r--` |
| **2** | Link count | `1` |
| **3** | Owner | `john` |
| **4** | Group | `users` |
| **5** | Size | `1024` bytes |
| **6-8** | Modification date/time | `Nov 15 10:30` |
| **9** | Filename | `document.txt` |

---

## Numeric Permissions

### Octal Notation

| Permission | Binary | Octal | Symbolic |
|------------|--------|-------|----------|
| No permission | 000 | 0 | `---` |
| Execute only | 001 | 1 | `--x` |
| Write only | 010 | 2 | `-w-` |
| Write + Execute | 011 | 3 | `-wx` |
| Read only | 100 | 4 | `r--` |
| Read + Execute | 101 | 5 | `r-x` |
| Read + Write | 110 | 6 | `rw-` |
| Read + Write + Execute | 111 | 7 | `rwx` |

### Calculating Numeric Permissions

| Permission | Value |
|------------|-------|
| Read (r) | 4 |
| Write (w) | 2 |
| Execute (x) | 1 |

**Formula:** Add values together for each group

### Common Numeric Permissions

| Numeric | Symbolic | Description | Common Use |
|---------|----------|-------------|------------|
| `777` | `rwxrwxrwx` | Everyone can do everything | ⚠️ Dangerous - avoid! |
| `755` | `rwxr-xr-x` | Owner full, others read/execute | Executables, directories |
| `700` | `rwx------` | Owner only has access | Private directories |
| `666` | `rw-rw-rw-` | Everyone can read/write | ⚠️ Rarely used |
| `644` | `rw-r--r--` | Owner writes, all read | Regular files, documents |
| `640` | `rw-r-----` | Owner writes, group reads | Shared files with group |
| `600` | `rw-------` | Owner only reads/writes | Private files, SSH keys |
| `555` | `r-xr-xr-x` | All can read/execute, no write | System binaries |
| `444` | `r--r--r--` | All can read only | Read-only files |
| `000` | `---------` | No access for anyone | Locked files |

### Numeric Permission Examples

| Numeric | Owner | Group | Others | Example Use |
|---------|-------|-------|--------|-------------|
| `755` | rwx (7) | r-x (5) | r-x (5) | Scripts, programs |
| `644` | rw- (6) | r-- (4) | r-- (4) | Text files |
| `600` | rw- (6) | --- (0) | --- (0) | Private configs |
| `700` | rwx (7) | --- (0) | --- (0) | Private directories |
| `775` | rwx (7) | rwx (7) | r-x (5) | Shared project directories |

---

## Symbolic Permissions

### Symbolic Notation Components

| Component | Options | Description |
|-----------|---------|-------------|
| **Who** | `u` | User (owner) |
| | `g` | Group |
| | `o` | Others |
| | `a` | All (user, group, others) |
| **Operator** | `+` | Add permission |
| | `-` | Remove permission |
| | `=` | Set exact permission |
| **Permission** | `r` | Read |
| | `w` | Write |
| | `x` | Execute |

### Symbolic Examples

| Command | Description |
|---------|-------------|
| `u+x` | Add execute for owner |
| `g-w` | Remove write from group |
| `o+r` | Add read for others |
| `a+x` | Add execute for all |
| `u=rwx` | Set owner to read, write, execute |
| `go=r` | Set group and others to read only |
| `u+rw,g+r,o-rwx` | Complex multi-permission change |

---

## chmod Command

### Basic chmod Syntax

| Syntax | Description | Example |
|--------|-------------|---------|
| `chmod [options] mode file` | Change file permissions | `chmod 755 script.sh` |

### chmod with Numeric Mode

| Command | Description | Result |
|---------|-------------|--------|
| `chmod 777 file` | Full access for all | `rwxrwxrwx` |
| `chmod 755 file` | Owner full, others read/execute | `rwxr-xr-x` |
| `chmod 644 file` | Owner read/write, others read | `rw-r--r--` |
| `chmod 600 file` | Owner read/write only | `rw-------` |
| `chmod 700 dir` | Owner full access to directory | `rwx------` |
| `chmod 444 file` | Read-only for all | `r--r--r--` |

### chmod with Symbolic Mode

| Command | Description | Result |
|---------|-------------|--------|
| `chmod u+x file` | Add execute for owner | Owner can now execute |
| `chmod g-w file` | Remove write from group | Group can't write |
| `chmod o-r file` | Remove read from others | Others can't read |
| `chmod a+r file` | Add read for all | Everyone can read |
| `chmod u=rwx,g=rx,o=r file` | Set specific permissions | `rwxr-xr--` |
| `chmod go-rwx file` | Remove all from group & others | `rwx------` |

### chmod Options

| Option | Description | Example |
|--------|-------------|---------|
| `-R` | Recursive (apply to directory and contents) | `chmod -R 755 directory/` |
| `-v` | Verbose (show what's being done) | `chmod -v 644 file.txt` |
| `-c` | Report only changes | `chmod -c 755 script.sh` |
| `-f` | Suppress error messages | `chmod -f 644 file.txt` |
| `--reference=file` | Use permissions from reference file | `chmod --reference=file1 file2` |

### chmod Examples

| Task | Command |
|------|---------|
| Make script executable | `chmod +x script.sh` |
| Make file read-only | `chmod 444 file.txt` |
| Private file | `chmod 600 secret.txt` |
| Public directory | `chmod 755 /var/www/html` |
| Shared directory | `chmod 775 /home/shared` |
| Remove all permissions | `chmod 000 locked.txt` |
| Recursive directory permissions | `chmod -R 755 /var/www` |
| Set directory and files differently | `find . -type d -exec chmod 755 {} \; && find . -type f -exec chmod 644 {} \;` |

---

## chown Command

### Basic chown Syntax

| Syntax | Description | Example |
|--------|-------------|---------|
| `chown [options] owner file` | Change file owner | `chown john file.txt` |
| `chown [options] owner:group file` | Change owner and group | `chown john:users file.txt` |
| `chown [options] :group file` | Change group only | `chown :developers file.txt` |

### chown Examples

| Command | Description |
|---------|-------------|
| `chown john file.txt` | Change owner to john |
| `chown john:developers file.txt` | Change owner to john, group to developers |
| `chown :www-data file.txt` | Change group to www-data |
| `chown -R john:users /home/john` | Recursive ownership change |
| `chown --reference=file1 file2` | Copy ownership from file1 to file2 |

### chown Options

| Option | Description | Example |
|--------|-------------|---------|
| `-R` | Recursive | `chown -R john:users directory/` |
| `-v` | Verbose | `chown -v john file.txt` |
| `-c` | Report only changes | `chown -c john file.txt` |
| `-f` | Suppress errors | `chown -f john file.txt` |
| `--from=user` | Change only if current owner matches | `chown --from=alice john file.txt` |

### Common chown Scenarios

| Scenario | Command |
|----------|---------|
| Change web files to web server user | `sudo chown -R www-data:www-data /var/www/html` |
| Fix home directory ownership | `sudo chown -R john:john /home/john` |
| Change log file ownership | `sudo chown syslog:adm /var/log/custom.log` |
| Transfer file ownership | `sudo chown alice:developers project.txt` |

---

## chgrp Command

### Basic chgrp Syntax

| Syntax | Description | Example |
|--------|-------------|---------|
| `chgrp [options] group file` | Change file group | `chgrp developers file.txt` |

### chgrp Examples

| Command | Description |
|---------|-------------|
| `chgrp developers file.txt` | Change group to developers |
| `chgrp -R www-data /var/www` | Recursive group change |
| `chgrp --reference=file1 file2` | Copy group from file1 to file2 |

### chgrp Options

| Option | Description | Example |
|--------|-------------|---------|
| `-R` | Recursive | `chgrp -R developers directory/` |
| `-v` | Verbose | `chgrp -v developers file.txt` |
| `-c` | Report changes only | `chgrp -c developers file.txt` |
| `-f` | Suppress errors | `chgrp -f developers file.txt` |

### chgrp vs chown

| Task | chgrp | chown Equivalent |
|------|-------|------------------|
| Change group only | `chgrp developers file` | `chown :developers file` |
| Change group recursively | `chgrp -R devs dir/` | `chown -R :devs dir/` |

---

## Special Permissions

### Three Special Permission Bits

| Permission | Numeric | On Files | On Directories |
|------------|---------|----------|----------------|
| **SUID (Set User ID)** | 4 | Execute as file owner | No effect |
| **SGID (Set Group ID)** | 2 | Execute as file group | New files inherit directory group |
| **Sticky Bit** | 1 | No effect | Only owner can delete own files |

### SUID (Set User ID)

| Aspect | Description |
|--------|-------------|
| **Purpose** | File executes with owner's permissions |
| **Symbol** | `s` in owner execute position |
| **Numeric** | Add 4000 to permissions |
| **Example** | `/usr/bin/passwd` (users can change passwords) |
| **Security Risk** | Can be exploited if not careful |

### SGID (Set Group ID)

| Aspect | Description |
|--------|-------------|
| **On Files** | Execute with group permissions |
| **On Directories** | New files inherit directory's group |
| **Symbol** | `s` in group execute position |
| **Numeric** | Add 2000 to permissions |
| **Common Use** | Shared project directories |

### Sticky Bit

| Aspect | Description |
|--------|-------------|
| **Purpose** | In shared directories, only owner can delete own files |
| **Symbol** | `t` in others execute position |
| **Numeric** | Add 1000 to permissions |
| **Example** | `/tmp` directory |
| **Use Case** | Prevent users from deleting others' files |

### Setting Special Permissions

| Command | Description | Result |
|---------|-------------|--------|
| `chmod u+s file` | Add SUID | `-rwsr-xr-x` |
| `chmod g+s file` | Add SGID | `-rwxr-sr-x` |
| `chmod +t dir` | Add sticky bit | `drwxrwxrwt` |
| `chmod 4755 file` | SUID + 755 | `-rwsr-xr-x` |
| `chmod 2755 dir` | SGID + 755 | `drwxr-sr-x` |
| `chmod 1777 dir` | Sticky + 777 | `drwxrwxrwt` |

### Special Permission Examples

| Permission String | Numeric | Meaning |
|-------------------|---------|---------|
| `-rwsr-xr-x` | 4755 | SUID + 755 |
| `-rwxr-sr-x` | 2755 | SGID + 755 |
| `drwxrwxrwt` | 1777 | Sticky bit + 777 |
| `-rwsr-sr-x` | 6755 | SUID + SGID + 755 |
| `drwxrws--t` | 3770 | SGID + Sticky + 770 |

---

## Default Permissions (umask)

### What is umask?

| Concept | Description |
|---------|-------------|
| **umask** | Defines default permissions for newly created files |
| **Subtraction** | Permissions are subtracted from base permissions |
| **Base for files** | 666 (rw-rw-rw-) |
| **Base for directories** | 777 (rwxrwxrwx) |

### Common umask Values

| umask | Files Created | Directories Created | Use Case |
|-------|---------------|---------------------|----------|
| `0022` | 644 (rw-r--r--) | 755 (rwxr-xr-x) | Default for most systems |
| `0002` | 664 (rw-rw-r--) | 775 (rwxrwxr-x) | Group collaboration |
| `0077` | 600 (rw-------) | 700 (rwx------) | Maximum privacy |
| `0000` | 666 (rw-rw-rw-) | 777 (rwxrwxrwx) | No restrictions (insecure) |
| `0027` | 640 (rw-r-----) | 750 (rwxr-x---) | Group read, no others |

### umask Commands

| Command | Description |
|---------|-------------|
| `umask` | Display current umask |
| `umask 0022` | Set umask to 0022 |
| `umask -S` | Display umask in symbolic form |

### Calculating Final Permissions

| umask | Base | Result | Explanation |
|-------|------|--------|-------------|
| 0022 | 666 (file) | 644 | 666 - 022 = 644 |
| 0022 | 777 (dir) | 755 | 777 - 022 = 755 |
| 0077 | 666 (file) | 600 | 666 - 077 = 600 |
| 0002 | 777 (dir) | 775 | 777 - 002 = 775 |

---

## Access Control Lists (ACL)

### What is ACL?

| Concept | Description |
|---------|-------------|
| **ACL** | Advanced permissions beyond owner/group/others |
| **Fine-Grained** | Set permissions for specific users or groups |
| **Extends Standard** | Works alongside traditional permissions |
| **Flexibility** | Multiple users with different permissions |

### ACL Commands

| Command | Description | Example |
|---------|-------------|---------|
| `getfacl` | View ACL permissions | `getfacl file.txt` |
| `setfacl -m` | Modify ACL | `setfacl -m u:john:rw file.txt` |
| `setfacl -x` | Remove ACL entry | `setfacl -x u:john file.txt` |
| `setfacl -b` | Remove all ACL | `setfacl -b file.txt` |
| `setfacl -R` | Recursive ACL | `setfacl -R -m u:john:rx directory/` |

### ACL Examples

| Command | Description |
|---------|-------------|
| `setfacl -m u:alice:rw file.txt` | Give alice read/write access |
| `setfacl -m g:developers:rwx directory/` | Give developers group full access |
| `setfacl -m u:bob:- file.txt` | Remove all permissions for bob |
| `setfacl -x u:alice file.txt` | Remove ACL entry for alice |
| `setfacl -m d:u:john:rwx directory/` | Set default ACL for new files |

---

## Practical Examples

### Example 1: Setting Up a Web Directory

| Step | Command | Purpose |
|------|---------|---------|
| 1. Set owner | `sudo chown -R www-data:www-data /var/www/html` | Web server owns files |
| 2. Set directory permissions | `sudo find /var/www/html -type d -exec chmod 755 {} \;` | Directories browsable |
| 3. Set file permissions | `sudo find /var/www/html -type f -exec chmod 644 {} \;` | Files readable |
| 4. Make scripts executable | `sudo chmod +x /var/www/html/cgi-bin/*.sh` | Scripts can run |

### Example 2: Shared Project Directory

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create group | `sudo groupadd developers` | Create project group |
| 2. Add users | `sudo usermod -aG developers john` | Add team members |
| 3. Create directory | `sudo mkdir /home/shared/project` | Shared location |
| 4. Set ownership | `sudo chown root:developers /home/shared/project` | Group owns directory |
| 5. Set permissions | `sudo chmod 2775 /home/shared/project` | SGID + group write |
| 6. Set sticky bit | `sudo chmod +t /home/shared/project` | Protect files |

### Example 3: Secure SSH Keys

| Step | Command | Purpose |
|------|---------|---------|
| 1. Set .ssh directory | `chmod 700 ~/.ssh` | Private directory |
| 2. Set private key | `chmod 600 ~/.ssh/id_rsa` | Only owner can read |
| 3. Set public key | `chmod 644 ~/.ssh/id_rsa.pub` | Readable by all |
| 4. Set authorized_keys | `chmod 600 ~/.ssh/authorized_keys` | Only owner can modify |

### Example 4: Making a Script Executable

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create script | `nano script.sh` | Write script |
| 2. Make executable | `chmod +x script.sh` | Add execute permission |
| 3. Run script | `./script.sh` | Execute script |

### Example 5: Read-Only Files

| Step | Command | Purpose |
|------|---------|---------|
| 1. Make read-only | `chmod 444 important.txt` | No one can modify |
| 2. Make writable again | `chmod 644 important.txt` | Owner can write |

### Example 6: Temporary Public Directory

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create directory | `mkdir /tmp/public` | Temporary share |
| 2. Set permissions | `chmod 1777 /tmp/public` | All can write, sticky bit set |
| 3. Result | Everyone can create files, only owner can delete own files | Protected sharing |

### Example 7: Private User Directory

| Step | Command | Purpose |
|------|---------|---------|
| 1. Set home directory | `chmod 700 /home/john` | Only john can access |
| 2. Set private files | `chmod 600 /home/john/private/*` | Only john can read/write |

### Example 8: Group Collaboration Directory

| Step | Command | Purpose |
|------|---------|---------|
| 1. Create directory | `sudo mkdir /var/projects` | Project location |
| 2. Set group ownership | `sudo chown :developers /var/projects` | Developers group owns |
| 3. Set SGID | `sudo chmod 2775 /var/projects` | New files inherit group |
| 4. Result | All developers can collaborate, files stay in group | Team sharing |

---

## Quick Reference Commands

### Permission Viewing

| Command | Description |
|---------|-------------|
| `ls -l file` | Show file permissions |
| `ls -ld directory` | Show directory permissions |
| `stat file` | Detailed file information |
| `getfacl file` | Show ACL permissions |

### Permission Changing

| Command | Description |
|---------|-------------|
| `chmod 755 file` | Set numeric permissions |
| `chmod u+x file` | Add execute for owner |
| `chmod -R 644 dir/` | Recursive permission change |
| `chown user:group file` | Change owner and group |
| `chgrp group file` | Change group only |

### Common Permission Tasks

| Task | Command |
|------|---------|
| Make executable | `chmod +x script.sh` |
| Private file | `chmod 600 private.txt` |
| Public readable | `chmod 644 document.txt` |
| Private directory | `chmod 700 mydir/` |
| Shared directory | `chmod 2775 shared/` |
| Remove all permissions | `chmod 000 locked` |

---

## Permission Best Practices

| Practice | Description |
|----------|-------------|
| **Principle of Least Privilege** | Give minimum permissions needed |
| **Never use 777** | Extremely dangerous - everyone has full access |
| **Protect private keys** | Always use 600 for SSH keys |
| **Use groups** | Easier than managing individual users |
| **Regular audits** | Check file permissions regularly |
| **SUID carefully** | Only use SUID when absolutely necessary |
| **Document changes** | Keep track of permission changes |

