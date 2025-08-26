


# Server Stats - Bash Server Performance Monitor

A lightweight and easy-to-use Bash script to display an at-a-glance summary of key server performance metrics on any Linux machine.

---

## Features

- **System Information:** Hostname, OS version, kernel, uptime, load average, logged-in users
- **CPU Usage:** Display current total CPU usage percentage
- **Memory Usage:** Show used/free memory with percentage breakdown
- **Disk Usage:** Totals for disk space used/free with percentages
- **Top Processes:** Lists the top 5 processes by CPU and memory consumption
- **Network Stats:** Shows RX/TX bytes for each interface, including top active TCP connections
- **Security Insight:** Displays the last 10 failed login attempts (if available)
- **Fully Shell-Based:** Uses standard Linux tools (`awk`, `ps`, `top`, `free`, `df`, `mpstat`, `ss`, `netstat`) to maximize compatibility

---

## Usage

### 1. Download or Clone this Repository

```
git clone https://github.com/yourusername/server-stats.git
cd server-stats
```

### 2. Make the Script Executable

```
chmod +x server-stats.sh
```

### 3. Run the Script

```
./server-stats.sh
```

#### Save the output to a file (optional):

```
./server-stats.sh > server-stats-report.txt
```

#### Display and save output at the same time:

```
./server-stats.sh | tee server-stats-report.txt
```

---

## Example Output

```
========================================
       SERVER PERFORMANCE REPORT
========================================

>>> System Information:
Hostname       : myserver
OS Version     : Ubuntu 20.04.6 LTS
Kernel         : 5.15.0-91-generic
Uptime         : up 12 hours, 35 minutes
Load Average   : 0.45, 0.32, 0.39
Logged in Users: 2

>>> CPU Usage:
CPU Usage      : 7.43%

>>> Memory Usage:
              total        used        free      shared  buff/cache   available
Mem:           8G          3G          1G        200M          4G          5G

Memory Used    : 3162780 / 8157516 (38.77%)

>>> Disk Usage (all mounted filesystems):
total        100G   60G   35G  63%

Disk Used      : 63%

>>> Top 5 Processes by CPU usage:
  PID COMMAND %CPU %MEM
 2312 java     25.3 15.2
 1843 postgres 10.0  1.8
 ...

>>> Top 5 Processes by Memory usage:
  PID COMMAND %CPU %MEM
 2312 java     25.3 15.2
 ...

>>> Network Statistics:
Interface: lo     | RX: 12345      | TX: 12345
Interface: eth0   | RX: 20485760   | TX: 12543678

>>> Top 10 Active TCP Connections:
State       Recv-Q Send-Q       Local Address:Port       Peer Address:Port
ESTAB       0      0            192.168.0.10:22         203.0.113.50:45678
...

>>> Failed Login Attempts (last 10):
Aug 25 09:22:45 myserver sshd: Failed password for root ...

========================================
         END OF REPORT
========================================
```

---

## Requirements

- Bash (any Linux shell)
- Standard Linux tools: `awk`, `ps`, `top`, `free`, `df`, `mpstat`, `ss` or `netstat` (as available)
- Access to `/var/log/auth.log` or `/var/log/secure` for failed login statistics

---

## License

This project is licensed under the MIT License.

---

## Contributions

Pull requests, bug reports, and feature suggestions are welcome!

---

## Author

[Anurag Patil]  
[Your GitHub Profile URL]

---
```

***

