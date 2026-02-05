# Ribbon SBC for Microsoft Teams Direct Routing

## Overview

As Unified Communications engineers, understanding how to bridge Microsoft Teams with traditional telephony systems is essential in hybrid environments. Ribbon Session Border Controllers (SBCs) are Microsoft-certified for Direct Routing, enabling secure SIP connectivity between Teams and platforms like CUCM or PSTN providers.

This guide walks through the architecture, configuration, and operational tasks involved in deploying Ribbon SBCs for Direct Routing. It’s designed to help engineers build foundational knowledge and confidently manage hybrid voice environments.



## Key Concepts

### What is Direct Routing?

Direct Routing allows Microsoft Teams to connect to the PSTN using:
- A certified SBC (like Ribbon)
- SIP trunks to CUCM or telecom providers
- Microsoft 365 Phone System licenses

  *This setup enables Teams users to make and receive external calls while integrating with existing voice infrastructure.*

### Why Use Ribbon SBC?

- Officially certified for Microsoft Teams
- Handles SIP normalization and media translation
- Supports hybrid voice scenarios (CUCM ↔ Teams ↔ PSTN)
- Provides robust security, logging, and call routing control



## Architecture Overview

[CUCM] <--SIP--> [Ribbon SBC] <--TLS/SRTP--> [Microsoft Teams (via Direct Routing)] | [PSTN] 

- Ribbon SBC acts as the intermediary between CUCM and Teams
- Manages SIP signaling and media conversion
- Supports TLS encryption and SRTP for secure Teams communication



## Configuration Steps

### 1. **Prepare the SBC**
- Ensure firmware is up to date
- Enable Direct Routing features
- Configure network interfaces (LAN/WAN)

### 2. **Configure SIP Trunks**
- **CUCM → SBC**: Create a SIP trunk in CUCM pointing to the SBC
- **SBC → Teams**: Configure a SIP trunk using Microsoft’s FQDNs and TLS

### 3. **Certificates**
- Install a public certificate trusted by Microsoft (e.g., DigiCert, GoDaddy)
- Bind the cert to the TLS interface used for Teams

### 4. **Routing Rules**
- Define call routing logic:
  - CUCM extensions → Teams
  - Teams DIDs → CUCM or PSTN
- Normalize dial plans as needed

### 5. **Firewall & DNS**
- Open required ports (SIP, RTP, HTTPS)
- Ensure SBC can resolve Microsoft SIP domains



## Common Tasks for UC Engineers

- Monitor SIP call flows and logs
- Troubleshoot TLS handshake or media issues
- Update dial plans and normalization rules
- Validate call routing between CUCM, Teams, and PSTN
- Backup and export SBC configuration



## Tools You’ll Use

- **Ribbon SBC Web UI**: Main configuration interface
- **Wireshark**: SIP and RTP packet analysis
- **PowerShell**: Teams Voice configuration
- **Teams Admin Center**: Assign voice routes and policies
- **RTMT / CUCM GUI**: Monitor CUCM SIP trunk status



## Tips for New Engineers

- Always test TLS connectivity to Teams first
- Use SIP OPTIONS ping to monitor trunk health
- Document all dial plan normalization rules
- Use Ribbon logs to trace call failures
- Coordinate with security team for firewall and cert management



## Further Learning

- Ribbon SBC Documentation
- Microsoft Direct Routing Guide
- CUCM SIP Trunk Configuration


## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
