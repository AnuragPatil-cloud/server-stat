


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
git clone https://github.com/AnuragPatil-cloud/server-stats.git
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
Hostname       : ip-172-31-10-157
OS Version     : Ubuntu 24.04.3 LTS
Kernel         : 6.17.0-1007-aws
Uptime         : up 2 minutes
Load Average   :  0.02, 0.03, 0.01
Logged in Users: 2

>>> CPU Usage:
CPU Usage      : 0.00 %

>>> Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           911Mi       359Mi       298Mi       2.7Mi       411Mi       552Mi
Swap:             0B          0B          0B

Memory Used    : 367744 / 933328 (39.40 %)

>>> Disk Usage (all mounted filesystems):
total            8.4G  4.0G  4.4G  48% -

Disk Used      : 48%

>>> Top 5 Processes by CPU usage:
    PID COMMAND         %CPU %MEM
    545 snapd            0.9  4.2
    538 amazon-ssm-agen  0.8  2.3
      1 systemd          0.6  1.4
    122 systemd-journal  0.1  1.5
    184 systemd-udevd    0.1  0.8

>>> Top 5 Processes by Memory usage:
    PID COMMAND         %CPU %MEM
    545 snapd            0.9  4.2
    181 multipathd       0.0  2.9
    671 unattended-upgr  0.0  2.4
    538 amazon-ssm-agen  0.8  2.3
    532 networkd-dispat  0.0  2.2

>>> Network Statistics:
Interface: lo     | RX: 9016       | TX: 9016      
Interface: ens5   | RX: 286132     | TX: 89027     

>>> Top 10 Active TCP Connections:
Recv-Q Send-Q Local Address:Port Peer Address:Port Process
0      0      172.31.10.157:22   13.233.177.4:48426       

>>> Failed Login Attempts (last 10):

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
<img width="1902" height="733" alt="Screenshot 2026-03-13 195447" src="https://github.com/user-attachments/assets/91d9774c-1b20-41be-8b34-f5b6e24ddcaa" />

---

## Contributions

Pull requests, bug reports, and feature suggestions are welcome!

---

## Author

Anurag Patil  
https://github.com/AnuragPatil-cloud

---




