# Using PuTTY, `show`, and `utils` Commands for CUCM Troubleshooting

## Overview
This guide explains how to use **PuTTY** to access Cisco Unified Communications Manager (CUCM) via SSH and leverage key CLI commands (`show` and `utils`) for troubleshooting and diagnostics, with real-world examples.
https://yurisk.info/2015/08/15/useful-cli-commands-for-cisco-cucm/

---

## 1. Accessing CUCM via PuTTY

### Prerequisites:
- CUCM IP address or hostname
- SSH access enabled
- Platform admin credentials

### Steps:
1. Launch **PuTTY**.
2. Enter CUCM's IP address (e.g., `10.10.20.15`) in the **Host Name** field.
3. Set **Port** to `22` and choose **SSH**.
4. Click **Open**.
5. Log in with your CUCM **platform credentials**.

---

## 2. Common `show` Commands

### 🔹 `show status`
Displays system health and resource usage.

**Example Output:**
```bash
Hostname: cucm-pub
Uptime: 45 days
CPU Usage: 12%
Memory Usage: 65%
Disk Usage: 70%
```

---

### 🔹 `show network eth0`
Shows IP settings for the primary NIC.

**Example Output:**
```bash
eth0 Link encap:Ethernet
inet addr:10.10.20.15  Bcast:10.10.20.255  Mask:255.255.255.0
```

---

### 🔹 `show version active`
Displays the active CUCM software version.

**Example Output:**
```bash
Active Version: 14.0.1.10000-20
```

---

### 🔹 `show hardware`
Lists hardware specs.

**Example Output:**
```bash
CPU: Intel Xeon E5-2620
Memory: 16 GB
Disk: 500 GB
```

---

## 3. Common `utils` Commands

### 🔹 `utils service list`
Lists all CUCM services and their status.

**Example Output:**
```bash
Cisco CallManager: Running
Cisco TFTP: Running
Cisco Tomcat: Running
Cisco DRF Master: Not Running
```

---

### 🔹 `utils service restart Cisco CallManager`
Restarts the CallManager service.

**Example Output:**
```bash
Service Cisco CallManager has been restarted successfully.
```

---

### 🔹 `utils network ping <IP>`
Tests connectivity to a remote host.

**Example:**
```bash
utils network ping 8.8.8.8
```

**Example Output:**
```bash
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=117 time=10.2 ms
```

---

### 🔹 `utils network traceroute <IP>`
Diagnoses routing path to a host.

**Example:**
```bash
utils network traceroute 8.8.8.8
```

**Example Output:**
```bash
1  10.10.20.1
2  172.16.0.1
3  192.168.1.1
4  8.8.8.8
```

---

### 🔹 `utils create report`
Generates a diagnostic report.

**Example Output:**
```bash
Report successfully created at /common/log/report_20250911.tar.gz
```

---

## 4. Tips & Best Practices

- Use `show` commands for passive diagnostics.
- Use `utils` commands for active troubleshooting.
- Avoid restarting services during production hours.
- Always document findings and actions taken.

---

## 5. Additional Resources

- Cisco CLI Reference Guide for CUCM
- Cisco Unified Reporting Tool
- Real-Time Monitoring Tool (RTMT)

---