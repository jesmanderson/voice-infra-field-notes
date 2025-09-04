# CUCM and Microsoft Teams Voice Interoperability

## Overview

As organizations transition from legacy PBX systems like Cisco CUCM to cloud-based platforms like Microsoft Teams Voice, **interoperability** becomes essential. This setup allows both systems to coexist during migration or support hybrid environments.

This guide introduces how CUCM and Teams Voice can work together using **Direct Routing**, **Session Border Controllers (SBCs)**, and **SIP trunking**.



## Key Concepts

### Why Interoperate?

- Gradual migration from CUCM to Teams Voice
- Support for analog devices or legacy integrations
- Business continuity during transition
- Centralized dial plan and call routing

### Core Components

| Component | Description |
|-----------|-------------|
| CUCM | On-premise call control system |
| Microsoft Teams | Cloud-based collaboration and calling platform |
| SBC (Session Border Controller) | Acts as a bridge between CUCM and Teams |
| Direct Routing | Microsoft’s method for connecting Teams to PSTN via SBC |
| SIP Trunk | Logical connection between CUCM and SBC |



## Architecture Overview

[CUCM] <--SIP--> [SBC] <--TLS/SRTP--> [Microsoft Teams (via Direct Routing)] 
- CUCM sends calls to SBC via SIP trunk
- SBC routes calls to Teams using Direct Routing
- Teams users can call CUCM extensions and vice versa 



## Call Flow Scenarios

1. **CUCM → Teams**: CUCM routes a call to the SBC, which forwards it to a Teams user.
2. **Teams → CUCM**: Teams user dials an internal extension; SBC routes it to CUCM.
3. **PSTN → Teams/CUCM**: SBC handles inbound PSTN calls and routes based on dial plan.



## Licensing & Requirements

- **Microsoft 365 E5** or E3 + Phone System license
- **SBC certified for Direct Routing**
- **Public DNS and certificates** for SBC
- **CUCM SIP trunk configuration**



## Common Tasks for UC Engineers

- Configure SIP trunk between CUCM and SBC
- Set up Direct Routing in Teams Admin Center
- Assign voice routing policies to Teams users
- Monitor call flows and troubleshoot interoperability issues
- Coordinate dial plan normalization between CUCM and Teams



## Tools You’ll Use

- **CUCM Admin GUI**: SIP trunk and route pattern configuration
- **Teams Admin Center**: Voice routing and user assignment
- **SBC Web UI or CLI**: SIP routing and TLS configuration
- **PowerShell**: Teams Voice configuration and diagnostics
- **Wireshark**: SIP and RTP packet analysis



## Tips for New Engineers

- Understand how dial plans differ between CUCM and Teams
- Always test call flows in both directions (CUCM ↔ Teams)
- Use certificates trusted by Microsoft for SBC TLS connections
- Document all routing rules and normalization patterns
- Monitor SBC logs for SIP errors and call failures


## Further Learning

- Microsoft Direct Routing Documentation
- Cisco CUCM SIP Trunk Configuration Guide
- SBC Vendor Documentation (e.g., AudioCodes, Ribbon)



## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)

