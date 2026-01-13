# Redirecting Call Traffic: How I Used a New Dial-Peer to Route External Calls to a New CUCM

This post breaks down how I used the Cisco VG CLI to point external calls to a new CUCM server, without interrupting service.

---

## Background

We were migrating users to a **new CUCM cluster**, but some external calls were still routing through the old CUCM. My goal was to **re-route outbound calls** to the new CUCM without disrupting current service.

---

## Step 1: Access the Voice Gateway

Used **PuTTY** to SSH into the voice gateway.

```bash
show dial-peer voice summary
```

Reviewed current dial-peers and identified the one sending calls to the old CUCM.

---

## Step 2: Create the New Dial-Peer

Instead of removing the old CUCM dial-peer, I **created a new one** pointing to the new CUCM:

```bash
dial-peer voice 4000 voip
 description External Calls to New CUCM
 destination-pattern 9T
 session target ipv4:10.10.10.5  ! new CUCM IP
 voice-class codec 1
 dtmf-relay rtp-nte
 no vad
```

- This kept the old config untouched in case of rollback.
- The `9T` pattern was chosen to match outbound dialing.

---

## Step 3: Testing & Verification

- Placed an outbound test call
- Pulled **CDR logs** from the CUCM

In the CDR:
- Verified `originalCalledPartyNumber`, `finalCalledPartyNumber`, and `destinationCUCM`
- Confirmed the call hit the new CUCM

---

## Step 4: Documenting in Excel

- Exported the CDR logs to CSV
- Used filters in Excel to isolate test calls
- Created a mini call flow table showing:
  - Call date/time
  - Caller
  - Called number
  - Trunk used
  - CUCM IP

---

## Outcome

> With a single CLI update, I corrected our outbound call flow to align with the new infrastructure, no outages.

---

## Lessons Learned

- You don’t always need to delete old dial-peers, layering new logic can be safer.
- Test, verify, document, especially when working on production voice systems.

---

*Posted by Jessica Anderson — UC Engineer | Voice + Cloud Hybrid | github.com/jessanderson*
