
# Cisco VG Initial Setup Checklist

### 1. **Basic Device Configuration**
```bash
hostname VG-HQ
enable secret [secure-password]
no ip domain-lookup
ip domain-name yourdomain.local
```

### 2. **Interface Configuration**
Assign IPs to interfaces:
```bash
interface GigabitEthernet0/0
 description Voice VLAN
 ip address 192.168.10.1 255.255.255.0
 no shutdown
```

### 3. **Routing**
Set default gateway or static routes:
```bash
ip route 0.0.0.0 0.0.0.0 192.168.10.254
```

---

## Voice Gateway Setup

### 4. **Voice Service Configuration**
```bash
voice service voip
 allow-connections sip to sip
 allow-connections h323 to h323
 allow-connections sip to h323
 allow-connections h323 to sip
 fax protocol t38 version 0 fallback none
```

### 5. **Enable DSP Farm (if needed)**
```bash
voice-card 0
 dspfarm
 dsp services dspfarm
```

---

## CUCM Integration

### 6. **SCCP for Media Resources**
```bash
sccp local GigabitEthernet0/0
sccp ccm 192.168.10.10 identifier 1 priority 1 version 6.0
sccp

sccp ccm group 1
 bind interface GigabitEthernet0/0
 associate ccm 1 priority 1
 associate profile 1 register MTP-VG
```

### 7. **MGCP or H.323/SIP Trunking**
For MGCP:
```bash
controller E1 0/0/0
 pri-group timeslots 1-31 service mgcp

mgcp
mgcp call-agent 192.168.10.10 2427 service-type mgcp
mgcp bind control source-interface GigabitEthernet0/0
mgcp bind media source-interface GigabitEthernet0/0
```

For SIP:
```bash
dial-peer voice 100 voip
 destination-pattern 9T
 session protocol sipv2
 session target ipv4:192.168.10.10
 codec g711ulaw
```

---

## Security & Access

### 8. **Enable SSH**
```bash
ip ssh version 2
username admin privilege 15 secret [secure-password]
line vty 0 4
 login local
 transport input ssh
```

### 9. **AAA & TACACS (Optional)**
```bash
aaa new-model
aaa authentication login default group tacacs+ local
tacacs-server host [IP] key [key]
```

---

## Final Steps

- **Save config**: `write memory`
- **Test connectivity**: ping CUCM, verify registration
- **Monitor call flow**: use `debug voip ccapi inout`, `show sccp`, `show mgcp`

