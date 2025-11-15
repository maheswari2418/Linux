# 📁 Linux Folder Structure - Simple Guide

> Easy-to-understand guide using tables only

---

## 📑 Table of Contents

| Section | Topic |
|---------|-------|
| 1 | [What is Linux Filesystem?](#1-what-is-linux-filesystem) |
| 2 | [Windows vs Linux](#2-windows-vs-linux) |
| 3 | [Linked Folders](#3-linked-folders) |
| 4 | [System Folders](#4-system-folders) |
| 5 | [User Folders](#5-user-folders) |
| 6 | [Temporary Folders](#6-temporary-folders) |
| 7 | [Device Folders](#7-device-folders) |
| 8 | [Mount Points](#8-mount-points) |
| 9 | [Complete Directory List](#9-complete-directory-list) |
| 10 | [Safety Guide](#10-safety-guide) |
| 11 | [Common Commands](#11-common-commands) |
| 12 | [Quick Reference](#12-quick-reference) |

---

## 1. What is Linux Filesystem?

| Concept | Explanation |
|---------|-------------|
| **Root Directory** | Everything starts from `/` (the root) - like the trunk of a tree |
| **Single Tree** | All folders branch from one starting point, not multiple drives |
| **Case Sensitive** | `File.txt` and `file.txt` are different files |
| **Organization** | Folders organized by purpose, not random names |

---

## 2. Windows vs Linux

| Feature | Windows | Linux |
|---------|---------|-------|
| **Multiple Drives** | C:\, D:\, E:\ | Only `/` (root) |
| **Your Files** | C:\Users\YourName | /home/yourname |
| **Programs** | C:\Program Files | /usr |
| **Settings** | Control Panel | /etc |
| **Temporary** | C:\Temp | /tmp |
| **Logs** | C:\Windows\Logs | /var/log |

---

## 3. Linked Folders

| Folder | Points To | What It Contains | Why It Exists |
|--------|-----------|------------------|---------------|
| `/bin` | → `/usr/bin` | Basic commands like `ls`, `cp`, `cat` | Old programs expect `/bin` to exist |
| `/sbin` | → `/usr/sbin` | Admin commands like `reboot`, `shutdown` | Backward compatibility with old scripts |
| `/lib` | → `/usr/lib` | Program libraries and modules | System programs look here for libraries |

### How to Check

| Command | What It Shows |
|---------|---------------|
| `ls -l /bin` | Shows it's a link to /usr/bin |
| `ls -l /sbin` | Shows it's a link to /usr/sbin |
| `ls -l /lib` | Shows it's a link to /usr/lib |

---

## 4. System Folders

| Folder | What's Inside | Like Windows | Can You Delete? | Example Files |
|--------|---------------|--------------|-----------------|---------------|
| `/boot` | Files to start computer | Boot files | ❌ Never | `vmlinuz` (kernel) |
| `/etc` | System settings | Control Panel | ❌ Never | `passwd`, `hosts`, `ssh/` |
| `/usr` | Installed programs | C:\Program Files | ❌ Never | Firefox, Python, Games |
| `/var` | Changing files (logs, emails) | C:\ProgramData | ⚠️ Carefully | Logs, databases, websites |

### What Each Folder Does

| Folder | Real-World Analogy | When You Need It |
|--------|-------------------|------------------|
| `/boot` | Car ignition | Computer won't start |
| `/etc` | Settings menu | Need to change WiFi, users, services |
| `/usr` | App store | Want to use installed programs |
| `/var` | Filing cabinet | Looking for logs, checking emails |

### Useful Commands

| Task | Command | Example |
|------|---------|---------|
| View boot files | `ls /boot` | See kernel versions |
| Check settings | `ls /etc` | View config files |
| List programs | `ls /usr/bin` | See installed commands |
| Check logs | `ls /var/log` | Find error logs |

---

## 5. User Folders

| Folder | What's Inside | Like Windows | Who Can Access | Size |
|--------|---------------|--------------|----------------|------|
| `/home` | Your personal files | C:\Users | Each user their own | Grows with use |
| `/root` | Administrator's files | C:\Users\Administrator | Only root user | Small |
| `/opt` | Manually installed programs | C:\Program Files | All users | Varies |
| `/srv` | Server data (websites) | C:\inetpub | Service accounts | Varies |

### Your Home Folder Structure

| Subfolder | What Goes Here | Example |
|-----------|----------------|---------|
| `/home/yourname/Documents` | Your documents | Reports, PDFs |
| `/home/yourname/Downloads` | Downloaded files | ISOs, installers |
| `/home/yourname/Pictures` | Photos and images | vacation.jpg |
| `/home/yourname/Music` | Audio files | songs.mp3 |
| `/home/yourname/Desktop` | Desktop files | shortcuts |

### Common Tasks

| Task | Command | What It Does |
|------|---------|--------------|
| Go to home | `cd ~` | Takes you to /home/yourname |
| List home contents | `ls ~` | Shows your files |
| Check home size | `du -sh ~` | See how much space you're using |
| List all users | `ls /home` | See all user folders |

---

## 6. Temporary Folders

| Folder | What's Inside | Stored On | Deleted When | Use For |
|--------|---------------|-----------|--------------|---------|
| `/tmp` | Temporary files from apps | Disk | Computer restarts | Quick downloads, temp processing |
| `/run` | Running program info | RAM | Computer restarts | PID files, sockets |
| `/proc` | Live process info | RAM (Virtual) | Never (auto-updated) | Check CPU, memory, processes |
| `/sys` | Hardware info | RAM (Virtual) | Never (auto-updated) | Check USB, network cards |
| `/dev` | Device files | Special | Never | Access hard drives, USB |

### Virtual vs Real Folders

| Folder | Real or Virtual? | Uses Disk Space? | What It Shows |
|--------|------------------|------------------|---------------|
| `/tmp` | Real | ✅ Yes | Actual temporary files |
| `/run` | Virtual (RAM) | ❌ No | Current running programs |
| `/proc` | Virtual (RAM) | ❌ No | Live system information |
| `/sys` | Virtual (RAM) | ❌ No | Hardware status |
| `/dev` | Special | ❌ No | Device access points |

### Useful Information Commands

| What You Want | Command | Example Output |
|---------------|---------|----------------|
| CPU info | `cat /proc/cpuinfo` | Processor details |
| Memory info | `cat /proc/meminfo` | RAM usage |
| All processes | `ls /proc` | Numbers (PIDs) |
| USB devices | `ls /dev/sd*` | sda, sdb, sdc |
| Network cards | `ls /sys/class/net` | eth0, wlan0 |

---

## 7. Device Folders

| Folder | Purpose | Contains | Can You Edit? |
|--------|---------|----------|---------------|
| `/dev` | Access to all devices | Hard drives, USB, keyboard files | ❌ No (system managed) |
| `/run` | Running program data | PID files, lock files, sockets | ⚠️ Only if you know what you're doing |

### Common Device Files

| Device File | What It Is | Example Use |
|-------------|------------|-------------|
| `/dev/sda` | First hard drive | Main system disk |
| `/dev/sda1` | First partition | Main partition |
| `/dev/sdb` | Second hard drive | External USB |
| `/dev/null` | Trash bin | Discard output: `command > /dev/null` |
| `/dev/zero` | Source of zeros | Create empty files |
| `/dev/random` | Random numbers | Generate passwords |

### Device Commands

| Task | Command | What It Does |
|------|---------|--------------|
| List all drives | `lsblk` | Shows all disks and partitions |
| View device files | `ls -l /dev/sd*` | Lists storage devices |
| Check USB | `ls /dev/disk/by-id/usb-*` | Shows USB devices |
| Send to trash | `echo "test" > /dev/null` | Output disappears |

---

## 8. Mount Points

| Folder | Purpose | When Used | Automatic? |
|--------|---------|-----------|------------|
| `/mnt` | Manual mounting | You plug in external drive manually | ❌ No - you control it |
| `/media` | Automatic mounting | System detects USB and mounts it here | ✅ Yes - system does it |
| `/data` | Custom storage | Docker containers, Windows WSL mounts | Depends on setup |

### Mount Point Examples

| Scenario | Windows Shows | Linux Shows | How to Access |
|----------|---------------|-------------|---------------|
| USB drive plugged in | E:\ | /media/john/USB_DRIVE | `cd /media/john/USB_DRIVE` |
| External hard drive | F:\ | /mnt/external | `cd /mnt/external` |
| Windows C: in WSL | C:\ | /mnt/c | `cd /mnt/c` |
| Docker volume | N/A | /data/myapp | `cd /data/myapp` |

### Mounting Commands

| Task | Command | When to Use |
|------|---------|-------------|
| See all mounts | `df -h` | Check what's connected |
| Mount manually | `sudo mount /dev/sdb1 /mnt/usb` | Connect external drive |
| Unmount (safe eject) | `sudo umount /mnt/usb` | Before unplugging USB |
| Check what's using mount | `lsof /mnt/usb` | If unmount fails |
| List media mounts | `ls /media/$USER` | See auto-mounted devices |

---

## 9. Complete Directory List

| Folder | Simple Explanation | Windows Similar | Important? | Size |
|--------|-------------------|-----------------|------------|------|
| `/` | Root - starting point of everything | C:\ | ⭐⭐⭐⭐⭐ | N/A |
| `/home` | Your personal files | C:\Users\YourName | ⭐⭐⭐⭐⭐ | Large |
| `/root` | Admin's personal files | C:\Users\Administrator | ⭐⭐⭐⭐ | Small |
| `/etc` | System settings | Control Panel configs | ⭐⭐⭐⭐⭐ | Small |
| `/usr` | Installed programs | C:\Program Files | ⭐⭐⭐⭐⭐ | Very Large |
| `/var` | Logs, databases, emails | C:\ProgramData | ⭐⭐⭐⭐ | Medium-Large |
| `/tmp` | Temporary files | C:\Temp | ⭐⭐ | Medium |
| `/boot` | Startup files | Boot folder | ⭐⭐⭐⭐⭐ | Small |
| `/opt` | Extra software | C:\Program Files (x86) | ⭐⭐⭐ | Medium |
| `/mnt` | Manual mount point | N/A | ⭐⭐ | N/A |
| `/media` | Auto mount point | E:\, F:\ (drives) | ⭐⭐⭐ | N/A |
| `/dev` | Device files | Device Manager | ⭐⭐⭐⭐ | Virtual |
| `/proc` | Process info | Task Manager data | ⭐⭐⭐ | Virtual |
| `/sys` | Hardware info | Device Manager data | ⭐⭐⭐ | Virtual |
| `/run` | Running program data | N/A | ⭐⭐ | Virtual |
| `/srv` | Server data | C:\inetpub | ⭐⭐ | Varies |
| `/bin` | Commands (link) | C:\Windows\System32 | ⭐⭐⭐⭐ | Link |
| `/sbin` | Admin commands (link) | C:\Windows\System32 | ⭐⭐⭐⭐ | Link |
| `/lib` | Libraries (link) | C:\Windows\System32 | ⭐⭐⭐⭐ | Link |

---

## 10. Safety Guide

### What You Can Do

| Folder | Can Explore? | Can Create Files? | Can Delete Files? | Notes |
|--------|--------------|-------------------|-------------------|-------|
| `/home/yourname` | ✅ Yes | ✅ Yes | ✅ Yes | Your safe space! |
| `/tmp` | ✅ Yes | ✅ Yes | ✅ Yes | Deleted on restart anyway |
| `/media` | ✅ Yes | ✅ Yes (on your devices) | ✅ Yes (on your devices) | Only your USB drives |

### What Needs Permission (sudo)

| Folder | Can View? | Can Edit? | Risk Level | What Happens If You Break It |
|--------|-----------|-----------|------------|------------------------------|
| `/etc` | ✅ Yes | ⚠️ With sudo | 🔴 High | System won't start, services fail |
| `/usr` | ✅ Yes | ⚠️ With sudo | 🔴 High | Programs won't work |
| `/var` | ✅ Yes | ⚠️ With sudo | 🟡 Medium | Logs lost, services fail |
| `/opt` | ✅ Yes | ⚠️ With sudo | 🟡 Medium | Installed apps break |
| `/boot` | ✅ Yes | ⚠️ With sudo | 🔴 Critical | Computer won't boot |

### Never Touch These

| Folder | Why Not? | What Could Go Wrong |
|--------|----------|---------------------|
| `/proc` | Virtual files - system managed | Nothing (you can't actually edit them) |
| `/sys` | Virtual files - system managed | Could crash hardware drivers |
| `/dev` | Device files - system managed | Could break device access |

### DO's and DON'Ts

| ✅ DO | ❌ DON'T |
|-------|----------|
| Keep files in `/home/yourname` | Delete anything from `/boot` |
| Backup `/home` regularly | Edit `/etc` without backup |
| Clean `/tmp` when disk is full | Remove files from `/dev` |
| Ask before using `sudo` | Use `rm -rf /` (deletes everything!) |
| Learn before you delete | Randomly delete system folders |

---

## 11. Common Commands

### Navigation Commands

| Task | Command | Example | Result |
|------|---------|---------|--------|
| Where am I? | `pwd` | `pwd` | Shows `/home/john` |
| Go home | `cd ~` | `cd ~` | Takes you to home folder |
| Go to folder | `cd /path` | `cd /var/log` | Changes to /var/log |
| Go up one level | `cd ..` | `cd ..` | Goes to parent folder |
| List files | `ls` | `ls /etc` | Shows files in /etc |
| List with details | `ls -lah` | `ls -lah /home` | Shows size, permissions, hidden files |

### Information Commands

| What You Want | Command | Example Output |
|---------------|---------|----------------|
| Disk space | `df -h` | Shows free space on all drives |
| Folder size | `du -sh /folder` | Shows size like "2.5G" |
| All folder sizes | `du -sh /*` | Size of each top-level folder |
| System info | `uname -a` | Linux version, kernel info |
| CPU info | `cat /proc/cpuinfo` | Processor details |
| Memory info | `free -h` | RAM usage |

### File Operations

| Task | Command | Example | What It Does |
|------|---------|---------|--------------|
| Copy file | `cp source dest` | `cp file.txt /tmp/` | Copies file to /tmp |
| Move file | `mv old new` | `mv file.txt Documents/` | Moves file to Documents |
| Delete file | `rm file` | `rm old.txt` | Deletes file |
| Create folder | `mkdir folder` | `mkdir ~/projects` | Creates new folder |
| View file | `cat file` | `cat /etc/hostname` | Shows file contents |

### Search Commands

| What to Find | Command | Example |
|--------------|---------|---------|
| Find file by name | `find /path -name "name"` | `find /home -name "*.txt"` |
| Find large files | `find /path -size +100M` | `find ~ -size +100M` |
| Find in /etc | `ls /etc | grep word` | `ls /etc | grep ssh` |

---

## 12. Quick Reference

### One-Line Explanations

| Folder | One-Line Summary |
|--------|-----------------|
| `/home` | Your files live here |
| `/etc` | Settings for everything |
| `/var` | Logs and changing data |
| `/usr` | Programs you can run |
| `/tmp` | Temporary scratch space |
| `/boot` | Files to start computer |
| `/dev` | Talk to hardware |
| `/proc` | Live system information |
| `/root` | Admin's home folder |
| `/opt` | Extra installed software |

### By Purpose

| Purpose | Folders to Check |
|---------|-----------------|
| Looking for your files | `/home/yourname` |
| Need to check logs | `/var/log` |
| Want to change settings | `/etc` |
| Computer won't boot | `/boot` |
| Check running programs | `/proc` |
| See hardware devices | `/dev`, `/sys` |
| Access USB drive | `/media/yourname` |
| Install program manually | `/opt` |

### By Safety Level

| Safety Level | Folders | Can You Break System? |
|--------------|---------|----------------------|
| 🟢 Safe | `/home`, `/tmp` | No |
| 🟡 Careful | `/opt`, `/srv` | Unlikely |
| 🟠 Needs sudo | `/etc`, `/var` | Yes, if careless |
| 🔴 Critical | `/boot`, `/usr` | Yes, easily |
| ⚫ Virtual | `/proc`, `/sys`, `/dev` | System-managed |

---

## 📝 Final Summary

### The 5 Most Important Folders

| # | Folder | Why Important | What's Inside |
|---|--------|---------------|---------------|
| 1 | `/home` | Your personal space | Documents, photos, downloads |
| 2 | `/etc` | System brain | All settings and configurations |
| 3 | `/var` | Problem solver | Logs help you fix issues |
| 4 | `/usr` | Where programs live | Everything you run |
| 5 | `/boot` | Computer starter | Without it, nothing works |

### Remember These Rules

| Rule | Why It Matters |
|------|----------------|
| Stay in `/home` for your work | Safe from breaking system |
| Need `sudo` for system folders | Linux protects important files |
| `/tmp` gets cleaned automatically | Don't store important files there |
| Check `/var/log` when things break | Logs tell you what went wrong |
| Backup `/home` regularly | Only folder with your personal data |

