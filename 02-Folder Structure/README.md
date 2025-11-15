# 📁 Linux Folder Structure

> Complete guide to Linux directory hierarchy

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Overview](#overview) | Introduction to Linux filesystem |
| [Root Directory (/)](#root-directory-) | The starting point |
| [Symbolic Links](#symbolic-links) | Linked directories |
| [System Directories](#system-directories) | Core system folders |
| [User Directories](#user-directories) | User and application folders |
| [Temporary & Virtual](#temporary--virtual-directories) | Temporary and virtual filesystems |
| [Device & Runtime](#device--runtime-directories) | Device and runtime data |
| [Mount Points](#mount-points) | External filesystem connections |
| [Complete Tree](#complete-directory-tree) | Full hierarchy visualization |

---

## Overview

### Linux vs Windows Filesystem

| Feature | Linux | Windows |
|---------|-------|---------|
| **Root Structure** | Single root `/` | Multiple drives (C:, D:, E:) |
| **Path Separator** | Forward slash `/` | Backslash `\` |
| **Case Sensitivity** | Yes (`File.txt` ≠ `file.txt`) | No (`File.txt` = `file.txt`) |
| **Drive Letters** | None | C:, D:, E:, etc. |

### Key Principles

| Principle | Explanation |
|-----------|-------------|
| **Everything is a file** | Devices, directories, processes are treated as files |
| **Single root** | All directories branch from `/` (root) |
| **Hierarchical structure** | Tree-like organization |
| **Standard layout** | Follows Filesystem Hierarchy Standard (FHS) |

---

## Root Directory (/)

### Root (`/`) - The Starting Point

| Attribute | Description |
|-----------|-------------|
| **Symbol** | `/` |
| **Name** | Root directory |
| **Parent** | None (top of hierarchy) |
| **Purpose** | Starting point for all files and directories |
| **Equivalent in Windows** | Similar to `C:\` but includes everything |

---

## Symbolic Links

### Symlinked Directories (Less Significant)

| Directory | Links To | Purpose | Type |
|-----------|----------|---------|------|
| `/bin` | `/usr/bin` | Essential user command binaries | Symlink |
| `/sbin` | `/usr/sbin` | System administrator binaries | Symlink |
| `/lib` | `/usr/lib` | Shared libraries for `/bin` and `/sbin` | Symlink |
| `/lib64` | `/usr/lib64` | 64-bit shared libraries | Symlink |

### Why Symlinks Exist

| Reason | Explanation |
|--------|-------------|
| **Backward compatibility** | Old scripts expect these paths |
| **Modernization** | Modern systems consolidated binaries into `/usr` |
| **FHS compliance** | Maintains compatibility with Filesystem Hierarchy Standard |

---

## System Directories

### Important System Directories

| Directory | Description | Contents |
|-----------|-------------|----------|
| `/boot` | Boot loader files | Kernel (`vmlinuz`), initrd, GRUB config |
| `/etc` | System configuration files | Config files, startup scripts |
| `/usr` | User programs and data | Applications, libraries, documentation |
| `/var` | Variable data | Logs, caches, databases, mail spools |

### `/boot` - Boot Files

| File/Directory | Purpose |
|----------------|---------|
| `vmlinuz` | Compressed Linux kernel |
| `initrd.img` | Initial RAM disk for boot |
| `grub/` | GRUB bootloader configuration |
| `System.map` | Kernel symbol table |
| `config-*` | Kernel configuration file |

### `/etc` - Configuration Files

| File/Directory | Purpose |
|----------------|---------|
| `passwd` | User account information |
| `shadow` | Encrypted user passwords |
| `group` | Group information |
| `hosts` | Static hostname to IP mapping |
| `fstab` | Filesystem mount configuration |
| `hostname` | System hostname |
| `resolv.conf` | DNS resolver configuration |
| `ssh/` | SSH server configuration |
| `systemd/` | Systemd service configurations |
| `network/` | Network configuration files |

### `/usr` - User Programs

| Subdirectory | Purpose | Contents |
|--------------|---------|----------|
| `/usr/bin` | User commands | Common programs (`ls`, `cp`, `python`) |
| `/usr/sbin` | System binaries | Admin commands (`useradd`, `fdisk`) |
| `/usr/lib` | Program libraries | Shared libraries for binaries |
| `/usr/local` | Locally installed software | User-compiled programs |
| `/usr/share` | Architecture-independent data | Documentation, icons, fonts |
| `/usr/src` | Source code | Kernel source, program sources |
| `/usr/include` | Header files | C/C++ header files |

### `/var` - Variable Data

| Subdirectory | Purpose | Contents |
|--------------|---------|----------|
| `/var/log` | System logs | `syslog`, `auth.log`, application logs |
| `/var/cache` | Application cache | Package cache, browser cache |
| `/var/tmp` | Temporary files | Preserved between reboots |
| `/var/spool` | Spool files | Print queues, mail queues |
| `/var/lib` | State information | Package databases, Docker data |
| `/var/www` | Web server content | Website files (Apache, Nginx) |
| `/var/mail` | User mailboxes | Email storage |

---

## User Directories

### User & Application-Specific Directories

| Directory | Description | Contents | Owner |
|-----------|-------------|----------|-------|
| `/home` | User home directories | Personal files, configs | Individual users |
| `/root` | Root user home directory | Root's personal files | Root only |
| `/opt` | Optional software | Third-party applications | Root |
| `/srv` | Service data | Web server, FTP data | Services |

### `/home` - User Home Directories

| Path | Purpose | Typical Contents |
|------|---------|------------------|
| `/home/username` | User's personal directory | Documents, Downloads, Pictures |
| `/home/username/.bashrc` | User's bash configuration | Shell settings |
| `/home/username/.ssh` | SSH keys and config | Private keys, known_hosts |
| `/home/username/.config` | Application configurations | App settings |
| `/home/username/Documents` | User documents | Files, PDFs |
| `/home/username/Downloads` | Downloaded files | Browser downloads |

### `/root` - Root User Home

| Attribute | Description |
|-----------|-------------|
| **Location** | `/root` |
| **Purpose** | Root (superuser) home directory |
| **Access** | Only root user |
| **Why separate?** | Available even if `/home` is unmounted |

### `/opt` - Optional Software

| Subdirectory | Example Applications |
|--------------|---------------------|
| `/opt/google` | Google Chrome |
| `/opt/lampp` | XAMPP server |
| `/opt/teamviewer` | TeamViewer |
| Custom apps | Self-contained applications |

### `/srv` - Service Data

| Service Type | Example Path | Purpose |
|--------------|-------------|---------|
| Web server | `/srv/www` | Website files |
| FTP server | `/srv/ftp` | FTP data |
| Git repositories | `/srv/git` | Git repos |

---

## Temporary & Virtual Directories

### Temporary & Virtual Filesystems

| Directory | Type | Storage | Cleared When | Purpose |
|-----------|------|---------|--------------|---------|
| `/tmp` | Temporary | Disk | On reboot | Temporary application files |
| `/run` | Runtime | RAM (tmpfs) | On reboot | Runtime process data |
| `/proc` | Virtual | RAM | Never (dynamic) | Process and kernel information |
| `/sys` | Virtual | RAM | Never (dynamic) | Hardware and kernel interfaces |
| `/dev` | Special | Special | Never | Device files |

### `/tmp` - Temporary Files

| Attribute | Value |
|-----------|-------|
| **Purpose** | Temporary file storage |
| **Permissions** | World-writable with sticky bit |
| **Persistence** | Cleared on reboot |
| **Use case** | Application temporary files |

### `/run` - Runtime Data

| Subdirectory | Contents |
|--------------|----------|
| `/run/lock` | Lock files |
| `/run/user` | User runtime data |
| `/run/systemd` | Systemd runtime data |
| PID files | Process ID files (e.g., `sshd.pid`) |

### `/proc` - Process Information

| Path | Information Provided |
|------|---------------------|
| `/proc/cpuinfo` | CPU information |
| `/proc/meminfo` | Memory information |
| `/proc/uptime` | System uptime |
| `/proc/version` | Kernel version |
| `/proc/[PID]` | Process-specific info (PID = process ID) |
| `/proc/filesystems` | Supported filesystems |
| `/proc/mounts` | Currently mounted filesystems |

### `/sys` - Hardware Information

| Subdirectory | Information |
|--------------|-------------|
| `/sys/block` | Block devices |
| `/sys/class` | Device classes (net, input, etc.) |
| `/sys/devices` | Physical device hierarchy |
| `/sys/kernel` | Kernel parameters |
| `/sys/module` | Loaded kernel modules |

---

## Device & Runtime Directories

### Device Files (`/dev`)

| Device Type | Examples | Purpose |
|-------------|----------|---------|
| **Block devices** | `/dev/sda`, `/dev/sdb` | Hard drives, SSDs |
| **Partitions** | `/dev/sda1`, `/dev/sda2` | Disk partitions |
| **Character devices** | `/dev/tty`, `/dev/null` | Terminals, special devices |
| **Special devices** | `/dev/zero`, `/dev/random` | Null, zero, random data |

### Common Device Files

| Device File | Description |
|-------------|-------------|
| `/dev/sda` | First SATA/SCSI disk |
| `/dev/sda1` | First partition on first disk |
| `/dev/sdb` | Second SATA/SCSI disk (often USB) |
| `/dev/nvme0n1` | NVMe SSD |
| `/dev/null` | Null device (discards all data) |
| `/dev/zero` | Provides infinite zeros |
| `/dev/random` | True random number generator |
| `/dev/urandom` | Pseudo-random number generator |
| `/dev/tty` | Current terminal |
| `/dev/loop0` | Loop device (mount files as disks) |

### Runtime Directory (`/run`)

| Type | Description |
|------|-------------|
| **Storage** | tmpfs (RAM-based) |
| **Persistence** | Cleared on boot |
| **Purpose** | Runtime variable data |
| **Replaced** | Old `/var/run` and `/var/lock` |

---

## Mount Points

### Filesystem Mount Points

| Directory | Purpose | Automatic? | Typical Use |
|-----------|---------|------------|-------------|
| `/mnt` | Temporary mount point | No (manual) | Admin mounts external filesystems |
| `/media` | Removable media | Yes (auto-mount) | USB drives, CDs, external drives |
| `/data` | Custom mount point | Varies | Persistent volumes, containers |

### `/mnt` - Manual Mounts

| Use Case | Example | Command |
|----------|---------|---------|
| Mount USB drive | `/mnt/usb` | `sudo mount /dev/sdb1 /mnt/usb` |
| Mount network share | `/mnt/nfs` | `sudo mount -t nfs server:/share /mnt/nfs` |
| Mount partition | `/mnt/backup` | `sudo mount /dev/sda2 /mnt/backup` |

### `/media` - Auto Mounts

| Scenario | Path | Description |
|----------|------|-------------|
| USB drive | `/media/username/USB_DRIVE` | Auto-mounted by system |
| External HDD | `/media/username/External_HDD` | Desktop environments handle this |
| SD card | `/media/username/SD_CARD` | Removable media |

### `/data` - Custom Mount Point

| Context | Use Case |
|---------|----------|
| **Docker containers** | Persistent volume mount |
| **WSL (Windows)** | Windows drive mount (e.g., `C:\ubuntu-data` → `/data`) |
| **Servers** | Large data partition |
| **Custom setup** | User-defined persistent storage |

---

## Complete Directory Tree

### Full Linux Filesystem Hierarchy

| Directory | Type | Description |
|-----------|------|-------------|
| `/` | Root | Base of filesystem tree |
| `/bin` | Symlink | → `/usr/bin` (essential binaries) |
| `/sbin` | Symlink | → `/usr/sbin` (system binaries) |
| `/lib` | Symlink | → `/usr/lib` (shared libraries) |
| `/boot` | Directory | Boot loader files |
| `/dev` | Special | Device files |
| `/etc` | Directory | Configuration files |
| `/home` | Directory | User home directories |
| `/root` | Directory | Root user home |
| `/media` | Directory | Removable media mounts |
| `/mnt` | Directory | Temporary mount point |
| `/opt` | Directory | Optional software |
| `/proc` | Virtual | Process information |
| `/run` | Virtual | Runtime data |
| `/srv` | Directory | Service data |
| `/sys` | Virtual | Hardware information |
| `/tmp` | Directory | Temporary files |
| `/usr` | Directory | User programs |
| `/var` | Directory | Variable data |

### ASCII Tree Representation

```
/                                   (Root Directory)
│
├── bin → usr/bin                   (Essential user binaries - symlink)
├── sbin → usr/sbin                 (System binaries - symlink)
├── lib → usr/lib                   (Shared libraries - symlink)
│
├── boot/                           (Boot loader files)
│   ├── vmlinuz                     (Linux kernel)
│   ├── initrd.img                  (Initial RAM disk)
│   └── grub/                       (GRUB bootloader)
│
├── dev/                            (Device files)
│   ├── sda                         (First disk)
│   ├── sda1                        (First partition)
│   ├── null                        (Null device)
│   └── random                      (Random generator)
│
├── etc/                            (Configuration files)
│   ├── passwd                      (User accounts)
│   ├── fstab                       (Mount points)
│   ├── hosts                       (Hostname mapping)
│   └── ssh/                        (SSH config)
│
├── home/                           (User directories)
│   ├── john/                       (User john)
│   │   ├── Documents/
│   │   ├── Downloads/
│   │   └── .bashrc
│   └── alice/                      (User alice)
│
├── root/                           (Root user home)
│
├── media/                          (Removable media)
│   └── username/
│       └── USB_DRIVE/
│
├── mnt/                            (Temporary mounts)
│
├── opt/                            (Optional software)
│   └── google/
│       └── chrome/
│
├── proc/                           (Process info - virtual)
│   ├── cpuinfo
│   ├── meminfo
│   └── [PID]/
│
├── run/                            (Runtime data - virtual)
│
├── srv/                            (Service data)
│   └── www/
│
├── sys/                            (Hardware info - virtual)
│   ├── block/
│   ├── class/
│   └── devices/
│
├── tmp/                            (Temporary files)
│
├── usr/                            (User programs)
│   ├── bin/                        (User commands)
│   ├── sbin/                       (System commands)
│   ├── lib/                        (Libraries)
│   ├── local/                      (Local installations)
│   ├── share/                      (Shared data)
│   └── src/                        (Source code)
│
└── var/                            (Variable data)
    ├── log/                        (Log files)
    ├── cache/                      (Application cache)
    ├── tmp/                        (Temp files)
    └── www/                        (Web content)
```

### Directory Categorization

| Category | Directories |
|----------|-------------|
| **Static binaries** | `/bin`, `/sbin`, `/lib`, `/usr` |
| **Configuration** | `/etc` |
| **User data** | `/home`, `/root` |
| **Variable data** | `/var`, `/tmp` |
| **Virtual** | `/proc`, `/sys`, `/dev`, `/run` |
| **Mount points** | `/mnt`, `/media` |
| **Optional** | `/opt`, `/srv` |
| **System boot** | `/boot` |

### Directory by Purpose

| Purpose | Primary Directory | Secondary Directories |
|---------|------------------|----------------------|
| **User files** | `/home` | `/root` |
| **Programs** | `/usr` | `/opt`, `/bin`, `/sbin` |
| **Configuration** | `/etc` | - |
| **Logs** | `/var/log` | - |
| **Temporary** | `/tmp` | `/var/tmp`, `/run` |
| **System info** | `/proc` | `/sys` |
| **Devices** | `/dev` | - |
| **Boot** | `/boot` | - |
| **External storage** | `/media` | `/mnt` |

---

**Last Updated:** November 2025  
**Standard:** Filesystem Hierarchy Standard (FHS) 3.0
