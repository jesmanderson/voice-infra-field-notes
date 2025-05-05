# Teams to PSTN Call Flow via Direct Routing (Markdown Guide)

This guide explains in simple terms how calls flow from Microsoft Teams through the SBC to the PSTN using Direct Routing.

---

## Step-by-Step Flow

### 1. **Dial Plan** (Teams Admin Center - Client Side)
- **Function:** Normalizes what the user dials to E.164 format.
- **Example:** `7135551234` -> `+17135551234`

---

### 2. **Voice Routing Policy** (Teams Admin Center - Assigned to User)
- **Function:** Determines what voice routes the user can access.
- **Think of it as:** A permission set for outbound calling paths.

---

### 3. **Voice Route** (Teams Admin Center - Routing Rules)
- **Function:** Matches the normalized number to a defined pattern.
- **Example:** `^\+1\d{10}$` - matches US numbers
- **Next step:** Points to a PSTN Usage

---

### 4. **PSTN Usage** (Teams Admin Center - Usage Profiles)
- **Function:** Links Voice Routes to the SBC.
- **Think of it as:** A logical connector from Teams to SBC.

---

### 5. **Signaling Group** (Ribbon SBC)
- **Function:** SIP link between SBC and Teams or CUCM or Carrier.
- **In this case:** Inbound call comes to `sip-Microsoft` signaling group.

---

### 6. **Transformation Table** (Ribbon SBC)
- **Function:** Modifies numbers (e.g. strips '+', adds prefixes).
- **Example:** `+17135551234` -> `17135551234`

---

### 7. **Call Routing Table** (Ribbon SBC)
- **Function:** Routes the transformed number to the correct signaling group (e.g., carrier or CUCM).
- **Think of it as:** The decision logic.

---

### 8. **Server Table** (Ribbon SBC)
- **Function:** Maps destination signaling group to an actual IP/FQDN of the endpoint.
- **Example:** `sip.carrier.com`

---

## Final Call Flow Diagram (Text-Based)

```
Teams User
   |
   | (1) Dial Plan
   v
(2) Voice Routing Policy
   |
(3) Voice Route
   |
(4) PSTN Usage
   |
   v
Ribbon SBC
   |
(5) Signaling Group: sip-Microsoft
   |
(6) Transformation Table
   |
(7) Call Routing Table
   |
(8) Server Table
   |
   v
PSTN (Phone Network)
```

---

**Maintained by:** UC Engineering Team  