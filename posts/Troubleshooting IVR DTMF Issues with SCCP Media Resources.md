# Troubleshooting IVR DTMF Issues with SCCP Media Resources

If you're a new engineer working with Cisco Unified Communications Manager (CUCM) and Voice Gateways (VGs), this guide will help you understand how SCCP media resources can solve common IVR keypad tone (DTMF) issues.

---

## Problem Scenario: IVR Not Responding to Keypad Tones

You're setting up an IVR (Interactive Voice Response) system. Callers reach the IVR, but when they press keys (DTMF tones), nothing happens; no routing, no menu selection.

This is a common issue and usually points to missing or misconfigured **media resources** in CUCM.

---

## Why DTMF Fails

DTMF (Dual-Tone Multi-Frequency) tones can be sent in different ways:
- **In-band**: tones are part of the audio stream.
- **Out-of-band**: tones are sent as signaling (e.g., RFC2833).

If CUCM or the IVR can't interpret the format, it won't respond to keypresses.

---

## How SCCP Media Resources Solve It

CUCM uses **SCCP (Skinny Client Control Protocol)** to register media resources from VGs:
- **MTP (Media Termination Point)**: helps with DTMF relay and codec mismatch.
- **Transcoder**: converts between codecs (e.g., G.729 ↔ G.711).
- **Conference Bridge**: mixes audio for multi-party calls (less relevant for IVR).

By registering these resources, CUCM can:
- Decode DTMF tones correctly.
- Transcode audio so IVR can understand it.
- Route calls based on keypresses.

---

## Configuration Overview

### On the Voice Gateway (VG):
1. Enable SCCP and bind to an interface.
2. Define CUCM IP and group.
3. Create DSP farm profiles:
   - `sccp ccm group 1`
   - `dspfarm profile 1 mtp`
   - `dspfarm profile 2 transcode`

### On CUCM:
1. Add the VG as an SCCP-controlled gateway.
2. Verify media resources are registered:
   - `Media Resources > Media Termination Point`
   - `Media Resources > Transcoder`
3. Assign resources to Media Resource Groups (MRGs).
4. Add MRGs to Media Resource Group Lists (MRGLs).
5. Assign MRGLs to IVR, trunks, or phones.

---

## Verification Steps

- Run `show sccp ccm group` on VG to confirm registration.
- Check CUCM GUI for media resource status.
- Make a test call and press keys — verify routing.
- Use RTMT or CDR logs to trace DTMF events.

---

## Best Practices

- Distribute media roles across multiple VGs.
- Ensure each VG has enough DSPs (PVDMs).
- Assign MRGLs carefully based on location and call flow.
- Monitor resource usage and registration status.

---

## Summary

SCCP media resources are essential for IVR functionality. Without them, CUCM may not decode DTMF tones or handle codec mismatches. 


