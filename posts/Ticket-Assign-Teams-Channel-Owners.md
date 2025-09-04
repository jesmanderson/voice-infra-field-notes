# Ticket: Assigning Teams Channel Owners

## Purpose
This ticket addresses a Microsoft Teams channel that currently has **no assigned owners**. Without an owner, critical changes and member management cannot be performed. The goal is to assign one or more appropriate users as channel owners to restore administrative control.



## Issue Summary

- **Channel Name**: `General`
- **Team Name**: `APAC Vessels`
- **Current Owners**: None
- **Impact**: 
  - No one can manage channel settings.
  - Member assignments and permissions cannot be updated.
  - Channel risks becoming unmanaged or misconfigured.



## Resolution Steps

1. **Identify appropriate owner(s)**:
   - Confirm with team lead or department head who should be assigned.
   - Ensure selected user(s) have appropriate permissions and responsibilities.

2. **Assign owner(s) via Teams Admin Center or PowerShell**:
   - **Teams Admin Center**:
     - Navigate to the affected Team.
     - Select the channel.
     - Add owner(s) under “Manage Team” > “Members”.
   - **PowerShell** (if needed):
     ```powershell
     # Connect to Teams
     Connect-MicrosoftTeams

     # Add owner to the team
     Add-TeamUser -GroupId "<TeamID>" -User "<UserEmail>" -Role Owner
     ```

3. **Notify the new owner(s)**:
   - Confirm they have access.
   - Provide guidance if they’re unfamiliar with owner responsibilities.


## Notes

- This change should be documented in the team’s change log or ticketing system.
- If no suitable owner is identified, escalate to department leadership or IT governance.



## Lessons Learned

- Always ensure Teams channels have at least one active owner.
- Consider implementing a periodic audit of Teams ownership to prevent similar issues.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)