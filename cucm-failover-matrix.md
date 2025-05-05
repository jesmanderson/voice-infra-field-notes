# CUCM Fallback Routing Matrix

This matrix outlines the impact and recommended redundancy strategies if the `cucm-central` cluster fails.

| Service / Call Flow                   | Impact if cucm-global Fails                                                    | Recommended Fallback / Redundancy                                |
|--------------------------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------|
| **Desk Phone Registration**          | Phones go offline unless SRST is configured                                   | Enable SRST on local routers                                     |
| **Analog Lines (paging, elevator)**  | Analog devices go down if they rely on cucm-global gateways                   | Use local FXO/FXS gateways with analog fallback                  |
| **Emergency Calling**                | Emergency calls fail if tied to cucm-global trunks                             | Route emergency calls via local PSTN or SRST gateway             |
| **Voicemail / Auto Attendants**      | Voicemail fails unless Unity or cloud voicemail has HA                         | Deploy Unity HA or cloud voicemail                               |
| **CUCM Trunk to SBC**                | Call routing from SBC to cucm-global fails                                     | Add backup CUCMs in SBC routing table                            |
| **Inter-site Calling (e.g., Brazil â†’ Global)** | Calls fail unless intercluster fallback routes exist                    | Use intercluster trunks to cucm-brazil / cucm-emea               |
| **Teams to CUCM Call Flow**          | Fails unless SBC routes to another CUCM                                        | Add secondary CUCM trunk on SBC                                  |
| **CUCM Call Processing**             | Call routing fails unless other CUCMs can take over                            | Enable redundancy via CUCM clustering or SIP trunk failover      |

---

**Maintained by:** UC Infrastructure Team 