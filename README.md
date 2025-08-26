#!/bin/bash
#
# server-stats.sh
# A simple script to display server performance stats including network usage
#

echo "========================================"
echo "       SERVER PERFORMANCE REPORT        "
echo "========================================"
echo

# -------------------------
# OS & System Information
# -------------------------
echo ">>> System Information:"
echo "Hostname       : $(hostname)"
echo "OS Version     : $(grep PRETTY_NAME /etc/os-release | cut -d= -f2- | tr -d '\"')"
echo "Kernel         : $(uname -r)"
echo "Uptime         : $(uptime -p)"
echo "Load Average   : $(uptime | awk -F'load average:' '{ print $2 }')"
echo "Logged in Users: $(who | wc -l)"
echo

# -------------------------
# CPU Usage
# -------------------------
echo ">>> CPU Usage:"
if command -v mpstat &> /dev/null; then
    idle=$(mpstat 1 1 | awk '/Average/ && $12 ~ /[0-9.]+/ {print $12}')
    usage=$(echo "100 - $idle" | bc)
    printf "CPU Usage      : %.2f %%\n" "$usage"
else
    usage=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}')
    printf "CPU Usage      : %.2f %%\n" "$usage"
fi
echo

# -------------------------
# Memory Usage
# -------------------------
echo ">>> Memory Usage:"
free -h
echo
used=$(free | awk '/Mem:/ {print $3}')
total=$(free | awk '/Mem:/ {print $2}')
percent=$(free | awk '/Mem:/ {printf("%.2f", $3/$2 * 100)}')
echo "Memory Used    : $used / $total ($percent %)"
echo

# -------------------------
# Disk Usage
# -------------------------
echo ">>> Disk Usage (all mounted filesystems):"
df -h --total | grep 'total'
echo
percent=$(df --total | awk '/total/ {print $5}')
echo "Disk Used      : $percent"
echo

# -------------------------
# Top Processes
# -------------------------
echo ">>> Top 5 Processes by CPU usage:"
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head -n 6
echo

echo ">>> Top 5 Processes by Memory usage:"
ps -eo pid,comm,%cpu,%mem --sort=-%mem | head -n 6
echo

# -------------------------
# Network Statistics
# -------------------------
echo ">>> Network Statistics:"
# RX/TX bytes from /proc/net/dev
awk 'NR>2 {iface=$1; gsub(":", "", iface); rx=$2; tx=$10; printf "Interface: %-6s | RX: %-10s | TX: %-10s\n", iface, rx, tx}' /proc/net/dev
echo

# Check active network connections
echo ">>> Top 10 Active TCP Connections:"
if command -v ss &> /dev/null; then
    ss -tn state established | head -n 11
elif command -v netstat &> /dev/null; then
    netstat -tnp | grep ESTABLISHED | head -n 10
else
    echo "Neither ss nor netstat found to list connections."
fi
echo

# -------------------------
# Failed Login Attempts
# -------------------------
echo ">>> Failed Login Attempts (last 10):"
if [[ -f /var/log/auth.log ]]; then
    grep "Failed password" /var/log/auth.log | tail -n 10
elif [[ -f /var/log/secure ]]; then
    grep "Failed password" /var/log/secure | tail -n 10
else
    echo "No failed login log found."
fi
echo

# -------------------------
# End of Report
# -------------------------
echo "========================================"
echo "         END OF REPORT"
echo "========================================"
