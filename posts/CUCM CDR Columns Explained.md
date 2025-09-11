# CUCM CDR Columns Explained

## Summary

Cisco Unified Communications Manager (CUCM) generates **Call Detail Records (CDRs)** and **Call Management Records (CMRs)** to log call activity and media quality. These records are essential for troubleshooting, billing, and performance monitoring. This guide breaks down the most commonly used CDR columns into categories to help engineers quickly interpret call flows, identify issues, and correlate call legs across CUCM nodes.

---

## 🔹 Call Identification

| Column | Meaning |
| --- | --- |
| **cdrRecordType** | Type of record (e.g., 1 = normal call leg, 2 = transfer/forward leg). |
| **globalCallID_callManagerId** | ID of the CUCM node that processed the call leg. |
| **globalCallID_callId** | Unique call ID across all call legs — use this to group legs of the same call. |
| **origLegCallIdentifier** | ID for the originating side of the call leg. |
| **destLegCallIdentifier** | ID for the destination side of the call leg. |

---

## 🔹 Timestamps

| Column | Meaning |
| --- | --- |
| **dateTimeOrigination** | Epoch time (seconds since Jan 1 1970) when the call started. |
| **dateTimeConnect** | Time when the call was answered/connected. |
| **dateTimeDisconnect** | Time when the call ended. |
| **duration** | Length of the call (in seconds). |

---

## 🔹 Originating Side

| Column | Meaning |
| --- | --- |
| **origDeviceName** | Device name of the originating endpoint (e.g., SEP&lt;MAC&gt; for phones, SIPTrunk for trunks, VGW for gateways). |
| **callingPartyNumber** | Calling number (may be internal extension or full DID). |
| **origCause_location** | Location where the disconnect cause was generated (e.g., local, remote). |
| **origCause_value** | Disconnect cause code for the orig side (e.g., 16 = Normal Call Clearing, 1 = Unallocated Number). |
| **origIpv4v6Addr** | IP address of the CUCM node handling the originating side. |

---

## 🔹 Destination Side
| Column | Meaning |
| --- | --- |
| **destDeviceName** | Device name of the destination endpoint. |
| **originalCalledPartyNumber** | The originally dialed number. |
| **finalCalledPartyNumber** | The number that actually rang after any forwards/translations. |
| **destCause_location** | Location of the disconnect cause (like orig side). |
| **destCause_value** | Disconnect cause code from the destination perspective. |
| **destIpv4v6Addr** | IP address of the CUCM node handling the destination side. |

---

## 🔹 Quality of Service (QoS)

*(if CMR — Call Management Records are included with your CDR)*

| Column | Meaning |
| --- | --- |
| **packetsSent / packetsReceived** | RTP packets from each side. |
| **packetsLost** | RTP packets lost. |
| **jitter** | Jitter experienced in ms. |
| **latency** | End-to-end delay. |
| **video metrics** | If video calls, you’ll see separate video stream data. |

---

## 🔹 Billing / Tracking

| Column | Meaning |
| --- | --- |
| **origDevicePoolId / destDevicePoolId** | Device pool for orig/dest devices. |
| **outpulsedCallingPartyNumber** | The number actually sent to the PSTN or trunk after translations. |
| **outpulsedCalledPartyNumber** | The final called number that left CUCM. |
| **callTerminationOnBehalfOf** | Indicates if CUCM, gateway, or endpoint terminated the call. |
| **lastRedirectDn** | The last redirecting number (important for forwarded calls, voicemail). |
| **finalRedirectDn** | Final redirect before call ended (e.g., VM pilot). |

---

## 🔹 Cause Codes Reference

CUCM uses standardized **Q.850 cause codes** to indicate why a call was disconnected. These codes appear in `origCause_value` and `destCause_value` fields.

| Code | Meaning |
|------|--------|
| **1** | Unallocated (unassigned) number |
| **16** | Normal call clearing |
| **17** | User busy |
| **18** | No user responding |
| **19** | No answer from user (user alerted) |
| **21** | Call rejected |
| **22** | Number changed |
| **27** | Destination out of order |
| **28** | Invalid number format |
| **29** | Facility rejected |
| **31** | Normal, unspecified |
| **34** | No circuit/channel available |
| **38** | Network out of order |
| **41** | Temporary failure |
| **42** | Switching equipment congestion |
| **47** | Resource unavailable |
| **57** | Bearer capability not authorized |
| **58** | Bearer capability not available |
| **65** | Bearer capability not implemented |
| **79** | Service or option not implemented |
| **87** | User not member of call group |
| **88** | Incompatible destination |
| **111** | Protocol error, unspecified |
| **127** | Interworking, unspecified |

> Use these codes to understand why a call failed or was terminated. For example, code **16** means the call ended normally, while **1** or **28** may indicate dialing issues.

---

## How to Use These Columns in Practice

- **Find who called who** → `callingPartyNumber` → `finalCalledPartyNumber`
- **Find which CUCM node handled the call** → `origIpv4v6Addr` and `destIpv4v6Addr`
- **Group call legs together** → use `globalCallID_callId`
- **Check disconnect reason** → `origCause_value` / `destCause_value` (use Cisco cause code list)
- **Check media quality** → look at associated **CMR file** (QoS metrics)

---

## Example Call Flow in CDR

1. User A (1001) dials User B (2002)  
   - `callingPartyNumber = 1001`  
   - `originalCalledPartyNumber = 2002`  
2. Call gets forwarded to voicemail (2002 → 5555)  
   - `finalCalledPartyNumber = 5555`  
   - `lastRedirectDn = 2002`  
3. Call ends normally  
   - `origCause_value = 16 (Normal Call Clearing)`  
   - `destCause_value = 16`  
4. Call legs show CUCM nodes involved  
   - `origIpv4v6Addr = 10.1.1.10 (Pub)`  
   - `destIpv4v6Addr = 10.2.2.20 (Sub-SIN)`  

---

⚠️ Different CUCM versions can add/remove columns — but the above are the **core fields** you’ll use 90% of the time for troubleshooting.
