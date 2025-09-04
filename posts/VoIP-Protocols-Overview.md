# VoIP Protocols Overview

Voice over IP (VoIP) enables voice communication over IP networks, replacing traditional telephony systems. Understanding the core protocols used in VoIP is essential for UC engineers, network admins, and anyone working with voice infrastructure.



## Key VoIP Protocols

### **SIP (Session Initiation Protocol)**
- **Purpose**: Establishes, modifies, and terminates voice/video sessions.
- **Used For**: Call setup, registration, presence, and signaling.
- **Ports**: Typically UDP/TCP 5060 (unencrypted), 5061 (TLS encrypted).
- **Common in**: Microsoft Teams, Cisco CUCM, Zoom, Asterisk.

### **RTP (Real-Time Transport Protocol)**
- **Purpose**: Transports audio and video media streams.
- **Used For**: Actual voice data transmission during a call.
- **Ports**: Dynamic UDP ports (often 16384–32767).
- **Works With**: SIP for signaling, RTP for media.

### **RTCP (RTP Control Protocol)**
- **Purpose**: Monitors RTP stream quality and provides feedback.
- **Used For**: Jitter, packet loss, latency reporting.
- **Helps With**: QoS monitoring and troubleshooting.

### **MGCP (Media Gateway Control Protocol)**
- **Purpose**: Controls media gateways from a call control device.
- **Used In**: Legacy systems and some Cisco deployments.
- **Replaced By**: SIP in most modern environments.

### **H.323**
- **Purpose**: Older protocol suite for multimedia communication.
- **Used In**: Early VoIP systems, video conferencing.
- **Status**: Largely replaced by SIP.



## Supporting Protocols

### **DNS & SRV Records**
- Used to locate SIP servers and services.
- Important for failover and load balancing.

### **STUN/TURN/ICE**
- Used in NAT traversal for peer-to-peer VoIP.
- Common in WebRTC and cloud-based voice platforms.

### **TLS & SRTP**
- Provide encryption for SIP signaling and RTP media.
- Essential for secure VoIP deployments.



## Protocol Summary Table

| Protocol | Role | Transport | Encryption |
|----------|------|-----------|------------|
| SIP      | Call signaling | UDP/TCP | TLS (5061) |
| RTP      | Media transport | UDP | SRTP |
| RTCP     | Media quality feedback | UDP | Optional |
| MGCP     | Gateway control | UDP | None |
| H.323    | Multimedia signaling | TCP/UDP | Optional |


## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)