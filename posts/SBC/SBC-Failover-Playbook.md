# SBC Failover Playbook

## Overview
This playbook outlines the impact and recommended mitigation strategies if any signaling group on Ribbon SBC `sbc-amas01` fails. Use this to guide troubleshooting and redundancy planning.

---

## Signaling Group Failures & Response

### 1. `sip-Microsoft`
- **Function:** Direct Routing to Microsoft Teams (SIP trunk)
- **Failure Scenario:** TLS failure, DNS resolution issue, expired certificate
- **Impact:**
  - Teams to PSTN and PSTN to Teams calls will fail
  - No backup = full outage
- **Mitigation:**
  - Use all 3 Microsoft SIP domains:
    - `sip.pstnhub.microsoft.com`
    - `sip.pstnhub.us`, `sip.pstnhub.emea`, `sip.pstnhub.apac`
  - Enable SIP Options
  - Use DNS SRV for geo-redundancy

---

### 2. `sip-telecom`
- **Function:** PSTN SIP trunk (carrier-based)
- **Failure Scenario:** Carrier down or SBC unable to reach provider
- **Impact:**
  - Inbound and outbound PSTN calling fails
- **Mitigation:**
  - Use backup telecom provider
  - Route outbound calls through Microsoft or alternate SBC

---

### 3. `sbc-emea`
- **Function:** Peer SBC in EMEA region
- **Failure Scenario:** WAN issue or regional SBC down
- **Impact:**
  - Intra-org calls to/from EMEA fail
- **Mitigation:**
  - Failover route to another SBC (`sbc-amas02` or `sbc-apac`)

---


### 4. `sbc-apac`
- **Function:** APAC regional SBC peer
- **Failure Scenario:** SIP or WAN link failure
- **Impact:**
  - APAC region calls fail
- **Mitigation:**
  - Backup route via `sbc-emea` or `sbc-amas02`

---

### 6. `sbc-amas02`
- **Function:** Backup SBC (High Availability)
- **Failure Scenario:** Redundancy broken or node unreachable
- **Impact:**
  - If `sbc-amas01` fails, there's no failover
- **Mitigation:**
  - Validate HA setup, test failover regularly
  - Monitor with SNMP/syslog

---

### 7. `cucm-central`
- **Function:** Central CUCM fallback
- **Failure Scenario:** SIP trunk failure
- **Impact:**
  - Central call routing, paging, or voicemail may be affected
- **Mitigation:**
  - Use dual registration
  - Prioritize emergency service redundancy

---

## Best Practices for Redundancy
- Enable SIP OPTIONS for health checks
- Use DNS SRV for Teams SIP routes
- Configure fallback in Ribbon routing table
- Monitor SBC health and certificate expirations
- Periodic failover testing (especially HA)

---

**Maintained by:** UC Engineering Team  
