# CUCM SCCP Migration: APAC Sub Node Decommission

## Overview
This task was part of the APAC region sub-node decommissioning project. The goal was to migrate SCCP-based services and devices from an old CUCM subscriber node to a new one. This involved updating route lists, modifying SCCP CCM group configurations, monitoring registration status, and safely decommissioning the legacy VM. 

## What is SCCP?
SCCP (Skinny Client Control Protocol) is a Cisco proprietary signaling protocol used for communication between Cisco IP phones, voice gateways (VGs), and Cisco Unified Communications Manager (CUCM).
**Key Functions:**
- Registers analog ports (FXO/FXS)
- Manages DSP resources (transcoding, conferencing)
- Controls IP phones 

## How SCCP Connects VGs to CUCM 
To register a Cisco VG to CUCM using SCCP:
1. Enable SCCP on the VG 
```
sccp
```
2. Define CUCM nodes
```
sccp ccm 10.1.1.1 identifier 1 version 7.0 
```
3. Create SCCP CCM group
```
sccp ccm group 1
associate ccm 1 priority 1
bind interface GigabitEthernet0/0
```
4. Associate voice ports or DSP profiles
```
voice-port 0/1/0
sccp ccm group 1

dspfarm profile 1 transcode
associate application SCCP
```

This configuration allows CUCM to control analog ports and DSP services on the VG.

## Runtime Behavior
- SCCP acts as a control path between CUCM and the VG/DSPs.
- CUCM instructs the VG when to open ports, initiate calls, or manage media.
- RTP media streams flow directly between endpoints, out-of-band from SCCP signaling.

## Why SCCP Matters
If SCCP is misconfigured:
- Analog phones won’t register
- Transcoding and conferencing may fail
- Emergency calls from analog lines may break

SCCP is critical for environments relying on analog/digital ports or CUCM-controlled DSP services. 

## Migration Steps Taken 
1. Review current SCCP config
```
sh run | section sccp
```
2. Remove old CCM entries
```
no sccp ccm 172.29.1.130 identifier 1 version 7.0
no sccp ccm group 1
no sccp ccm 172.29.1.1 identifier 1 version 7.0
```
3. Add new CCM entries
```
sccp ccm 172.28.127.1 identifier 1 version 7.0
sccp ccm group 1
description *** Associate DSP farm to CCM ***
bind interface GigabitEthernet0/0
associate ccm 1 priority 1
associate ccm 2 priority 2
associate profile 3 register MTP-CHN-VGW
associate profile 2 register XCOD-SHE1-VGW
associate profile 1 register CFB-SHE1-VGW
switchover method immediate
switchback method immediate
```
4. Verify registration
```
sh run | section sccp
``` 

Other VGs automatically re-registered to the new node.

## Citations
- Cisco IOS Voice Command Reference
- Wikipedia: SCCP
- Cisco CUCM SCCP Integration Guide

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)