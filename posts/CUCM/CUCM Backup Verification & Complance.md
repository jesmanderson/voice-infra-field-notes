# CUCM Backup Verification & Complance 

## Overview 
As a Unified Communications engineer, maintaining reliable backups of Cisco Unified Communications Manager (CUCM) is not just a technical task, it’s a critical part of business continuity and disaster recovery strategy. This guide outlines how to verify CUCM backups, document results, and ensure compliance with internal and external audit requirements.

Whether you're new to CUCM or transitioning into a more senior role, understanding the backup lifecycle and its operational dependencies is essential.

## Key Features 
1. Automated Scheduled Backups
    - CUCM uses its built-in Disaster Recovery System (DRS) to schedule backups during off-peak hours.
    - Backups should be configured to run at least weekly, with retention policies aligned to business requirements.
2. Centralized Management
    - All backup operations are initiated from the CUCM Publisher node via the web-based GUI.
    - Only the Publisher has write access to the configuration database, making it the authoritative source for backup initiation.
3. Multi-Node Backup Coverage
    - DRS supports full backup of:
        - CallManager (CM) database
        - TFTP
        - CDR (Call Detail Records)
        - MOH (Music on Hold)
4. Audit and Compliance Tracking
    - Weekly backup logs are maintained for audit readiness.
    - Failed backups must be escalated and documented with remediation steps.

## Technologies Used 
| Technology | Description |
| ---------- | ----------- | 
| CUCM       | Cisco UC Manager - Core VoIP call control system |
| DRS        | Disater Recovery System - Built-in CUCM for scheduling and managing backups |
| NFS (STFP Server) | Remote server where CUCM stores backups |
| SSH | Secure Shell - used for CLI-level diagnostics |
| Web Browser (HTTPS) | Used to log into CUCM GUI for backup verification 
| Microsoft Excel / Sharepoint| Used to track weekly backup logs for compliance 
| Email / Ticketing Tool (ServiceNow) | For escalating failed backup reports 

## Architecture Diagram 
Link Here 

## Setup Instructions 
| Step | Task | Details |
| --- | --- | ---|
| 1 | Access DRS | Log into CUCM publisher node via https|
| 2 | Verify Backup Status | Go to Backup History Tab and check last backup date and time | 
| 3 | Confirm Backup Completion | Ensure the status is "Successful" for all components |
| 4 | Troubleshoot if Failed | If backup failed, click on the entry / view logs. Note error |
| 5 | Log Results | Record status in internal tracker (Excel / Sharpoint, etc.) |
| 6 | Notify if Issue | If failed, notify the server team and/or escalate to TAC if needed |
| 7 | Record Notes | Add weekly notes
| 8 | Screenshot Proof | Take screenshot of successful backup and store in secure folder |  

## Troubleshooting Notes 
Common Error: "Unable to contact server. Master or local Agent could be down" <br/> 
- Restart services via CLI:
```
utils service restart Cisco DRF Master
utils service restart Cisco DRF Local
```
- Manual Backup Test: Run backup manually to validate service recovery.
- SUB Node Inaccessible: If CLI and HTTPS fail:
    - Contact server team to reboot the SUB node.
    - If VM fails to boot with error:
"unexpected inconsistency; run fsck manually" <br/>
Follow recovery steps:
        - Upload CUCM ISO to vSphere Datastore
        - Mount ISO to CUCM VM
        - Boot into ISO
        - Access Recovery Shell
        - Run fsck
        - Reboot system
        - Validate recovery (SSH, web access, DRS)
- If recovery fails: Restore from DRS backup


## Future Enhancements 
- Automate backup verification alerts via email or dashboard
- Build Power BI dashboard to visualize:
    - Device registration
    - Failover patterns
    - QoS health metrics

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)
