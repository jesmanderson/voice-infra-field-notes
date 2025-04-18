# 📞 How I Troubleshoot SIP Call Flows (Field Notes)

As a UC engineer working with CUCM, Ribbon SBC, and Teams Voice, one of the most important skills I’ve developed is being able to troubleshoot SIP call flows quickly and confidently. Here’s a breakdown of my personal workflow that I follow when something goes wrong with voice routing.

---

## 🧭 1. Understand the Call Path
Before anything else, I sketch (mentally or visually) the expected call flow:

Example:
```
Caller (Teams or PSTN) → SBC → CUCM → VG or Endpoint (e.g., phone, fax)
```

This helps narrow down where to start based on symptoms (e.g., no audio vs. call fails immediately).

---

## 🔍 2. Collect Key Info
I always start with this checklist:
- Calling number and called number
- Timestamp of the failed call attempt
- Is the call inbound or outbound?
- Does it fail for all users or just one?
- What message or tone does the user hear?

---

## 🧪 3. Check SIP Signaling Logs

### 📍 SBC (Ribbon)
- Go to **Call Logs** or **SIP Ladder Diagrams**
- Look for:
  - `INVITE`, `100 Trying`, `183 Session Progress`, `200 OK`, `BYE`
  - Any `404`, `403`, or `503` errors
  - Media IP addresses (for one-way audio issues)

### 🧭 CUCM
- Use **CDR / CMR** to trace calls:
  - Filter by originalCalledPartyNumber or callingPartyNumber
  - Check if the call ever reaches CUCM
- Look for Translation Patterns or Route Patterns mismatching

---

## ⚙️ 4. Test with Dialed Number Analyzer (CUCM)
- Use **DNA Tool** to simulate how CUCM handles the dialed number
- Look at:
  - Translation Pattern matches
  - Route List or Route Group paths

---

## 🧰 5. Use Wireshark (Only When Needed)
- Run a packet capture on SBC or VG
- Filter with: `sip` or `ip.addr==<IP>`
- Follow the SIP conversation
- Check for RTP stream negotiation and media path

---

## 🧹 6. Common Fixes
- Dial Peer not pointing to correct session target
- Missing Route Pattern for full E.164 number
- Translation Pattern rewriting issue
- Mismatched codec negotiation between devices
- Firewall/NAT blocking RTP
- Wrong Calling Search Space (CSS) or Partition

---

## 💬 Example Real Ticket
> Caller says: "Call rings but no audio"

What I did:
- Verified RTP never reached the remote party
- Found that SBC was negotiating media with CUCM sub, but call was pinned to a different server
- Corrected Region preference in CUCM to route RTP to the right server

---

## ✍🏽 Final Notes
Troubleshooting SIP is like reading a story — the `INVITE` is the intro, the `200 OK` is the peak, and the `BYE` is the ending. My job is to find where the story breaks and why.

Let me know if you want my SIP log analysis templates or want to turn this into a real video tutorial!