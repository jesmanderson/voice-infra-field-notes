# SCCP Media Resource Distribution in Cisco Voice Gateways

This guide introduces you to a  feature in Cisco Unified Communications: **SCCP-based media resource distribution across Voice Gateways (VGs)**.

---

## What is SCCP?

**SCCP (Skinny Client Control Protocol)** is a Cisco proprietary signaling protocol that allows devices like phones and **Voice Gateways** to register **media resources** with **Cisco Unified Communications Manager (CUCM)**.

Think of SCCP as the "language" that lets CUCM talk to your VG and say:
- “I need help decoding DTMF tones.”
- “Can you convert audio formats?”
- “Can you host a conference?”

---

## Media Resources Explained

Voice Gateways contain **DSPs (Digital Signal Processors)** — hardware chips that handle media tasks. You can configure these DSPs to register with CUCM as:

| Resource Type | Description | Example Use |
|---------------|-------------|-------------|
| **MTP (Media Termination Point)** | Helps with DTMF relay and codec mismatch | IVR digit collection |
| **Transcoder** | Converts between codecs (e.g., G.711 ↔ G.729) | Codec negotiation between endpoints |
| **Conference Bridge** | Mixes multiple audio streams | Ad-hoc or meet-me conferencing |

Each resource is defined as a **DSP farm profile** on the VG and registered to CUCM via SCCP.

---

## How Registration Works

1. Configure SCCP on the VG:
   - Bind SCCP to an interface
   - Point to CUCM IP
   - Define DSP farm profiles

2. VG registers each profile with CUCM:
   - CUCM sees them as media devices
   - They appear under `Media Resources` in CUCM

3. CUCM uses these resources during calls:
   - Based on need (DTMF, codec, conferencing)
   - Based on availability and configuration

---

## Distributing Resources Across Gateways

Here’s the magic: **You can distribute media roles across multiple gateways!**

| Gateway | Registered Resource |
|---------|---------------------|
| VG-HOU | MTP |
| VG-NYC | Transcoder |
| VG-LON | Conference Bridge |

CUCM doesn’t care which VG the resource came from — it just uses what’s available based on:

- **Media Resource Groups (MRGs)**
- **Media Resource Group Lists (MRGLs)**
- **Device Pool assignments**

This allows for:
- **Load balancing**
- **Redundancy**
- **Geographic optimization**

---

## Best Practices

- Distribute roles across gateways for scalability
- Ensure each VG has enough DSPs (PVDMs)
- Monitor registration status in CUCM
- Assign MRGLs properly to phones, trunks, IVRs

---

## Real-World Example

A caller reaches an IVR and presses keys:
- CUCM uses MTP to decode DTMF
- CUCM uses transcoder if codec mismatch occurs
- CUCM routes the call based on input

Without SCCP media resources, this flow may fail. With proper distribution, it works seamlessly!

---

## Final Thoughts

SCCP media resource distribution is a powerful tool in your Cisco VoIP toolbox. It allows CUCM to leverage DSPs across your network intelligently and flexibly.



