# Copilot-Assisted UC Troubleshooting (Teams + Ribbon SBC)

## Overview
This project explores how **Microsoft 365 Copilot** and **Azure AI** can support UC engineers in troubleshooting Microsoft Teams Direct Routing and Ribbon SBC call flow issues.  

Instead of manually combing through SIP logs, CDR records, and error codes, Copilot was used to **summarize issues, suggest probable causes, and draft remediation steps**.  

---

## Problem Statement
In UC operations, troubleshooting often involves:
- Reviewing **Teams call failure reports** in TAC/Admin Center  
- Pulling **SIP ladders** from Ribbon SBCs  
- Analyzing **CUCM/CDR logs** for error codes (e.g., 500 Internal Server Error)  
- Documenting findings for tickets  

This is time-consuming, inconsistent across engineers, and error-prone.  

---

## Copilot-Assisted Approach
1. **Log Collection**  
   - Export SIP ladder from Ribbon SBC (`Diagnostics → Call Trace`)  
   - Pull Teams Call Analytics report for the failing user  
   - Collect CUCM CDR snippet if involved  

2. **Copilot Input**  
   Example prompt:  
   > “Summarize this SBC SIP ladder. Identify error responses (4xx/5xx), explain likely cause, and suggest next troubleshooting steps.”  

3. **Copilot Output (Sample)**  
   - Summarized the call path: Teams → SBC → CUCM  
   - Identified `500 Internal Server Error` from CUCM node  
   - Suggested checking **MTP registration** or **translation patterns**  
   - Drafted remediation checklist  

4. **Engineer Validation**  
   - UC engineer validated Copilot’s suggestions against actual configs  
   - Confirmed root cause (MTP unregistered)  
   - Applied fix (SCCP reset on VG → MTP registered)  

---

## Outcome
- Reduced **initial triage time** from hours to minutes  
- Created **draft troubleshooting guides** Copilot could reuse  
- Improved **documentation quality** for tickets and change records  
- Demonstrated practical **AI augmentation** of UC operations  

---

## Future Enhancements
- Integrate with **Azure OpenAI** to build a Teams-based “UC Troubleshooting Assistant” bot  
- Feed historical SBC/CDR logs into an AI knowledge base for pattern recognition  
- Automate **post-mortem documentation** using Copilot + SharePoint  

---

## References
- [Microsoft Teams Copilot](https://learn.microsoft.com/en-us/microsoft-365-copilot/overview)  
- [Ribbon SBC Call Trace](https://support.ribboncommunications.com/)  
- [Cisco CDR Analysis](https://www.cisco.com/c/en/us/support/unified-communications/unified-communications-manager-callmanager/products-technical-reference-list.html)  
