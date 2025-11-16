# 📊 Linux System Monitoring Guide

> Complete guide to monitoring system resources and performance in Linux

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What is system monitoring |
| [Why Monitor?](#why-monitor) | Importance and benefits |
| [Monitoring Categories](#monitoring-categories) | Types of monitoring |
| [CPU Monitoring](#cpu-monitoring) | CPU usage and performance |
| [Memory Monitoring](#memory-monitoring) | RAM and swap usage |
| [Disk Monitoring](#disk-monitoring) | Disk usage and I/O |
| [Network Monitoring](#network-monitoring) | Network traffic and connections |
| [Process Monitoring](#process-monitoring) | Running processes |
| [System Load](#system-load) | Load average and uptime |
| [Log Monitoring](#log-monitoring) | System and application logs |
| [Performance Analysis](#performance-analysis) | Advanced diagnostics |
| [Real-Time Monitoring](#real-time-monitoring) | Live system stats |
| [Automated Monitoring](#automated-monitoring) | Scripts and alerts |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What is System Monitoring?

| Concept | Description |
|---------|-------------|
| **System Monitoring** | Tracking system resources, performance, and health |
| **Metrics** | Measurable data points (CPU, memory, disk, network) |
| **Real-Time** | Live monitoring of current system state |
| **Historical** | Tracking trends over time |
| **Alerting** | Notifications when thresholds are exceeded |

### Key Monitoring Areas

| Area | What to Monitor | Why |
|------|----------------|-----|
| **CPU** | Usage, load, processes | Performance bottlenecks |
| **Memory** | RAM, swap, cache | Memory leaks, insufficient RAM |
| **Disk** | Usage, I/O, read/write speed | Storage capacity, I/O bottlenecks |
| **Network** | Traffic, connections, errors | Bandwidth issues, connectivity |
| **Processes** | Running apps, zombies, resource usage | Application problems |
| **Logs** | Errors, warnings, events | Troubleshooting, security |

---

## Why Monitor?

### Benefits of System Monitoring

| Benefit | Description | Example |
|---------|-------------|---------|
| **Performance Optimization** | Identify and fix bottlenecks | Find process using 100% CPU |
| **Capacity Planning** | Plan for future needs | Know when to add more RAM |
| **Troubleshooting** | Diagnose problems quickly | Identify why system is slow |
| **Security** | Detect unusual activity | Spot unauthorized processes |
| **Uptime** | Prevent downtime | Fix issues before failures |
| **Resource Management** | Optimize resource allocation | Balance workload across CPUs |

### Use Cases

| Scenario | Monitoring Task |
|----------|----------------|
| **Server running slow** | Check CPU, memory, and I/O usage |
| **Website down** | Monitor network and processes |
| **Disk full** | Track disk usage and growth |
| **High bandwidth usage** | Monitor network traffic |
| **Application crashes** | Check logs and memory |
| **Security breach** | Monitor unusual processes and connections |

---

## Monitoring Categories

### Types of Monitoring

| Type | Description | Tools |
|------|-------------|-------|
| **Resource Monitoring** | CPU, memory, disk, network | top, vmstat, iostat |
| **Process Monitoring** | Running processes | ps, top, htop |
| **Performance Monitoring** | System performance metrics | sar, perf, sysstat |
| **Log Monitoring** | System and application logs | tail, journalctl, grep |
| **Network Monitoring** | Network traffic and connections | netstat, ss, iftop |
| **Service Monitoring** | Daemon and service status | systemctl, service |

---

## CPU Monitoring

### CPU Information Commands

| Command | Description | Output |
|---------|-------------|--------|
| `lscpu` | Display CPU architecture | CPU cores, model, speed |
| `cat /proc/cpuinfo` | Detailed CPU information | All CPU details |
| `nproc` | Number of processing units | CPU core count |
| `grep 'cpu cores' /proc/cpuinfo` | Number of CPU cores | Core count per socket |

### CPU Usage Commands

| Command | Description | Use Case |
|---------|-------------|----------|
| `top` | Real-time CPU usage | Overall system view |
| `htop` | Enhanced CPU monitor | Interactive interface |
| `mpstat` | Multiprocessor statistics | Per-CPU breakdown |
| `vmstat` | Virtual memory stats (includes CPU) | Overall system stats |
| `sar -u` | CPU utilization report | Historical data |
| `uptime` | Load average | Quick CPU load check |

### top CPU Display

| Field | Description |
|-------|-------------|
| **%us** | User space CPU usage |
| **%sy** | System (kernel) CPU usage |
| **%ni** | Nice (low priority) processes |
| **%id** | Idle CPU percentage |
| **%wa** | I/O wait time |
| **%hi** | Hardware interrupts |
| **%si** | Software interrupts |
| **%st** | Steal time (virtualization) |

### mpstat Command

| Command | Description |
|---------|-------------|
| `mpstat` | CPU statistics for all processors |
| `mpstat -P ALL` | Per-CPU statistics |
| `mpstat 1 5` | Update every 1 second, 5 times |
| `mpstat -P 0 1` | Monitor CPU 0 every second |

### CPU Monitoring Examples

| Task | Command |
|------|---------|
| Check CPU usage | `top` or `htop` |
| Per-CPU breakdown | `mpstat -P ALL` |
| Average CPU load | `uptime` |
| CPU info | `lscpu` |
| CPU-intensive processes | `ps aux --sort=-%cpu | head -10` |
| Monitor CPU continuously | `watch -n 1 'mpstat -P ALL'` |

---

## Memory Monitoring

### Memory Information Commands

| Command | Description | Output |
|---------|-------------|--------|
| `free` | Memory usage summary | RAM and swap usage |
| `free -h` | Human-readable format | Memory in GB/MB |
| `free -m` | Memory in megabytes | Detailed MB view |
| `vmstat` | Virtual memory statistics | Memory, swap, I/O |
| `cat /proc/meminfo` | Detailed memory info | All memory details |

### free Command Output

| Column | Description |
|--------|-------------|
| **total** | Total installed memory |
| **used** | Used memory |
| **free** | Unused memory |
| **shared** | Memory used by tmpfs |
| **buff/cache** | Buffers and cache |
| **available** | Memory available for new apps |

### Memory Monitoring Commands

| Command | Description |
|---------|-------------|
| `free -h` | Human-readable memory usage |
| `free -s 5` | Update every 5 seconds |
| `vmstat 1` | Virtual memory stats every second |
| `top` (press M) | Sort processes by memory |
| `htop` | Interactive memory view |
| `smem` | Per-process memory usage (if installed) |

### Memory Usage by Process

| Command | Description |
|---------|-------------|
| `ps aux --sort=-%mem` | Processes sorted by memory |
| `ps aux --sort=-%mem | head -10` | Top 10 memory users |
| `top -o %MEM` | Sort top by memory |
| `pmap PID` | Memory map of process |

### Swap Monitoring

| Command | Description |
|---------|-------------|
| `swapon --show` | Show swap devices |
| `free -h` | Shows swap usage |
| `vmstat 1` | Monitor swap activity |
| `cat /proc/swaps` | Swap device information |

### Memory Monitoring Examples

| Task | Command |
|------|---------|
| Check memory usage | `free -h` |
| Monitor continuously | `watch -n 2 free -h` |
| Find memory hogs | `ps aux --sort=-%mem | head -10` |
| Check swap usage | `swapon --show` |
| Detailed memory info | `cat /proc/meminfo` |
| Virtual memory stats | `vmstat 1 10` |

---

## Disk Monitoring

### Disk Space Commands

| Command | Description | Output |
|---------|-------------|--------|
| `df` | Disk free space | All mounted filesystems |
| `df -h` | Human-readable format | Space in GB/MB |
| `df -i` | Inode usage | Available inodes |
| `du` | Disk usage | Directory sizes |
| `du -sh` | Summary, human-readable | Total size |
| `du -sh /*` | Size of top-level directories | Root directory breakdown |

### df Command Examples

| Command | Description |
|---------|-------------|
| `df -h` | Human-readable disk space |
| `df -h /home` | Space for specific mount |
| `df -i` | Inode usage |
| `df -T` | Show filesystem type |
| `df -h --total` | Show total at bottom |

### du Command Examples

| Command | Description |
|---------|-------------|
| `du -sh /var/*` | Size of /var subdirectories |
| `du -h --max-depth=1 /home` | Home directory sizes |
| `du -sh * | sort -rh | head -10` | Top 10 largest items |
| `du -ahx /home | sort -rh | head -20` | Top 20 files/dirs |

### Disk I/O Monitoring

| Command | Description |
|---------|-------------|
| `iostat` | CPU and I/O statistics |
| `iostat -x` | Extended statistics |
| `iostat -x 1` | Update every second |
| `iotop` | Real-time I/O monitor (needs install) |
| `vmstat 1` | Shows I/O wait |

### iostat Output

| Column | Description |
|--------|-------------|
| **tps** | Transfers per second |
| **kB_read/s** | KB read per second |
| **kB_wrtn/s** | KB written per second |
| **kB_read** | Total KB read |
| **kB_wrtn** | Total KB written |

### Finding Large Files

| Command | Description |
|---------|-------------|
| `find / -type f -size +100M` | Files larger than 100MB |
| `find /var -type f -size +1G` | Files over 1GB in /var |
| `du -ah /home | sort -rh | head -20` | 20 largest files in /home |
| `ncdu /` | Interactive disk usage analyzer |

### Disk Monitoring Examples

| Task | Command |
|------|---------|
| Check disk space | `df -h` |
| Find large directories | `du -sh /* | sort -rh` |
| Monitor disk I/O | `iostat -x 1` |
| Find large files | `find / -type f -size +100M` |
| Inode usage | `df -i` |
| Real-time I/O | `iotop` |
| Disk usage by directory | `du -h --max-depth=1 /var | sort -rh` |

---

## Network Monitoring

### Network Interface Information

| Command | Description |
|---------|-------------|
| `ip addr` | Show IP addresses |
| `ifconfig` | Network interface config (legacy) |
| `ip link show` | Network interfaces |
| `ethtool eth0` | Interface details |

### Network Statistics

| Command | Description |
|---------|-------------|
| `netstat` | Network statistics (legacy) |
| `ss` | Socket statistics (modern) |
| `ss -tuln` | TCP/UDP listening ports |
| `ss -s` | Summary statistics |
| `netstat -i` | Interface statistics |

### Active Connections

| Command | Description |
|---------|-------------|
| `ss -tunap` | All TCP/UDP connections |
| `netstat -tunap` | Active connections (legacy) |
| `ss -tn state established` | Established TCP connections |
| `lsof -i` | Open network files |
| `lsof -i :80` | What's using port 80 |

### Network Traffic Monitoring

| Command | Description |
|---------|-------------|
| `iftop` | Real-time bandwidth usage |
| `nethogs` | Per-process bandwidth monitor |
| `vnstat` | Network traffic statistics |
| `nload` | Network load visualizer |
| `iptraf-ng` | Interactive IP LAN monitor |

### Bandwidth Usage

| Command | Description |
|---------|-------------|
| `iftop -i eth0` | Monitor interface eth0 |
| `nethogs eth0` | Per-process on eth0 |
| `vnstat -l -i eth0` | Live traffic on eth0 |
| `nload eth0` | Visual load on eth0 |

### Network Testing

| Command | Description |
|---------|-------------|
| `ping host` | Test connectivity |
| `traceroute host` | Trace route to host |
| `mtr host` | Network diagnostic tool |
| `nmap host` | Port scanning |
| `tcpdump -i eth0` | Packet capture |

### Network Monitoring Examples

| Task | Command |
|------|---------|
| Show IP addresses | `ip addr` |
| List open ports | `ss -tuln` |
| Active connections | `ss -tunap` |
| Real-time bandwidth | `iftop` |
| Per-process network | `nethogs` |
| Test connectivity | `ping google.com` |
| Check who's on port 80 | `lsof -i :80` |
| Network statistics | `ss -s` |

---

## Process Monitoring

### Process Listing

| Command | Description |
|---------|-------------|
| `ps aux` | All processes |
| `ps -ef` | Full format listing |
| `ps -u username` | User's processes |
| `pstree` | Process tree |
| `pgrep process_name` | Find PID by name |

### Real-Time Process Monitoring

| Command | Description |
|---------|-------------|
| `top` | Real-time process viewer |
| `htop` | Enhanced interactive viewer |
| `atop` | Advanced system monitor |
| `glances` | Cross-platform monitor |

### Process Resource Usage

| Command | Description |
|---------|-------------|
| `ps aux --sort=-%cpu` | Sort by CPU usage |
| `ps aux --sort=-%mem` | Sort by memory usage |
| `pidstat` | Per-process statistics |
| `pidstat 1` | Update every second |

### Process Details

| Command | Description |
|---------|-------------|
| `ps -p PID -o %cpu,%mem,cmd` | Specific process stats |
| `cat /proc/PID/status` | Process status |
| `lsof -p PID` | Open files by process |
| `pmap PID` | Process memory map |

### Process Monitoring Examples

| Task | Command |
|------|---------|
| View all processes | `ps aux` |
| Real-time monitor | `top` or `htop` |
| Find CPU hogs | `ps aux --sort=-%cpu | head -10` |
| Find memory hogs | `ps aux --sort=-%mem | head -10` |
| Process tree | `pstree` |
| Monitor specific process | `top -p PID` |

---

## System Load

### Understanding Load Average

| Concept | Description |
|---------|-------------|
| **Load Average** | Average number of processes waiting for CPU |
| **Three Numbers** | 1-minute, 5-minute, 15-minute averages |
| **Interpretation** | Compare to number of CPU cores |
| **< Core Count** | System not busy |
| **= Core Count** | Fully utilized |
| **> Core Count** | Processes waiting |

### Load Average Commands

| Command | Description |
|---------|-------------|
| `uptime` | Show load average |
| `w` | Who is logged in + load |
| `top` | First line shows load |
| `cat /proc/loadavg` | Raw load average data |

### Load Average Examples

| Load | CPUs | Status |
|------|------|--------|
| 0.50, 0.60, 0.70 | 1 core | Light load |
| 1.00, 1.00, 1.00 | 1 core | Fully utilized |
| 2.00, 2.50, 3.00 | 1 core | Overloaded |
| 2.00, 2.00, 2.00 | 4 cores | Half utilized |
| 4.00, 4.00, 4.00 | 4 cores | Fully utilized |
| 8.00, 8.00, 8.00 | 4 cores | Heavily overloaded |

### System Uptime

| Command | Description |
|---------|-------------|
| `uptime` | System uptime and load |
| `who -b` | Last boot time |
| `last reboot` | Reboot history |
| `cat /proc/uptime` | Uptime in seconds |

---

## Log Monitoring

### System Logs Location

| Log File | Description |
|----------|-------------|
| `/var/log/syslog` | System logs (Debian/Ubuntu) |
| `/var/log/messages` | System logs (RHEL/CentOS) |
| `/var/log/auth.log` | Authentication logs |
| `/var/log/kern.log` | Kernel logs |
| `/var/log/dmesg` | Boot messages |
| `/var/log/boot.log` | Boot process logs |
| `/var/log/cron` | Cron job logs |

### Log Viewing Commands

| Command | Description |
|---------|-------------|
| `tail /var/log/syslog` | Last 10 lines |
| `tail -f /var/log/syslog` | Follow in real-time |
| `tail -n 50 /var/log/syslog` | Last 50 lines |
| `head /var/log/syslog` | First 10 lines |
| `less /var/log/syslog` | View with pagination |
| `cat /var/log/syslog` | View entire log |

### journalctl (systemd Logs)

| Command | Description |
|---------|-------------|
| `journalctl` | All journal logs |
| `journalctl -f` | Follow in real-time |
| `journalctl -u service` | Logs for specific service |
| `journalctl --since today` | Today's logs |
| `journalctl --since "1 hour ago"` | Last hour |
| `journalctl -p err` | Only errors |
| `journalctl -k` | Kernel messages |
| `journalctl -b` | Current boot logs |

### Searching Logs

| Command | Description |
|---------|-------------|
| `grep "error" /var/log/syslog` | Search for errors |
| `grep -i "fail" /var/log/auth.log` | Case-insensitive search |
| `grep -r "error" /var/log/` | Search all logs |
| `journalctl | grep "error"` | Search journal |
| `zgrep "pattern" /var/log/syslog*.gz` | Search compressed logs |

### Log Monitoring Examples

| Task | Command |
|------|---------|
| Watch system log | `tail -f /var/log/syslog` |
| Check authentication | `tail -f /var/log/auth.log` |
| View service logs | `journalctl -u nginx -f` |
| Find errors | `journalctl -p err --since today` |
| Boot messages | `dmesg | less` |
| Last 100 lines | `tail -n 100 /var/log/syslog` |
| Search for failed logins | `grep "Failed" /var/log/auth.log` |

---

## Performance Analysis

### System Analysis Tools

| Command | Description |
|---------|-------------|
| `vmstat` | Virtual memory statistics |
| `iostat` | I/O statistics |
| `mpstat` | Processor statistics |
| `sar` | System activity reporter |
| `perf` | Performance analysis tool |

### vmstat Command

| Command | Description |
|---------|-------------|
| `vmstat` | One-time report |
| `vmstat 1` | Update every second |
| `vmstat 1 10` | 10 updates, 1 second apart |
| `vmstat -s` | Memory statistics |
| `vmstat -d` | Disk statistics |

### vmstat Output

| Column | Description |
|--------|-------------|
| **r** | Processes waiting for CPU |
| **b** | Processes in uninterruptible sleep |
| **swpd** | Virtual memory used |
| **free** | Free memory |
| **buff** | Buffer memory |
| **cache** | Cache memory |
| **si** | Swap in (from disk) |
| **so** | Swap out (to disk) |
| **bi** | Blocks in (read) |
| **bo** | Blocks out (write) |

### sar Command (System Activity Reporter)

| Command | Description |
|---------|-------------|
| `sar` | CPU usage (default) |
| `sar -u` | CPU utilization |
| `sar -r` | Memory utilization |
| `sar -b` | I/O statistics |
| `sar -n DEV` | Network statistics |
| `sar -u 1 10` | CPU usage, 10 samples |
| `sar -f /var/log/sa/sa15` | Historical data from 15th |

### Performance Monitoring Examples

| Task | Command |
|------|---------|
| Overall system stats | `vmstat 1` |
| CPU breakdown | `mpstat -P ALL 1` |
| I/O performance | `iostat -x 1` |
| Memory performance | `vmstat -s` |
| Network performance | `sar -n DEV 1 5` |
| Historical CPU | `sar -u` |

---

## Real-Time Monitoring

### Interactive Monitors

| Tool | Description | Features |
|------|-------------|----------|
| `top` | Traditional process viewer | Basic, widely available |
| `htop` | Enhanced interactive monitor | Colors, mouse support, tree view |
| `atop` | Advanced system monitor | Detailed stats, logging |
| `glances` | Cross-platform monitor | Modern interface, modules |
| `nmon` | Performance monitor | IBM tool, comprehensive |

### top Command Keys

| Key | Action |
|-----|--------|
| `M` | Sort by memory |
| `P` | Sort by CPU |
| `T` | Sort by time |
| `k` | Kill process |
| `r` | Renice process |
| `u` | Filter by user |
| `1` | Show individual CPUs |
| `h` | Help |
| `q` | Quit |

### htop Features

| Feature | Description |
|---------|-------------|
| **Color coded** | Easy to read meters |
| **Mouse support** | Click to select |
| **Tree view** | F5 for process tree |
| **Filtering** | F4 to filter |
| **Search** | F3 to search |
| **Setup** | F2 for settings |

### glances Features

| Feature | Description |
|---------|-------------|
| **Web interface** | Access via browser |
| **Modules** | CPU, mem, disk, network |
| **Alerts** | Configurable thresholds |
| **Export** | CSV, JSON output |
| **Client/server** | Monitor remote systems |

---

## Automated Monitoring

### Monitoring Scripts

| Script Purpose | Basic Command |
|----------------|---------------|
| CPU alert | `if [ $(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1) -gt 80 ]; then ...` |
| Disk alert | `if [ $(df -h / | tail -1 | awk '{print $5}' | cut -d'%' -f1) -gt 90 ]; then ...` |
| Memory alert | `if [ $(free | grep Mem | awk '{print ($3/$2) * 100}') -gt 90 ]; then ...` |

### Cron Monitoring Jobs

| Schedule | Command | Purpose |
|----------|---------|---------|
| Every 5 min | `*/5 * * * * /path/to/monitor.sh` | Regular checks |
| Hourly | `0 * * * * /path/to/hourly_check.sh` | Periodic logs |
| Daily | `0 0 * * * /path/to/daily_report.sh` | Daily reports |

### Watch Command

| Command | Description |
|---------|-------------|
| `watch command` | Repeat every 2 seconds |
| `watch -n 5 command` | Repeat every 5 seconds |
| `watch -d command` | Highlight differences |
| `watch -n 1 'df -h'` | Monitor disk space |
| `watch -n 2 'free -h'` | Monitor memory |

### Monitoring with watch

| Task | Command |
|------|---------|
| Disk space | `watch -n 5 df -h` |
| Memory | `watch -n 2 free -h` |
| Load average | `watch -n 1 uptime` |
| Network | `watch -n 1 'ss -s'` |
| Process count | `watch -n 5 'ps aux | wc -l'` |

---

## Practical Examples

### Example 1: System Health Check

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check load | `uptime` | See system load |
| 2. Check CPU | `top` (press 1) | Per-CPU usage |
| 3. Check memory | `free -h` | RAM usage |
| 4. Check disk | `df -h` | Disk space |
| 5. Check processes | `ps aux --sort=-%cpu | head -10` | Top CPU users |

### Example 2: Find Resource Bottleneck

| Step | Command | Purpose |
|------|---------|---------|
| 1. Overall view | `top` | Identify issue type |
| 2. If high CPU | `ps aux --sort=-%cpu | head -10` | Find CPU hogs |
| 3. If high memory | `ps aux --sort=-%mem | head -10` | Find memory hogs |
| 4. If I/O wait | `iostat -x 1` | Check disk I/O |
| 5. If network | `iftop` | Check bandwidth |

### Example 3: Monitor Disk Space

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check current | `df -h` | Current usage |
| 2. Find large dirs | `du -sh /* | sort -rh | head -10` | Top directories |
| 3. Find large files | `find / -type f -size +100M -exec ls -lh {} \;` | Files over 100MB |
| 4. Monitor growth | `watch -n 60 df -h` | Track changes |

### Example 4: Track Memory Leak

| Step | Command | Purpose |
|------|---------|---------|
| 1. Baseline | `ps aux | grep process_name` | Initial memory |
| 2. Monitor | `watch -n 5 'ps aux | grep process_name'` | Track over time |
| 3. Details | `pmap PID` | Memory map |
| 4. Log data | `while true; do ps aux | grep process >> mem.log; sleep 60; done` | Historical data |

### Example 5: Network Traffic Analysis

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check connections | `ss -tunap` | Active connections |
| 2. Bandwidth usage | `iftop` | Real-time traffic |
| 3. Per-process | `nethogs` | Which app using bandwidth |
| 4. Port usage | `lsof -i :80` | What's on port 80 |

### Example 6: Service Performance

| Step | Command | Purpose |
|------|---------|---------|
| 1. Service status | `systemctl status nginx` | Check if running |
| 2. Service logs | `journalctl -u nginx -f` | Watch logs |
| 3. Resource usage | `ps aux | grep nginx` | CPU/memory usage |
| 4. Connections | `ss -tunap | grep nginx` | Active connections |

### Example 7: Automated Alert Script

```bash
#!/bin/bash
# Simple monitoring script

# CPU threshold
CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1)
if (( $(echo "$CPU > 80" | bc -l) )); then
    echo "High CPU: $CPU%" | mail -s "Alert" admin@example.com
fi

# Disk threshold
DISK=$(df -h / | tail -1 | awk '{print $5}' | cut -d'%' -f1)
if [ $DISK -gt 90 ]; then
    echo "Disk usage: $DISK%" | mail -s "Alert" admin@example.com
fi

# Memory threshold  
MEM=$(free | grep Mem | awk '{print ($3/$2) * 100}' | cut -d'.' -f1)
if [ $MEM -gt 90 ]; then
    echo "Memory usage: $MEM%" | mail -s "Alert" admin@example.com
fi
```

### Example 8: Daily Report Script

```bash
#!/bin/bash
# Generate daily system report

REPORT="/tmp/daily_report.txt"
DATE=$(date '+%Y-%m-%d')

echo "System Report - $DATE" > $REPORT
echo "===================" >> $REPORT
echo "" >> $REPORT

echo "UPTIME:" >> $REPORT
uptime >> $REPORT
echo "" >> $REPORT

echo "DISK USAGE:" >> $REPORT
df -h >> $REPORT
echo "" >> $REPORT

echo "MEMORY:" >> $REPORT
free -h >> $REPORT
echo "" >> $REPORT

echo "TOP PROCESSES (CPU):" >> $REPORT
ps aux --sort=-%cpu | head -10 >> $REPORT

# Email report
cat $REPORT | mail -s "Daily Report - $DATE" admin@example.com
```

---

## Quick Reference

### Essential Monitoring Commands

| Task | Command |
|------|---------|
| CPU usage | `top` or `mpstat -P ALL` |
| Memory usage | `free -h` |
| Disk space | `df -h` |
| Disk I/O | `iostat -x` |
| Network | `ss -tunap` or `iftop` |
| System load | `uptime` |
| All processes | `ps aux` |
| System logs | `tail -f /var/log/syslog` |
| Service logs | `journalctl -u service -f` |

### Quick Health Check

| Command | What to Check |
|---------|---------------|
| `uptime` | Load average < CPU cores |
| `free -h` | Available memory > 10% |
| `df -h` | Disk usage < 90% |
| `top` | No single process using > 90% CPU |
| `ss -s` | Reasonable connection count |

---

## Best Practices

| Practice | Description |
|----------|-------------|
| **Regular monitoring** | Check system health daily |
| **Set baselines** | Know normal values for your system |
| **Automate alerts** | Script notifications for issues |
| **Log retention** | Keep logs for troubleshooting |
| **Trend analysis** | Track metrics over time |
| **Document thresholds** | Know when to act on alerts |
| **Test monitoring** | Verify alerts work |
