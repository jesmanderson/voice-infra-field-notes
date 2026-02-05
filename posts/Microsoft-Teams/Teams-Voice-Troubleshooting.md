# Teams Voice Call Flow Troubleshooting Guide

This guide outlines the general call flow for Microsoft Teams Voice and provides troubleshooting steps for diagnosing issues with outbound and inbound calls, particularly when using Direct Routing via Session Border Controllers (SBCs).



## Outbound Call Flow Overview

1. **User Initiates Call**  
   A Teams user dials an external number.

2. **Policy Check**  
   Microsoft Teams checks the user's assigned policies:
   - **Dial Plan**: Normalizes the number to E.164 format.
   - **Voice Routing Policy (VRP)**: Determines if the user is authorized to make the call.
   - **Voice Route**: Selects the appropriate route based on the dialed number and VRP.
   - **PSTN Usage**: Filters the route to link to the correct SBC.

3. **Call Routing via SBC**  
   - Microsoft sends the call to the SBC.
   - SBC processes the call using:
     - **Transformation Table**: Modifies the number if needed.
     - **Call Routing Table**: Determines the next hop.
     - **Signaling Group**: Manages SIP/media settings.
     - **Server Table**: Provides connection details.
   - SBC sends the call to the PSTN for final delivery.



## Outbound Troubleshooting Steps

### Step 1: Validate Dialed Number
- What number is the user dialing?
- Is it in the correct format (E.164)?
- Can the number be reached from other sources (e.g., mobile phone)?
- Is the issue isolated to one user, a group, or an entire site?

### Step 2: Check SBC Routing
- Confirm if the call is reaching the correct SBC.
- If using multiple SBCs, check both primary and secondary.

#### Actions:
- Log into the SBC and download call logs.
- Use log viewer tools to inspect SIP messages.
- Look for:
  - SIP errors
  - Whether the call reached the PSTN
  - Any transformation or routing issues

### Step 3: Simulate the Call
- Create a test Teams account with the same calling settings.
- Attempt the same call to identify misconfigured policies or routing rules.



## Inbound Call Flow Overview

1. **External Caller Initiates Call**  
   A call is placed from the PSTN or external VoIP source to a Teams-assigned number.

2. **Carrier Routes Call to SBC**  
   The external carrier sends the call to your organization's SBC.  
   SBC receives the SIP INVITE and begins processing.

3. **SBC Processes the Call**  
   - **Transformation Table**: Adjusts number format if needed.
   - **Call Routing Table**: Determines destination (Teams user).
   - **Signaling Group**: Applies SIP/media settings for Teams.
   - **Server Table**: Directs call to Microsoft Teams SIP endpoint.

4. **Microsoft Teams Receives the Call**  
   - Teams checks:
     - **User assignment** (number mapped to user)
     - **Calling policies**
     - **Availability and presence**
   - If valid, the call is delivered to the Teams client.



## Inbound Troubleshooting Steps

### Step 1: Confirm the Dialed Number
- Is the number in E.164 format?
- Is it assigned to a Teams user?
- Is the user licensed for Teams Phone?

### Step 2: Check SBC Logs
- Log into the SBC and locate the inbound SIP INVITE.
- Verify:
  - Call reached the SBC
  - Number transformation was correct
  - Routing table pointed to Teams
  - SIP signaling was successful

### Step 3: Validate Teams Configuration
- Use PowerShell or Teams Admin Center:
  - Confirm number assignment
  - Check user license and policies
  - Review call forwarding or blocking rules



## Summary

| Component | Role |
|-----------|------|
| **Dial Plan** | Normalizes dialed numbers |
| **Voice Routing Policy** | Authorizes call routing |
| **Voice Route** | Selects route based on number |
| **PSTN Usage** | Links route to SBC |
| **SBC** | Handles SIP signaling and PSTN handoff |
| **Teams** | Validates user and delivers call |




> This generalized guide is intended for Teams Voice administrators and UC engineers troubleshooting outbound and inbound call issues in environments using Direct Routing and SBCs. Always follow your organization's change management and escalation procedures when making configuration changes.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
