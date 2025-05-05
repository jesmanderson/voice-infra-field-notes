# CUCM Troubleshooting Field Notes

A quick-reference guide for diagnosing issues in a Cisco Unified Communications Manager (CUCM) cluster.

---

## 1. Node and Service Status

Run from the affected CUCM node:
```bash
utils system uptime
utils service list
```
Look for `STARTED` services:
- Cisco CallManager
- Cisco TFTP
- Cisco DB
- Cisco Tomcat

---

## 2. Database Replication Health

Run from the Publisher:
```bash
utils dbreplication runtimestate
utils dbreplication status
```
- Status `2 = good`
- `0 or 1 = bad`

---

## 3. Disk Space Check

```bash
show status
```
Look for:
- `/common` or `/dev/sda` usage
- CPU/memory usage

List large log files:
```bash
file list activelog platform/log/* detail
```

---

## 4. Phone Registration (RIS)

```bash
run sql select name,description from device where tkdeviceprotocol = 1
show risdb query phone
```

---

## 5. Restart Targeted Services

Only restart specific services:
```bash
utils service restart Cisco CallManager
utils service restart Cisco Tomcat
```
> Avoid restarting Cisco DB or Informix unless directed by TAC.

---

## 6. Alarms & Core Dumps

```bash
file list activelog /core detail
file list activelog cm/trace/ccm/sdi/detail
file view activelog cm/trace/ccm/sdi/ccm*.txt
```

---

## 7. Subscriber Health (GUI)

- **System > Server**
- **Cisco Unified Serviceability > Control Center - Network Services**

---

## 8. Logs to Collect for TAC

- CallManager traces
- Tomcat logs
- DB replication outputs
- Syslog/SNMP traps if configured

---

## Tools to Keep Ready

| Tool | Purpose |
|------|---------|
| RTMT | Real-time monitoring |
| SSH (Putty) | Direct CLI access |
| Prime Collaboration / DNA Center | Alerts and health monitoring |
| Ribbon SBC UI | Call tracing when CUCM fails |

---

**Maintained by:** UC Operations Team  