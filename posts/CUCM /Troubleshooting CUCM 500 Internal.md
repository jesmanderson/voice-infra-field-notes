# Troubleshooting CUCM 500 Internal Error on International Calls

## Overview
While testing international calls from **Microsoft Teams (Direct Routing) → Ribbon SBC → CUCM → Carrier**, calls were failing with **500 Internal Server Error** responses.  

Initial suspicion was Teams or SBC routing, but SIP traces showed the **500 was coming from CUCM itself**.  



## Root Cause
- CUCM attempted to allocate a **Media Termination Point (MTP)** for the call.  
- The site’s **Voice Gateway (VG) SCCP config** was still pointing at a **decommissioned CUCM Subscriber**.  
- Because of this, the VG’s **DSP resources (MTP/Transcoder/CFB)** never registered to an active CUCM node.  
- With no available MTP, CUCM failed the call and returned a **500 error**.



## Troubleshooting Steps
1. **Reviewed SBC logs**  
   - `500 Internal Server Error` received **from CUCM IP**.  
   - Confirmed INVITE digits normalized correctly → not a dial plan issue.  

2. **Checked CUCM Media Resources**  
   - In CUCM Admin → **Media Resources → MTP**  
   - Status = **Unregistered**.  

3. **Checked VG SCCP config**  
   ```bash
   show sccp

SCCP state = Down (registered to decom node).

### Resolution 
On the VG:
```bash
conf t
sccp ccm group 1
sccp
end
write memory 

# Then verified:
show sccp   
```
- SCCP Admin State = **UP**
- DSP profiles show **Registered**

In CUCM:

- MTP now shows **Registered**.
- Assigned to MRGL accessible by SIP trunk to SBC.  

### Validation
- Test international calls.
- Use **RTMT Session Trace** to confirm CUCM allocates MTP.
- Verify inbound, outbound, and emergency calls at the site. 

## Lessons Learned
- Always check **Media Resource registration (MTP/XCOD/CFB)** when CUCM sends 500 errors.
- If SCCP is tied to a decom node, DSP resources won’t register → CUCM call processing fails.
- SBC errors often reflect upstream failures — in this case, the SBC only relayed CUCM’s 500.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
