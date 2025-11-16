# ⚙️ Linux Process Management Guide

> Complete guide to managing processes in Linux

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What are processes |
| [Why Process Management?](#why-process-management) | Importance and benefits |
| [Process Types](#process-types) | Different kinds of processes |
| [Process States](#process-states) | Understanding process lifecycle |
| [Process Hierarchy](#process-hierarchy) | Parent-child relationships |
| [Viewing Processes](#viewing-processes) | Commands to see running processes |
| [Process Information](#process-information) | Detailed process data |
| [Starting Processes](#starting-processes) | Foreground and background |
| [Stopping Processes](#stopping-processes) | Kill and terminate |
| [Process Priority](#process-priority) | Nice and renice |
| [Job Control](#job-control) | Managing jobs in shell |
| [System Monitoring](#system-monitoring) | Real-time monitoring tools |
| [Service Management](#service-management) | Systemd and services |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What is a Process?

| Concept | Description |
|---------|-------------|
| **Process** | Running instance of a program in memory |
| **Program vs Process** | Program is file on disk, process is program in execution |
| **PID (Process ID)** | Unique number identifying each process |
| **Multi-tasking** | Linux runs multiple processes simultaneously |
| **Resource Usage** | Each process uses CPU, memory, and I/O |

### Basic Process Concepts

| Term | Description |
|------|-------------|
| **PID** | Process ID - unique identifier |
| **PPID** | Parent Process ID - who started this process |
| **UID** | User ID - which user owns the process |
| **State** | Current status (running, sleeping, stopped) |
| **Priority** | Importance level for CPU scheduling |
| **CPU Time** | How much CPU time process has used |
| **Memory** | RAM used by process |

---

## Why Process Management?

### Importance of Process Management

| Reason | Description | Example |
|--------|-------------|---------|
| **Performance** | Monitor and optimize system resources | Kill hung process eating CPU |
| **Troubleshooting** | Identify problematic processes | Find which process is using 100% CPU |
| **Resource Control** | Manage CPU and memory usage | Lower priority of background tasks |
| **Security** | Identify unauthorized processes | Detect malware or unauthorized daemons |
| **System Stability** | Prevent system crashes | Kill runaway processes |
| **Multi-tasking** | Run multiple tasks efficiently | Background jobs while working |

### Use Cases

| Scenario | Process Management Task |
|----------|------------------------|
| **System slow** | Find resource-hungry processes |
| **Application frozen** | Kill unresponsive process |
| **Server maintenance** | Start/stop services |
| **Development** | Run build processes in background |
| **Monitoring** | Track system performance |
| **Automation** | Schedule and manage cron jobs |

---

## Process Types

### Types of Processes

| Type | Description | Example |
|------|-------------|---------|
| **Foreground Process** | Interactive, attached to terminal | Text editor, shell commands |
| **Background Process** | Runs without user interaction | Started with `&` |
| **Daemon** | Background system service | `sshd`, `apache2`, `cron` |
| **Parent Process** | Creates other processes | Shell creates child processes |
| **Child Process** | Created by parent process | Commands run from shell |
| **Orphan Process** | Parent died, adopted by init | Process whose parent terminated |
| **Zombie Process** | Dead but not cleaned up | Terminated but still in process table |

### Process Categories

| Category | Description | Examples |
|----------|-------------|----------|
| **System Processes** | Core system operations | `init`, `systemd`, `kthreadd` |
| **User Processes** | Started by users | `bash`, `firefox`, `python script.py` |
| **Kernel Threads** | Kernel-level processes | Names in square brackets `[kworker]` |

---

## Process States

### Process State Diagram

| State | Symbol | Description |
|-------|--------|-------------|
| **Running** | R | Currently executing or ready to execute |
| **Sleeping** | S | Waiting for event (interruptible) |
| **Uninterruptible Sleep** | D | Waiting for I/O (cannot be interrupted) |
| **Stopped** | T | Paused (Ctrl+Z or SIGSTOP) |
| **Zombie** | Z | Terminated but not reaped by parent |
| **Idle** | I | Idle kernel thread |

### State Transitions

| From State | To State | Trigger |
|------------|----------|---------|
| Running | Sleeping | Waiting for I/O or event |
| Sleeping | Running | Event occurred, scheduled by CPU |
| Running | Stopped | Ctrl+Z or SIGSTOP signal |
| Stopped | Running | `fg` command or SIGCONT signal |
| Any | Zombie | Process terminates but parent hasn't read exit status |

---

## Process Hierarchy

### Process Tree Structure

| Concept | Description |
|---------|-------------|
| **Init Process** | First process (PID 1), parent of all |
| **systemd/init** | Modern init system |
| **Parent-Child** | Every process has a parent (except init) |
| **PPID** | Parent Process ID |
| **Process Tree** | Hierarchical structure of processes |

### Process Relationships

| Relationship | Description | Command to View |
|--------------|-------------|-----------------|
| **Parent → Child** | Parent creates child processes | `pstree` |
| **Orphan Adoption** | Init adopts orphaned processes | PID 1 becomes parent |
| **Process Group** | Related processes grouped together | `ps -ejH` |
| **Session** | Collection of process groups | `ps -eo pid,sid,cmd` |

---

## Viewing Processes

### ps Command

| Command | Description | Output |
|---------|-------------|--------|
| `ps` | Show processes in current terminal | Minimal info |
| `ps -e` | Show all processes | All system processes |
| `ps -ef` | Full format listing | Detailed info for all |
| `ps aux` | BSD style, all processes | User-oriented output |
| `ps -u username` | Processes for specific user | User's processes |
| `ps -p PID` | Specific process by PID | Single process info |

### ps Common Options

| Option | Description | Example |
|--------|-------------|---------|
| `-e` or `-A` | All processes | `ps -e` |
| `-f` | Full format | `ps -ef` |
| `-l` | Long format | `ps -l` |
| `aux` | BSD style, detailed | `ps aux` |
| `-u user` | Processes by user | `ps -u john` |
| `-p PID` | Specific process | `ps -p 1234` |
| `--forest` | Tree view | `ps -ef --forest` |
| `-o` | Custom output | `ps -eo pid,comm,%cpu,%mem` |

### ps Output Columns

| Column | Description |
|--------|-------------|
| **PID** | Process ID |
| **PPID** | Parent Process ID |
| **USER** | Owner of process |
| **%CPU** | CPU usage percentage |
| **%MEM** | Memory usage percentage |
| **VSZ** | Virtual memory size (KB) |
| **RSS** | Resident set size (physical memory in KB) |
| **TTY** | Terminal associated with process |
| **STAT** | Process state |
| **START** | Time process started |
| **TIME** | CPU time consumed |
| **COMMAND** | Command that started process |

### ps Examples

| Task | Command |
|------|---------|
| All processes detailed | `ps aux` |
| All processes hierarchical | `ps -ejH` |
| All processes tree view | `ps -ef --forest` |
| Processes by CPU usage | `ps aux --sort=-%cpu` |
| Processes by memory | `ps aux --sort=-%mem` |
| Top 10 CPU users | `ps aux --sort=-%cpu | head -11` |
| Find specific process | `ps aux | grep nginx` |
| Custom output | `ps -eo pid,user,comm,%cpu,%mem --sort=-%cpu` |

---

## Process Information

### Detailed Process Commands

| Command | Description | Example |
|---------|-------------|---------|
| `top` | Real-time process viewer | `top` |
| `htop` | Enhanced interactive viewer | `htop` (needs installation) |
| `pgrep` | Find process ID by name | `pgrep firefox` |
| `pidof` | Find PID of running program | `pidof nginx` |
| `pstree` | Display process tree | `pstree` |
| `/proc/[PID]/` | Process information directory | `cat /proc/1234/status` |

### pgrep Command

| Command | Description |
|---------|-------------|
| `pgrep process_name` | Find PID by name |
| `pgrep -u username` | PIDs for specific user |
| `pgrep -l process` | Show PID and name |
| `pgrep -a process` | Show PID and full command |
| `pgrep -c process` | Count matching processes |
| `pgrep -f pattern` | Match full command line |

### /proc Filesystem

| Path | Information |
|------|-------------|
| `/proc/[PID]/status` | Process status and details |
| `/proc/[PID]/cmdline` | Command line arguments |
| `/proc/[PID]/environ` | Environment variables |
| `/proc/[PID]/fd/` | Open file descriptors |
| `/proc/[PID]/maps` | Memory maps |
| `/proc/cpuinfo` | CPU information |
| `/proc/meminfo` | Memory information |

---

## Starting Processes

### Foreground Processes

| Command | Description |
|---------|-------------|
| `command` | Run in foreground (blocks terminal) |
| `firefox` | Starts Firefox in foreground |
| `./script.sh` | Run script in foreground |

### Background Processes

| Command | Description |
|---------|-------------|
| `command &` | Run in background |
| `firefox &` | Start Firefox in background |
| `./script.sh &` | Run script in background |
| `nohup command &` | Run immune to hangups |
| `nohup script.sh > output.log 2>&1 &` | Background with output to file |

### nohup Command

| Command | Description |
|---------|-------------|
| `nohup command &` | Run process immune to hangups |
| `nohup script.sh &` | Continue after logout |
| `nohup command > log.txt 2>&1 &` | Redirect output and errors |

### Process Scheduling

| Command | Description |
|---------|-------------|
| `at` | Schedule one-time job |
| `cron` | Schedule recurring jobs |
| `batch` | Run when system load is low |

---

## Stopping Processes

### Kill Command

| Command | Description | Use Case |
|---------|-------------|----------|
| `kill PID` | Send TERM signal (graceful) | Normal termination |
| `kill -9 PID` | Send KILL signal (force) | Unresponsive process |
| `kill -15 PID` | Send TERM signal (default) | Graceful shutdown |
| `kill -STOP PID` | Pause process | Temporarily stop |
| `kill -CONT PID` | Resume process | Continue stopped process |
| `kill -HUP PID` | Reload configuration | Restart without stopping |

### Common Kill Signals

| Signal | Number | Name | Description |
|--------|--------|------|-------------|
| **SIGHUP** | 1 | Hangup | Reload configuration |
| **SIGINT** | 2 | Interrupt | Ctrl+C |
| **SIGQUIT** | 3 | Quit | Ctrl+\ |
| **SIGKILL** | 9 | Kill | Force kill (cannot be caught) |
| **SIGTERM** | 15 | Terminate | Graceful termination (default) |
| **SIGSTOP** | 19 | Stop | Pause process |
| **SIGCONT** | 18 | Continue | Resume process |

### Kill Signal Usage

| Task | Command |
|------|---------|
| Normal termination | `kill PID` or `kill -15 PID` |
| Force kill | `kill -9 PID` or `kill -KILL PID` |
| Reload config | `kill -1 PID` or `kill -HUP PID` |
| Pause process | `kill -STOP PID` |
| Resume process | `kill -CONT PID` |

### killall Command

| Command | Description |
|---------|-------------|
| `killall process_name` | Kill all processes by name |
| `killall -9 firefox` | Force kill all Firefox processes |
| `killall -u username` | Kill all processes of user |
| `killall -i firefox` | Interactive (confirm each) |

### pkill Command

| Command | Description |
|---------|-------------|
| `pkill process_name` | Kill processes by name |
| `pkill -u username` | Kill user's processes |
| `pkill -9 firefox` | Force kill by name |
| `pkill -f pattern` | Kill matching full command line |

### Kill Examples

| Task | Command |
|------|---------|
| Kill process by PID | `kill 1234` |
| Force kill process | `kill -9 1234` |
| Kill all Firefox | `killall firefox` |
| Kill by name pattern | `pkill fire` |
| Kill user's processes | `pkill -u john` |
| Kill matching command | `pkill -f "python script.py"` |

---

## Process Priority

### Understanding Priority

| Concept | Description |
|---------|-------------|
| **Nice Value** | Priority level (-20 to 19) |
| **Lower Nice** | Higher priority (more CPU time) |
| **Higher Nice** | Lower priority (less CPU time) |
| **Default Nice** | 0 |
| **Range** | -20 (highest) to +19 (lowest) |

### Nice Value Scale

| Nice Value | Priority | Usage |
|------------|----------|-------|
| **-20** | Highest | Critical system processes |
| **-10 to -1** | High | Important tasks |
| **0** | Normal | Default priority |
| **1 to 10** | Low | Background tasks |
| **11 to 19** | Lowest | Very low priority tasks |

### nice Command

| Command | Description |
|---------|-------------|
| `nice command` | Run with default nice (10) |
| `nice -n 10 command` | Run with nice value 10 |
| `nice -n -5 command` | Run with nice value -5 |
| `nice -20 command` | Lowest priority |
| `nice --20 command` | Highest priority (needs root) |

### renice Command

| Command | Description |
|---------|-------------|
| `renice -n 10 -p PID` | Change nice value of running process |
| `renice 10 PID` | Set nice to 10 for PID |
| `renice -n 5 -u username` | Change priority for user's processes |
| `renice -n 10 -g groupname` | Change priority for group |

### Priority Examples

| Task | Command |
|------|---------|
| Start low priority process | `nice -n 15 ./script.sh` |
| Start high priority | `sudo nice -n -10 ./important.sh` |
| Lower running process priority | `renice -n 10 -p 1234` |
| Increase process priority | `sudo renice -n -5 -p 1234` |
| Lower all user processes | `renice -n 10 -u john` |

---

## Job Control

### Background and Foreground

| Command | Description |
|---------|-------------|
| `command &` | Start in background |
| `Ctrl+Z` | Suspend foreground process |
| `bg` | Resume suspended job in background |
| `fg` | Bring background job to foreground |
| `jobs` | List background jobs |

### Jobs Command

| Command | Description |
|---------|-------------|
| `jobs` | List all jobs |
| `jobs -l` | List with PIDs |
| `jobs -r` | List running jobs |
| `jobs -s` | List stopped jobs |

### Job Control Examples

| Task | Command |
|------|---------|
| Start background | `firefox &` |
| List jobs | `jobs` |
| Bring job 1 to foreground | `fg %1` |
| Resume job 2 in background | `bg %2` |
| Kill job 1 | `kill %1` |

### Job References

| Reference | Meaning |
|-----------|---------|
| `%1` | Job number 1 |
| `%%` or `%+` | Current job |
| `%-` | Previous job |
| `%string` | Job whose command starts with string |
| `%?string` | Job whose command contains string |

---

## System Monitoring

### top Command

| Command | Description |
|---------|-------------|
| `top` | Real-time process monitor |
| `top -u username` | Monitor user's processes |
| `top -p PID` | Monitor specific process |
| `top -d 5` | Update every 5 seconds |

### top Interactive Keys

| Key | Action |
|-----|--------|
| `q` | Quit |
| `k` | Kill process (prompts for PID) |
| `r` | Renice process |
| `M` | Sort by memory usage |
| `P` | Sort by CPU usage |
| `T` | Sort by running time |
| `u` | Filter by user |
| `h` | Help |
| `1` | Show individual CPUs |
| `Space` | Refresh immediately |

### htop Command

| Command | Description |
|---------|-------------|
| `htop` | Enhanced interactive process viewer |
| `htop -u username` | Monitor user's processes |
| `htop -p PID` | Monitor specific process |

### htop Interactive Keys

| Key | Action |
|-----|--------|
| `F1` | Help |
| `F2` | Setup |
| `F3` | Search |
| `F4` | Filter |
| `F5` | Tree view |
| `F6` | Sort by column |
| `F9` | Kill process |
| `F10` | Quit |
| `Space` | Tag process |
| `u` | Filter by user |

### Other Monitoring Commands

| Command | Description |
|---------|-------------|
| `vmstat` | Virtual memory statistics |
| `iostat` | CPU and I/O statistics |
| `mpstat` | Multiprocessor statistics |
| `sar` | System activity report |
| `free` | Memory usage |
| `uptime` | System uptime and load |

### System Load

| Command | Description |
|---------|-------------|
| `uptime` | Show load average |
| `w` | Who is logged in and load |
| `cat /proc/loadavg` | Load average file |

### Load Average Meaning

| Load Average | CPU Cores | Status |
|--------------|-----------|--------|
| **< 1.0** | 1 core | System not busy |
| **1.0** | 1 core | System fully utilized |
| **> 1.0** | 1 core | Processes waiting |
| **< 4.0** | 4 cores | System not busy |
| **4.0** | 4 cores | Fully utilized |

---

## Service Management

### systemd Commands

| Command | Description |
|---------|-------------|
| `systemctl start service` | Start service |
| `systemctl stop service` | Stop service |
| `systemctl restart service` | Restart service |
| `systemctl reload service` | Reload configuration |
| `systemctl status service` | Check service status |
| `systemctl enable service` | Enable at boot |
| `systemctl disable service` | Disable at boot |
| `systemctl is-active service` | Check if running |
| `systemctl is-enabled service` | Check if enabled |

### Systemctl Examples

| Task | Command |
|------|---------|
| Start Apache | `sudo systemctl start apache2` |
| Stop MySQL | `sudo systemctl stop mysql` |
| Restart SSH | `sudo systemctl restart sshd` |
| Enable Docker at boot | `sudo systemctl enable docker` |
| Check Nginx status | `systemctl status nginx` |
| List all services | `systemctl list-units --type=service` |
| List enabled services | `systemctl list-unit-files --state=enabled` |

### Service Status Output

| Status | Meaning |
|--------|---------|
| **active (running)** | Service is running |
| **active (exited)** | One-shot service completed |
| **inactive (dead)** | Service is stopped |
| **failed** | Service failed to start |

### Legacy Service Commands

| Command | Description |
|---------|-------------|
| `service name start` | Start service (old method) |
| `service name stop` | Stop service |
| `service name restart` | Restart service |
| `service name status` | Check status |

---

## Practical Examples

### Example 1: Find and Kill High CPU Process

| Step | Command | Purpose |
|------|---------|---------|
| 1. Find process | `top` or `ps aux --sort=-%cpu | head` | Identify CPU hog |
| 2. Note PID | Look at first column | Get process ID |
| 3. Try graceful kill | `kill PID` | Send TERM signal |
| 4. Wait | Wait 10-15 seconds | Give it time |
| 5. Force kill if needed | `kill -9 PID` | Force termination |

### Example 2: Run Long Process in Background

| Step | Command | Purpose |
|------|---------|---------|
| 1. Start with nohup | `nohup ./long-script.sh > output.log 2>&1 &` | Run in background, immune to hangups |
| 2. Get PID | Note PID from output or `echo $!` | Track process |
| 3. Monitor | `tail -f output.log` | Watch progress |
| 4. Check if running | `ps -p PID` | Verify still running |

### Example 3: Find Process by Name

| Step | Command | Purpose |
|------|---------|---------|
| 1. Find by name | `pgrep -l firefox` | Get PID and name |
| 2. Get details | `ps -p $(pgrep firefox)` | Full process info |
| 3. Alternative | `ps aux | grep firefox` | Search in all processes |

### Example 4: Monitor Specific Process

| Step | Command | Purpose |
|------|---------|---------|
| 1. Find PID | `pgrep process_name` | Get process ID |
| 2. Monitor | `top -p PID` | Watch specific process |
| 3. Or use htop | `htop -p PID` | Enhanced view |
| 4. Check details | `cat /proc/PID/status` | Detailed information |

### Example 5: Start Low Priority Background Task

| Step | Command | Purpose |
|------|---------|---------|
| 1. Start with nice | `nice -n 15 ./backup.sh &` | Low priority background |
| 2. Verify priority | `ps -o pid,ni,comm -p PID` | Check nice value |
| 3. Adjust if needed | `renice -n 19 -p PID` | Lower priority more |

### Example 6: Kill All Processes of User

| Step | Command | Purpose |
|------|---------|---------|
| 1. List user processes | `ps -u username` | See what's running |
| 2. Kill all | `sudo pkill -u username` | Terminate all user processes |
| 3. Force kill if needed | `sudo pkill -9 -u username` | Force termination |

### Example 7: Find Memory-Hungry Process

| Step | Command | Purpose |
|------|---------|---------|
| 1. Sort by memory | `ps aux --sort=-%mem | head -10` | Top 10 memory users |
| 2. Or use top | `top` then press `M` | Sort by memory in top |
| 3. Get details | `ps -o pid,user,%mem,command -p PID` | Specific process info |

### Example 8: Restart Hung Service

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check status | `systemctl status service_name` | See current state |
| 2. Try restart | `sudo systemctl restart service_name` | Normal restart |
| 3. If fails, force | `sudo systemctl kill -s SIGKILL service_name` | Force kill |
| 4. Then start | `sudo systemctl start service_name` | Start fresh |

### Example 9: Find Zombie Processes

| Step | Command | Purpose |
|------|---------|---------|
| 1. Find zombies | `ps aux | grep Z` | List zombie processes |
| 2. Or use | `ps -eo stat,pid,ppid,comm | grep ^Z` | Detailed zombie info |
| 3. Kill parent | `kill PPID` | Parent reaps zombie |
| 4. If parent won't die | `kill -9 PPID` | Force kill parent |

### Example 10: Monitor System Load

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check load | `uptime` | See load average |
| 2. Continuous monitor | `watch -n 1 uptime` | Update every second |
| 3. Detailed view | `top` | See process breakdown |
| 4. CPU breakdown | `mpstat -P ALL 1` | Per-CPU statistics |

---

## Quick Reference

### Essential Process Commands

| Task | Command |
|------|---------|
| List all processes | `ps aux` |
| Real-time monitor | `top` or `htop` |
| Find process by name | `pgrep process_name` |
| Find PID | `pidof program` |
| Kill process | `kill PID` |
| Force kill | `kill -9 PID` |
| Kill by name | `killall process_name` |
| Background process | `command &` |
| List jobs | `jobs` |
| Process tree | `pstree` |

### Common Signals

| Signal | Number | Use |
|--------|--------|-----|
| TERM | 15 | Graceful shutdown (default) |
| KILL | 9 | Force kill |
| HUP | 1 | Reload config |
| STOP | 19 | Pause |
| CONT | 18 | Resume |

### Service Commands

| Task | Command |
|------|---------|
| Start service | `systemctl start service` |
| Stop service | `systemctl stop service` |
| Restart service | `systemctl restart service` |
| Check status | `systemctl status service` |
| Enable at boot | `systemctl enable service` |

---

## Best Practices

| Practice | Description |
|----------|-------------|
| **Try SIGTERM first** | Always try graceful kill before SIGKILL |
| **Monitor before killing** | Understand what process does before killing |
| **Use nice for background** | Lower priority for non-urgent tasks |
| **Regular monitoring** | Check system regularly with top/htop |
| **Clean up zombies** | Kill parent process to clean zombies |
| **Use nohup** | For long-running processes over SSH |
| **Document changes** | Keep track of what processes you kill |

