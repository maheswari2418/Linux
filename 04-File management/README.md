# 📂 Linux File Management Guide

> Complete guide to managing files and directories in Linux

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What is file management and why it matters |
| [Why File Management?](#why-file-management) | Benefits and use cases |
| [File System Basics](#file-system-basics) | Understanding files and directories |
| [How Files Work](#how-files-work) | Internal file system structure |
| [Navigation Commands](#navigation-commands) | Moving around the filesystem |
| [Viewing Files](#viewing-files) | Reading and displaying file contents |
| [Creating Files & Directories](#creating-files--directories) | Making new files and folders |
| [Copying Files](#copying-files) | Duplicating files and directories |
| [Moving & Renaming](#moving--renaming) | Moving and renaming files |
| [Deleting Files](#deleting-files) | Removing files and directories |
| [Finding Files](#finding-files) | Searching for files and directories |
| [File Permissions](#file-permissions) | Understanding and managing permissions |
| [File Compression](#file-compression) | Compressing and extracting archives |
| [File Content Operations](#file-content-operations) | Searching and manipulating file contents |
| [Links](#links) | Hard links and symbolic links |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What is File Management?

| Concept | Description |
|---------|-------------|
| **File Management** | Process of organizing, storing, retrieving, and manipulating files and directories |
| **Hierarchical Structure** | Files organized in tree-like directory structure starting from `/` (root) |
| **Everything is a File** | In Linux, everything is treated as a file (devices, directories, processes) |
| **Case Sensitive** | `File.txt` and `file.txt` are different files |

### Linux File System Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Single Root** | All files start from `/` (root directory) |
| **No Drive Letters** | Unlike Windows (C:, D:), Linux uses mount points |
| **Hidden Files** | Files starting with `.` are hidden (e.g., `.bashrc`) |
| **No Extensions Required** | File type not determined by extension but by content |
| **Path Separators** | Forward slash `/` used (not backslash `\`) |

---

## Why File Management?

### Benefits of Proper File Management

| Benefit | Description | Example |
|---------|-------------|---------|
| **Organization** | Keep files structured and easy to find | Projects in separate directories |
| **Efficiency** | Quick access to files without searching | Organized home directory |
| **Security** | Control who can access files | Restrict sensitive files to owner only |
| **Backup** | Easier to backup organized files | Backup entire `/home` directory |
| **Collaboration** | Share files with proper permissions | Team project directories with group access |
| **Maintenance** | Clean up old or unnecessary files | Regular cleanup of `/tmp` |

### Use Cases

| Scenario | Why File Management Matters |
|----------|----------------------------|
| **Development Projects** | Organize code, tests, documentation separately |
| **Web Server** | Proper structure for websites, logs, configs |
| **Media Storage** | Organize photos, videos, music by category |
| **System Administration** | Maintain configs, backups, logs systematically |
| **Data Analysis** | Keep datasets, scripts, results organized |

### Common File Management Tasks

| Task | Frequency | Importance |
|------|-----------|------------|
| **Creating backups** | Daily/Weekly | Critical |
| **Organizing files** | Daily | High |
| **Finding files** | Multiple times daily | High |
| **Managing permissions** | As needed | Critical |
| **Cleaning temp files** | Weekly/Monthly | Medium |
| **Archiving old data** | Monthly/Quarterly | Medium |

---

## File System Basics

### File Types in Linux

| Type | Symbol | Description | Example |
|------|--------|-------------|---------|
| **Regular File** | `-` | Normal files (text, binary, images) | `document.txt`, `photo.jpg` |
| **Directory** | `d` | Folder containing files | `/home/user` |
| **Symbolic Link** | `l` | Shortcut to another file | `link -> /path/to/file` |
| **Block Device** | `b` | Block storage device | `/dev/sda` (hard drive) |
| **Character Device** | `c` | Character device | `/dev/tty` (terminal) |
| **Socket** | `s` | Inter-process communication | `/var/run/docker.sock` |
| **Named Pipe** | `p` | FIFO pipe for process communication | Named pipes |

### Path Types

| Path Type | Description | Example | When to Use |
|-----------|-------------|---------|-------------|
| **Absolute Path** | Starts from root `/` | `/home/john/documents/file.txt` | When exact location needed |
| **Relative Path** | Relative to current directory | `documents/file.txt` | When working in related directories |
| **Home Directory** | Represented by `~` | `~/documents/file.txt` | Referring to user's home |

### Special Directory Symbols

| Symbol | Meaning | Example Usage |
|--------|---------|---------------|
| `/` | Root directory | `cd /` |
| `~` | Current user's home directory | `cd ~` or `cd ~/documents` |
| `.` | Current directory | `cp file.txt .` |
| `..` | Parent directory | `cd ..` |
| `-` | Previous directory | `cd -` |

---

## How Files Work

### File Metadata (Inode)

| Attribute | Description | Example |
|-----------|-------------|---------|
| **Inode Number** | Unique identifier for file | `12345678` |
| **File Type** | Type of file | Regular, directory, link |
| **Permissions** | Access rights | `rwxr-xr-x` |
| **Owner** | User who owns file | `john` (UID: 1001) |
| **Group** | Group that owns file | `users` (GID: 100) |
| **Size** | File size in bytes | `1024` bytes |
| **Timestamps** | Access, modify, change times | Last modified: 2025-11-15 |
| **Link Count** | Number of hard links | `1` |

### File Timestamps

| Timestamp | Description | When Updated | View Command |
|-----------|-------------|--------------|--------------|
| **atime** | Access time | When file is read | `ls -lu` |
| **mtime** | Modification time | When file content changes | `ls -l` |
| **ctime** | Change time | When metadata changes | `ls -lc` |

### File Size Units

| Unit | Size | Description |
|------|------|-------------|
| **Byte (B)** | 1 byte | Smallest unit |
| **Kilobyte (KB)** | 1,024 bytes | Small files |
| **Megabyte (MB)** | 1,024 KB | Medium files |
| **Gigabyte (GB)** | 1,024 MB | Large files |
| **Terabyte (TB)** | 1,024 GB | Very large files |

---

## Navigation Commands

### Basic Navigation

| Command | Description | Example | Result |
|---------|-------------|---------|--------|
| `pwd` | Print working directory | `pwd` | `/home/john/documents` |
| `cd` | Change directory | `cd /var/log` | Moves to `/var/log` |
| `cd ~` | Go to home directory | `cd ~` | Moves to `/home/john` |
| `cd ..` | Go to parent directory | `cd ..` | Moves up one level |
| `cd -` | Go to previous directory | `cd -` | Returns to previous location |
| `cd /` | Go to root directory | `cd /` | Moves to `/` |

### Listing Files

| Command | Description | Example | Shows |
|---------|-------------|---------|-------|
| `ls` | List files | `ls` | Basic file list |
| `ls -l` | Long format | `ls -l` | Detailed info with permissions |
| `ls -a` | Show all (including hidden) | `ls -a` | Shows `.bashrc`, `.profile` |
| `ls -h` | Human readable sizes | `ls -lh` | Shows `1.5K` instead of `1536` |
| `ls -R` | Recursive listing | `ls -R` | Lists subdirectories too |
| `ls -t` | Sort by modification time | `ls -lt` | Newest files first |
| `ls -S` | Sort by size | `ls -lS` | Largest files first |
| `ls -r` | Reverse order | `ls -lr` | Reverse alphabetical |

### ls Output Explained

| Column | Description | Example |
|--------|-------------|---------|
| **Permissions** | File access rights | `-rw-r--r--` |
| **Links** | Number of hard links | `1` |
| **Owner** | File owner username | `john` |
| **Group** | File group name | `users` |
| **Size** | File size | `1024` |
| **Date/Time** | Last modification | `Nov 15 10:30` |
| **Filename** | Name of file | `document.txt` |

### Directory Tree Commands

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `tree` | Display directory tree | `tree` | Visual directory structure |
| `tree -L` | Limit depth | `tree -L 2` | Show 2 levels only |
| `tree -d` | Directories only | `tree -d` | Skip files |
| `tree -a` | Show hidden files | `tree -a` | Include dotfiles |

---

## Viewing Files

### Display File Contents

| Command | Description | Example | Best For |
|---------|-------------|---------|----------|
| `cat` | Display entire file | `cat file.txt` | Small files |
| `less` | View file with pagination | `less file.txt` | Large files (scrollable) |
| `more` | Page through file | `more file.txt` | Large files (forward only) |
| `head` | Show first lines | `head file.txt` | File beginning (default 10 lines) |
| `head -n` | Show first N lines | `head -n 20 file.txt` | First 20 lines |
| `tail` | Show last lines | `tail file.txt` | File end (default 10 lines) |
| `tail -n` | Show last N lines | `tail -n 20 file.txt` | Last 20 lines |
| `tail -f` | Follow file (live updates) | `tail -f /var/log/syslog` | Log monitoring |

### less Commands (While Viewing)

| Key | Action |
|-----|--------|
| `Space` | Page down |
| `b` | Page up |
| `q` | Quit |
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next search result |
| `N` | Previous search result |
| `g` | Go to beginning |
| `G` | Go to end |

### File Type Identification

| Command | Description | Example | Output |
|---------|-------------|---------|--------|
| `file` | Determine file type | `file document.pdf` | `PDF document, version 1.4` |
| `file *` | Check all files in directory | `file *` | Type of each file |
| `stat` | Display file statistics | `stat file.txt` | Detailed file metadata |

---

## Creating Files & Directories

### Creating Files

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `touch` | Create empty file or update timestamp | `touch file.txt` | Create new file |
| `touch file1 file2` | Create multiple files | `touch file1.txt file2.txt` | Multiple files at once |
| `> file` | Create empty file (redirect) | `> newfile.txt` | Quick empty file |
| `echo "text" > file` | Create file with content | `echo "Hello" > file.txt` | File with initial content |

### Creating Directories

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `mkdir` | Create directory | `mkdir documents` | Single directory |
| `mkdir -p` | Create parent directories | `mkdir -p dir1/dir2/dir3` | Nested directories |
| `mkdir -m` | Create with permissions | `mkdir -m 755 mydir` | Set permissions at creation |
| `mkdir dir1 dir2` | Create multiple directories | `mkdir docs projects backups` | Multiple directories |

### mkdir Options

| Option | Description | Example |
|--------|-------------|---------|
| `-p` | Create parent directories as needed | `mkdir -p a/b/c` |
| `-m` | Set permissions | `mkdir -m 700 private` |
| `-v` | Verbose (show what's being created) | `mkdir -v newdir` |

---

## Copying Files

### Copy Commands

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `cp source dest` | Copy file | `cp file.txt backup.txt` | Duplicate file |
| `cp file1 file2 dir/` | Copy multiple files | `cp *.txt documents/` | Multiple files to directory |
| `cp -r dir1 dir2` | Copy directory recursively | `cp -r projects/ backup/` | Copy entire directory tree |
| `cp -i` | Interactive (prompt before overwrite) | `cp -i file.txt dest/` | Prevent accidental overwrites |
| `cp -u` | Update (copy only if newer) | `cp -u source dest` | Backup only changed files |
| `cp -v` | Verbose (show progress) | `cp -v file.txt dest/` | See what's being copied |
| `cp -p` | Preserve attributes | `cp -p file.txt dest/` | Keep timestamps, permissions |

### cp Options

| Option | Description | Example |
|--------|-------------|---------|
| `-r` or `-R` | Recursive (for directories) | `cp -r dir1/ dir2/` |
| `-i` | Interactive (confirm overwrites) | `cp -i file.txt dest/` |
| `-f` | Force (overwrite without asking) | `cp -f file.txt dest/` |
| `-u` | Update (copy only if newer) | `cp -u source dest` |
| `-v` | Verbose | `cp -v file.txt dest/` |
| `-p` | Preserve mode, ownership, timestamps | `cp -p file.txt dest/` |
| `-a` | Archive (same as `-dpR`, preserve all) | `cp -a dir1/ dir2/` |
| `-n` | No clobber (don't overwrite) | `cp -n file.txt dest/` |

### Copy Examples

| Task | Command |
|------|---------|
| Copy file to directory | `cp file.txt /tmp/` |
| Copy and rename | `cp file.txt newname.txt` |
| Copy all text files | `cp *.txt documents/` |
| Copy directory | `cp -r projects/ backup/` |
| Backup with timestamp | `cp file.txt file.txt.$(date +%Y%m%d)` |

---

## Moving & Renaming

### Move/Rename Commands

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `mv source dest` | Move or rename file | `mv file.txt newname.txt` | Rename file |
| `mv file dir/` | Move file to directory | `mv file.txt documents/` | Move to folder |
| `mv file1 file2 dir/` | Move multiple files | `mv *.txt documents/` | Move many files |
| `mv -i` | Interactive (prompt before overwrite) | `mv -i file.txt dest/` | Prevent overwrites |
| `mv -u` | Update (move only if newer) | `mv -u source dest` | Update files only |
| `mv -v` | Verbose (show progress) | `mv -v file.txt dest/` | See what's being moved |
| `mv -n` | No clobber (don't overwrite) | `mv -n file.txt dest/` | Safe move |

### mv Options

| Option | Description | Example |
|--------|-------------|---------|
| `-i` | Interactive (confirm overwrites) | `mv -i file.txt dest/` |
| `-f` | Force (overwrite without asking) | `mv -f file.txt dest/` |
| `-u` | Update (move only if newer) | `mv -u source dest` |
| `-v` | Verbose | `mv -v file.txt dest/` |
| `-n` | No clobber (don't overwrite) | `mv -n file.txt dest/` |

### Move/Rename Examples

| Task | Command |
|------|---------|
| Rename file | `mv oldname.txt newname.txt` |
| Move file | `mv file.txt /tmp/` |
| Move directory | `mv projects/ /backup/` |
| Move all text files | `mv *.txt documents/` |
| Rename directory | `mv old_folder new_folder` |

---

## Deleting Files

### Delete Commands

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `rm file` | Remove file | `rm file.txt` | Delete single file |
| `rm file1 file2` | Remove multiple files | `rm file1.txt file2.txt` | Delete multiple files |
| `rm -r dir` | Remove directory recursively | `rm -r directory/` | Delete directory and contents |
| `rm -i` | Interactive (confirm each deletion) | `rm -i file.txt` | Safe deletion |
| `rm -f` | Force (no confirmation) | `rm -f file.txt` | Force delete |
| `rm -rf dir` | Force remove directory | `rm -rf directory/` | Delete directory forcefully |
| `rm -v` | Verbose (show deleted files) | `rm -v file.txt` | See what's deleted |
| `rmdir` | Remove empty directory only | `rmdir emptydir/` | Delete only if empty |

### rm Options

| Option | Description | Example | Warning Level |
|--------|-------------|---------|---------------|
| `-r` or `-R` | Recursive (for directories) | `rm -r dir/` | High |
| `-i` | Interactive (confirm each) | `rm -i file.txt` | Safe |
| `-f` | Force (no confirmation) | `rm -f file.txt` | Very High |
| `-v` | Verbose | `rm -v file.txt` | Info only |
| `-I` | Prompt once before removing many | `rm -I *.txt` | Medium |
| `-d` | Remove empty directories | `rm -d emptydir/` | Low |

### ⚠️ Dangerous Commands - NEVER RUN!

| Command | Why Dangerous | Result |
|---------|---------------|--------|
| `rm -rf /` | Deletes entire system | System destroyed |
| `rm -rf /*` | Deletes everything in root | System destroyed |
| `rm -rf ~` | Deletes your entire home | All personal files lost |
| `rm -rf .` | Deletes current directory | All files in current dir lost |
| `rm -rf *` | Deletes all in current directory | Everything in directory lost |

### Safe Deletion Practices

| Practice | Command | Purpose |
|----------|---------|---------|
| Use `-i` flag | `rm -i file.txt` | Confirm before deletion |
| List first | `ls file.txt`, then `rm file.txt` | Verify file before deletion |
| Use trash | `trash file.txt` (if installed) | Recoverable deletion |
| Make backups | `cp file.txt file.txt.backup` | Keep backup before deletion |

---

## Finding Files

### Find Command

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `find path -name` | Find by name | `find /home -name "*.txt"` | Search by filename |
| `find path -iname` | Find case-insensitive | `find /home -iname "file.txt"` | Ignore case |
| `find path -type` | Find by type | `find /home -type f` | Find files only (`f`=file, `d`=directory) |
| `find path -size` | Find by size | `find /home -size +100M` | Files larger than 100MB |
| `find path -mtime` | Find by modification time | `find /home -mtime -7` | Modified in last 7 days |
| `find path -user` | Find by owner | `find /home -user john` | Files owned by john |
| `find path -perm` | Find by permissions | `find /home -perm 777` | Files with 777 permissions |

### find Options

| Option | Description | Example |
|--------|-------------|---------|
| `-name pattern` | Find by exact name | `find . -name "file.txt"` |
| `-iname pattern` | Find case-insensitive | `find . -iname "*.TXT"` |
| `-type f` | Files only | `find . -type f` |
| `-type d` | Directories only | `find . -type d` |
| `-type l` | Symbolic links only | `find . -type l` |
| `-size +100M` | Larger than 100MB | `find . -size +100M` |
| `-size -1k` | Smaller than 1KB | `find . -size -1k` |
| `-mtime -7` | Modified in last 7 days | `find . -mtime -7` |
| `-mtime +30` | Modified more than 30 days ago | `find . -mtime +30` |
| `-user username` | Owned by user | `find . -user john` |
| `-perm 777` | Exact permissions | `find . -perm 777` |
| `-empty` | Empty files or directories | `find . -empty` |

### find Actions

| Action | Description | Example |
|--------|-------------|---------|
| `-exec command {} \;` | Execute command on results | `find . -name "*.txt" -exec cat {} \;` |
| `-delete` | Delete found files | `find . -name "*.tmp" -delete` |
| `-ls` | List found files in detail | `find . -name "*.txt" -ls` |
| `-print` | Print filenames (default) | `find . -name "*.txt" -print` |

### locate Command

| Command | Description | Example | Notes |
|---------|-------------|---------|-------|
| `locate filename` | Find file in database | `locate file.txt` | Fast but may be outdated |
| `locate -i` | Case-insensitive | `locate -i FiLe.TxT` | Ignore case |
| `updatedb` | Update locate database | `sudo updatedb` | Run before using locate |

### which and whereis

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `which` | Find command location | `which python` | Shows `/usr/bin/python` |
| `whereis` | Find binary, source, manual | `whereis ls` | Shows binary and man page locations |

---

## File Permissions

### Understanding Permissions

| Permission | Symbol | Numeric | On Files | On Directories |
|------------|--------|---------|----------|----------------|
| **Read** | `r` | 4 | View contents | List contents |
| **Write** | `w` | 2 | Modify contents | Create/delete files |
| **Execute** | `x` | 1 | Run as program | Enter directory |
| **None** | `-` | 0 | No access | No access |

### Permission Groups

| Group | Description | Example |
|-------|-------------|---------|
| **Owner (u)** | File owner | `rwx` (7) |
| **Group (g)** | File's group | `r-x` (5) |
| **Others (o)** | Everyone else | `r--` (4) |

### chmod - Change Permissions

| Method | Command | Description |
|--------|---------|-------------|
| **Numeric** | `chmod 755 file` | Owner: rwx, Group: r-x, Others: r-x |
| **Symbolic** | `chmod u+x file` | Add execute for owner |
| **Symbolic** | `chmod g-w file` | Remove write for group |
| **Symbolic** | `chmod o=r file` | Set others to read only |

### chmod Numeric Examples

| Numeric | Symbolic | Description | Common Use |
|---------|----------|-------------|------------|
| `777` | `rwxrwxrwx` | Full access for all | ⚠️ Dangerous - avoid! |
| `755` | `rwxr-xr-x` | Owner full, others read/execute | Executable scripts |
| `644` | `rw-r--r--` | Owner read/write, others read | Regular files |
| `600` | `rw-------` | Owner read/write only | Private files, SSH keys |
| `700` | `rwx------` | Owner full access only | Private directories |
| `664` | `rw-rw-r--` | Owner/group read/write, others read | Shared documents |

### chmod Symbolic Examples

| Command | Description |
|---------|-------------|
| `chmod u+x file` | Add execute permission for owner |
| `chmod g-w file` | Remove write permission from group |
| `chmod o-r file` | Remove read permission from others |
| `chmod a+r file` | Add read for all (owner, group, others) |
| `chmod u=rwx,g=rx,o=r file` | Set specific permissions |
| `chmod -R 755 dir/` | Set permissions recursively |

### chown - Change Ownership

| Command | Description | Example |
|---------|-------------|---------|
| `chown user file` | Change owner | `sudo chown john file.txt` |
| `chown user:group file` | Change owner and group | `sudo chown john:developers file.txt` |
| `chown :group file` | Change group only | `sudo chown :developers file.txt` |
| `chown -R user dir/` | Change recursively | `sudo chown -R john:john /home/john` |

### chgrp - Change Group

| Command | Description | Example |
|---------|-------------|---------|
| `chgrp group file` | Change group | `sudo chgrp developers file.txt` |
| `chgrp -R group dir/` | Change group recursively | `sudo chgrp -R developers /var/www` |

---

## File Compression

### tar - Archive Files

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `tar -cf` | Create archive | `tar -cf archive.tar files/` | Create uncompressed archive |
| `tar -czf` | Create gzip archive | `tar -czf archive.tar.gz files/` | Create compressed archive (gzip) |
| `tar -cjf` | Create bzip2 archive | `tar -cjf archive.tar.bz2 files/` | Create compressed archive (bzip2) |
| `tar -xf` | Extract archive | `tar -xf archive.tar` | Extract archive |
| `tar -xzf` | Extract gzip archive | `tar -xzf archive.tar.gz` | Extract gzip archive |
| `tar -xjf` | Extract bzip2 archive | `tar -xjf archive.tar.bz2` | Extract bzip2 archive |
| `tar -tf` | List archive contents | `tar -tf archive.tar` | View without extracting |
| `tar -xf -C` | Extract to directory | `tar -xf archive.tar -C /tmp/` | Extract to specific location |

### tar Options

| Option | Description | Example |
|--------|-------------|---------|
| `-c` | Create archive | `tar -cf archive.tar files/` |
| `-x` | Extract archive | `tar -xf archive.tar` |
| `-t` | List contents | `tar -tf archive.tar` |
| `-f` | Specify filename | `tar -cf archive.tar` |
| `-z` | Use gzip compression | `tar -czf archive.tar.gz` |
| `-j` | Use bzip2 compression | `tar -cjf archive.tar.bz2` |
| `-v` | Verbose (show progress) | `tar -czvf archive.tar.gz files/` |
| `-r` | Append to archive | `tar -rf archive.tar newfile` |
| `-C` | Change to directory | `tar -xf archive.tar -C /tmp/` |

### gzip/gunzip

| Command | Description | Example | Result |
|---------|-------------|---------|--------|
| `gzip file` | Compress file | `gzip file.txt` | Creates `file.txt.gz`, deletes original |
| `gzip -k file` | Compress and keep original | `gzip -k file.txt` | Creates `file.txt.gz`, keeps original |
| `gunzip file.gz` | Decompress file | `gunzip file.txt.gz` | Creates `file.txt`, deletes `.gz` |
| `gzip -d file.gz` | Decompress (alternative) | `gzip -d file.txt.gz` | Same as gunzip |
| `gzip -r dir/` | Compress directory recursively | `gzip -r documents/` | Compresses all files in directory |

### zip/unzip

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `zip archive.zip files` | Create zip archive | `zip archive.zip file1 file2` | Create zip file |
| `zip -r archive.zip dir/` | Zip directory recursively | `zip -r archive.zip documents/` | Zip entire directory |
| `unzip archive.zip` | Extract zip archive | `unzip archive.zip` | Extract to current directory |
| `unzip archive.zip -d dir/` | Extract to directory | `unzip archive.zip -d /tmp/` | Extract to specific location |
| `unzip -l archive.zip` | List contents | `unzip -l archive.zip` | View without extracting |

### Compression Comparison

| Format | Command | Extension | Compression | Speed | Common Use |
|--------|---------|-----------|-------------|-------|------------|
| **tar** | `tar -cf` | `.tar` | None | Fast | Archiving without compression |
| **gzip** | `tar -czf` | `.tar.gz` | Good | Medium | Most common in Linux |
| **bzip2** | `tar -cjf` | `.tar.bz2` | Better | Slow | Better compression ratio |
| **xz** | `tar -cJf` | `.tar.xz` | Best | Slowest | Maximum compression |
| **zip** | `zip` | `.zip` | Good | Fast | Cross-platform compatibility |

---

## File Content Operations

### Searching in Files

| Command | Description | Example | Use Case |
|---------|-------------|---------|----------|
| `grep pattern file` | Search for pattern | `grep "error" logfile.txt` | Find text in file |
| `grep -i` | Case-insensitive search | `grep -i "error" file.txt` | Ignore case |
| `grep -r` | Recursive search | `grep -r "error" /var/log/` | Search in directories |
| `grep -n` | Show line numbers | `grep -n "error" file.txt` | See line numbers |
| `grep -v` | Invert match (exclude) | `grep -v "debug" file.txt` | Show lines NOT matching |
| `grep -c` | Count matches | `grep -c "error" file.txt` | Count occurrences |
| `grep -l` | List files with matches | `grep -l "error" *.txt` | Show filenames only |
| `grep -w` | Match whole word | `grep -w "error" file.txt` | Match exact word |

### grep Options

| Option | Description | Example |
|
