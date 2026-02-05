# Introduction to Microsoft Teams Voice

## Overview

Microsoft Teams Voice is a cloud-based telephony solution that integrates enterprise-grade calling capabilities directly into the Teams interface. It enables users to make and receive PSTN calls, manage voicemail, and collaborate; all within the Microsoft 365 ecosystem.

For UC engineers, Teams Voice represents a shift from traditional PBX systems like Cisco CUCM to a modern, cloud-native voice platform. This guide introduces the core concepts, architecture, and tasks involved in deploying and managing Teams Voice.



## Key Concepts

### What is Teams Voice?

Teams Voice allows users to:
- Make/receive PSTN calls
- Use voicemail and call forwarding
- Access call history and contacts
- Integrate with Microsoft 365 apps

### Core Components

| Component | Description |
|-----------|-------------|
| Phone System | Microsoft’s cloud-based PBX |
| Calling Plan | Microsoft-provided PSTN connectivity |
| Direct Routing | Use your own SBC to connect to PSTN |
| Operator Connect | PSTN service via certified telecom providers |



## Architecture Overview

- **Cloud-based**: No on-premise hardware required (unless using Direct Routing).
- **Integrated with Azure AD**: User identities and licenses managed via Microsoft 365.
- **SBCs (Session Border Controllers)**: Used in Direct Routing to connect Teams to external telephony.



## User Provisioning

Users are enabled for Teams Voice via:
- Microsoft 365 licensing (Phone System + Calling Plan or Direct Routing)
- Teams Admin Center or PowerShell
- Assigning phone numbers and voice policies



## Call Flow

1. User initiates a call in Teams.
2. Call is routed via Microsoft cloud or SBC (Direct Routing).
3. PSTN call is established.
4. Call logs and voicemail are stored in Exchange Online.



## Licensing

To enable Teams Voice, users need:
- Microsoft 365 E5 **or**
- Microsoft 365 E3 + Phone System add-on
- Optional: Calling Plan or Direct Routing setup



## Common Tasks for UC Engineers

- Assign phone numbers and voice policies
- Configure call queues and auto attendants
- Monitor call quality and usage
- Troubleshoot call failures and registration issues
- Manage SBCs and Direct Routing configurations



## Tools You’ll Use

- **Teams Admin Center**: GUI for managing users, policies, and call settings
- **PowerShell**: For bulk provisioning and advanced configuration
- **Call Quality Dashboard (CQD)**: Analyze call performance
- **Azure Monitor**: Optional for advanced alerting and logging



## Tips for New Engineers

- Understand the difference between **Calling Plan**, **Direct Routing**, and **Operator Connect**
- Use **PowerShell** for automation and bulk changes
- Monitor call quality regularly using CQD
- Document all changes and use **Change Requests** for production updates
- Collaborate with networking teams for SBC and firewall configurations



## Further Learning

- Microsoft Docs: [Teams Voice Overview- Microsoft Learn Modules]
- Internal lab simulations and sandbox environments


## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
