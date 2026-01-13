# SBC (Ribbon) Concepts

As a UC engineer working in a hybrid world of CUCM, Teams, and global carrier interconnects, understanding Session Border Controllers (SBCs) is mission-critical. Here’s a breakdown of what an SBC is, why it’s used, and how I work with CRTs, TTs, and call flow configurations specifically on the Ribbon SBC 2000.

---

## What Is an SBC?

A **Session Border Controller (SBC)** is a device or virtual appliance that:
- Sits at the edge of your VoIP network
- Controls SIP signaling and RTP media
- Secures, routes, and normalizes VoIP traffic
- Interconnects internal voice systems (e.g., CUCM, Teams) with external systems (e.g., carriers)

### Key Functions:
- Protocol normalization (SIP to SIP variants)
- Topology hiding
- Codec translation
- Encryption (TLS/SRTP)
- Call routing + number transformation
- Session admission control + bandwidth policies

Ribbon SBCs, especially the SBC 2000, are widely used for Microsoft Teams Direct Routing and CUCM interop.

---

## Call Flow Configuration on Ribbon

The basic building blocks of a call flow inside a Ribbon SBC include:

### Call Routing Table (CRT)
- **Think of this like a routing map**
- CRTs determine **where to send the call** based on criteria (like called number, source IP, or signaling group)
- You can have multiple CRTs, inbound vs. outbound
- Each CRT entry includes:
  - Matching rule (pattern, SIP headers)
  - Target signaling group
  - Optional priority, filtering

### Transformation Table (TT)
- TT handles **digit manipulation**,  number rewriting
- Works similarly to CUCM translation patterns or route filters
- Can apply to:
  - Called number (CDPN)
  - Calling number (CGPN)
  - SIP headers (From, P-Asserted-Identity, etc.)
- TTs are assigned in the Signaling Group configuration or directly in the CRT

---

## Example Call Flow

1. **Inbound PSTN Call** from carrier
2. **SBC receives INVITE** on external signaling group
3. **TT normalizes called number** (e.g., strips +, formats to E.164)
4. **CRT checks match** and routes call to internal signaling group (e.g., CUCM or Teams)
5. **Call delivered internally** with rewritten number and required headers

---

## Real-World Notes
- I’ve used TTs to rewrite Brazilian carrier numbers to match CUCM route patterns
- CRTs are critical when multiple carriers share a SIP trunk, routing logic by source IP is common
- When calls fail silently, I always check:
  - If the CRT is matching
  - If the TT is rewriting as expected
  - If the signaling group is up and registered

---




