# CUCM Voice Call Flow Troubleshooting Guide

This guide outlines the general call flow and troubleshooting steps for Cisco Unified Communications Manager (CUCM) voice calling. It is designed for UC engineers managing enterprise voice infrastructure using CUCM.



## General Outbound Call Flow Overview

1. **User Initiates Call**
   - A user places a call from a Cisco IP phone or soft client.

2. **CUCM Call Processing**
   - CUCM receives the dialed digits.
   - Applies:
     - **Calling Search Space (CSS)** and **Partitions**
     - **Translation Patterns** and **Route Patterns**
     - **Route Lists** and **Route Groups**
     - **SIP Trunk or Gateway Selection**

3. **Call Routing to PSTN**
   - CUCM sends the call to the selected SIP trunk or gateway.
   - Gateway routes the call to the PSTN or carrier.



##  Outbound Troubleshooting Steps

### Step 1: Validate Dialed Number
- Is the number in the correct format?
- Is the number reachable from other endpoints?
- Is the issue isolated to one user, device, or site?

### Step 2: Check CUCM Configuration
- Review CSS and Partition assignments.
- Verify Route Pattern matches the dialed number.
- Confirm Route List and Route Group are configured correctly.
- Check SIP trunk or gateway status.

### Step 3: Use CUCM Logs and RTMT
- Use Real-Time Monitoring Tool (RTMT) or call detail records (CDRs).
- Look for call setup failures, SIP errors, or routing mismatches.



##  General Inbound Call Flow Overview

1. **External Caller Initiates Call**
   - A call is placed from the PSTN to a number assigned to CUCM.

2. **Carrier Routes Call to Gateway**
   - The carrier sends the call to your SIP trunk or gateway.

3. **CUCM Receives the Call**
   - CUCM processes the incoming digits.
   - Applies:
     - **Translation Patterns**
     - **Inbound CSS and Partitions**
     - **Directory Number (DN) Mapping**

4. **Call Delivered to Endpoint**
   - CUCM routes the call to the assigned IP phone or client.



## Inbound Troubleshooting Steps

### Step 1: Confirm Called Number
- Is the number assigned to a DN in CUCM?
- Is the DN reachable and active?

### Step 2: Check Gateway and Trunk
- Verify gateway is registered and operational.
- Confirm SIP trunk settings and inbound dial peers.

### Step 3: Review CUCM Routing
- Check inbound CSS and Partition.
- Validate Translation Patterns and DN mapping.

### Step 4: Use RTMT and Logs
- Analyze call flow using RTMT or CDRs.
- Look for SIP errors, routing failures, or endpoint issues.



## Tips

- Use **dialed number analyzer (DNA)** in CUCM to simulate call routing.
- Document all changes and test scenarios.
- Use ladder diagrams to trace SIP signaling when applicable.



## Summary

| Component | Role |
|-----------|------|
| **CSS/Partition** | Controls call routing permissions |
| **Translation Pattern** | Modifies dialed digits |
| **Route Pattern/List/Group** | Defines outbound routing |
| **SIP Trunk/Gateway** | Connects CUCM to PSTN |
| **Directory Number** | Maps inbound calls to endpoints |

---

> This guide helps UC engineers troubleshoot inbound and outbound call issues in Cisco Unified Communications Manager environments. Always follow your organization's change management and escalation procedures when making configuration changes.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
