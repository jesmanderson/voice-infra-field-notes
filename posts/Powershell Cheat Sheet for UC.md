# PowerShell Cheat Sheet for UC Engineers

## Overview
This cheat sheet provides quick-reference PowerShell commands and scripts commonly used by Unified Communications (UC) engineers for managing Windows servers, services, logs, network settings, and automation tasks.

---

## 1. System Information

### 🔹 Get Computer Info
```powershell
Get-ComputerInfo
```

### 🔹 Get OS Version
```powershell
(Get-WmiObject -Class Win32_OperatingSystem).Caption
```

### 🔹 Get System Uptime
```powershell
(Get-CimInstance Win32_OperatingSystem).LastBootUpTime
```

---

## 2. Service Management

### 🔹 List All Services
```powershell
Get-Service
```

### 🔹 Check Specific Service Status
```powershell
Get-Service -Name 'Cisco CallManager'
```

### 🔹 Start/Stop/Restart a Service
```powershell
Start-Service -Name 'Cisco CallManager'
Stop-Service -Name 'Cisco CallManager'
Restart-Service -Name 'Cisco CallManager'
```

---

## 3. Network Diagnostics

### 🔹 Ping a Host
```powershell
Test-Connection -ComputerName 8.8.8.8 -Count 4
```

### 🔹 Get IP Configuration
```powershell
Get-NetIPAddress
```

### 🔹 Get DNS Configuration
```powershell
Get-DnsClientServerAddress
```

---

## 4. Log Management

### 🔹 View Event Logs
```powershell
Get-EventLog -LogName Application -Newest 50
```

### 🔹 Filter Logs by Source
```powershell
Get-EventLog -LogName System -Source 'Cisco Unified CM' -Newest 20
```

### 🔹 Export Logs to CSV
```powershell
Get-EventLog -LogName System -Newest 100 | Export-Csv -Path "C:\Logs\SystemLogs.csv" -NoTypeInformation
```

---

## 5. File Operations

### 🔹 List Files in a Directory
```powershell
Get-ChildItem -Path "C:\CUCM_Backups"
```

### 🔹 Copy Files
```powershell
Copy-Item -Path "C:\CUCM_Backups\config.xml" -Destination "D:\Backup\config.xml"
```

### 🔹 Compress Files
```powershell
Compress-Archive -Path "C:\CUCM_Backups\*" -DestinationPath "D:\Backup\CUCM_Backup.zip"
```

---

## 6. Remote Access & Automation

### 🔹 Run Command on Remote Server
```powershell
Invoke-Command -ComputerName 'CUCM-Node1' -ScriptBlock { Get-Service }
```

### 🔹 Create Scheduled Task
```powershell
$action = New-ScheduledTaskAction -Execute "PowerShell.exe" -Argument "-File C:\Scripts\CUCMHealthCheck.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At 3am
Register-ScheduledTask -TaskName "CUCM Health Check" -Action $action -Trigger $trigger
```

---

## 7. Security & Credentials

### 🔹 Securely Store Credentials
```powershell
$cred = Get-Credential
$cred | Export-Clixml -Path "C:\Secure\CUCMCred.xml"
```

### 🔹 Import Stored Credentials
```powershell
$cred = Import-Clixml -Path "C:\Secure\CUCMCred.xml"
```

---

## 8. Useful One-Liners

### 🔹 Check if Port is Listening
```powershell
Test-NetConnection -ComputerName 'CUCM-Pub' -Port 5060
```

### 🔹 Get Disk Space
```powershell
Get-PSDrive -PSProvider 'FileSystem'
```

### 🔹 List Scheduled Tasks
```powershell
Get-ScheduledTask
```

---

## Resources

- Microsoft PowerShell Documentation
- Cisco UC CLI Reference
- Windows Event Log Reference

---
