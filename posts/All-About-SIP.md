# All About SIP (Session Initiation Protocol)

**SIP** is the backbone of modern VoIP and Unified Communications systems. It’s a signaling protocol used to initiate, manage, and terminate voice, video, and messaging sessions over IP networks.



## What Is SIP?

- **Full Name**: Session Initiation Protocol
- **Defined By**: IETF RFC 3261
- **Purpose**: Establishes, modifies, and terminates multimedia sessions (voice, video, messaging).
- **Transport Protocols**: UDP, TCP, TLS
- **Common Ports**:
  - `5060` for SIP over UDP/TCP
  - `5061` for SIP over TLS (encrypted)



## SIP Core Concepts

### SIP URI
- Format: `sip:username@domain.com`
- Used to identify endpoints (users, devices, services)

### SIP Methods
| Method | Description |
|--------|-------------|
| `INVITE` | Starts a call/session |
| `ACK` | Confirms session establishment |
| `BYE` | Ends a session |
| `CANCEL` | Cancels a pending request |
| `REGISTER` | Registers a device/user with a SIP server |
| `OPTIONS` | Queries capabilities of a SIP endpoint |

### 🔹 SIP Headers
- Carry metadata like caller ID, codec preferences, routing info.
- Examples: `From`, `To`, `Contact`, `Via`, `Call-ID`, `CSeq`


## SIP Call Flow (Basic)

1. **User A sends INVITE to User B**
2. **User B responds with 100 Trying, 180 Ringing**
3. **User B answers with 200 OK**
4. **User A sends ACK**
5. **Media (RTP) begins**
6. **Call ends with BYE**



## SIP Security

- **TLS**: Encrypts SIP signaling (port 5061)
- **SRTP**: Encrypts media streams (used with SIP)
- **Authentication**: Digest authentication using `WWW-Authenticate` and `Authorization` headers



## SIP in Practice

### Used In:
- Microsoft Teams (via Direct Routing)
- Cisco CUCM
- Zoom Phone
- Asterisk
- FreeSWITCH
- Avaya, Mitel, and other PBXs

### SIP Trunking
- Replaces traditional PRI lines
- Connects enterprise PBX to PSTN via IP



## Troubleshooting SIP

- Use tools like:
  - **Wireshark**: Analyze SIP packets
  - **SIP ladder diagrams**: Visualize call flow
  - **SBC logs**: Trace signaling and media routing

- Common issues:
  - `404 Not Found`: User not registered or reachable
  - `403 Forbidden`: Permission denied
  - `488 Not Acceptable Here`: Codec mismatch
  - `408 Request Timeout`: No response from endpoint



## Summary

| Feature | Description |
|--------|-------------|
| Protocol Type | Signaling |
| Transport | UDP, TCP, TLS |
| Media | RTP (separate from SIP) |
| Use Cases | VoIP, video calls, messaging |
| Security | TLS for signaling, SRTP for media |


## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
