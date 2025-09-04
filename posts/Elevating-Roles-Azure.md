# UC Engineer Guide: Elevating Roles in Microsoft Entra for Admin Tasks 

## Purpose 
As a Unified Communications (UC) Engineer, you’ll frequently need elevated permissions in Microsoft Entra to perform administrative tasks across Microsoft Teams, Exchange, Licensing, and User Management. This guide outlines the process for elevating roles securely and efficiently using your assigned aliases. 

## Your Aliases
You will typically operate under three aliases:
- Regular alias – Default user account for daily tasks.
- AZR alias – Used for Azure-related tasks and elevated role assignments.
- OU alias – Used for organizational unit-specific tasks or legacy systems.

## Roles You Need to Elevate To 
To perform PowerShell and admin tasks, you’ll need to elevate to the following roles:
| Role Name |	Purpose |
| :-------  | :------ |
| Teams Admin |	Manage Teams policies, configurations, and troubleshooting. |
| License Admin	| Assign and manage user licenses.|
| Exchange Admin |	Manage mailboxes, connectors, and mail flow.|
| User Admin |	Create, modify, and manage user accounts and groups.|

## Elevation Process in Microsoft Entra
### Step 1: Sign in to Microsoft Entra Admin Center
- Go to https://entra.microsoft.com    
- Sign in using your AZR alias.
### Step 2: Navigate to PIM (Privileged Identity Management)
- In the left-hand menu, select "Privileged Identity Management".
- Click on "My roles".
### Step 3: Activate Required Roles
- Locate the roles listed above.
- Click "Activate" next to each role.
- Provide justification (e.g., “UC admin tasks”).
- Set the duration (typically 1–8 hours depending on policy).
- Click "Activate".

*Note: You may be prompted for MFA (Multi-Factor Authentication). Ensure your device is registered.*

## PowerShell Access
Once roles are elevated, you can use PowerShell to perform tasks. Use Windows PowerShell ISE or VS Code with the following modules:
### Modules to Install
```
Install-Module -Name MicrosoftTeams
Install-Module -Name ExchangeOnlineManagement
Install-Module -Name AzureAD
```  
### Connect to Services
```
# Connect to Teams
Connect-MicrosoftTeams

# Connect to Exchange
Connect-ExchangeOnline -UserPrincipalName yourAZRalias@domain.com

# Connect to Azure AD
Connect-AzureAD
```

## Best Practices
- Always use your AZR alias for elevation and PowerShell tasks.
- Log out of elevated sessions when tasks are complete.
- Document changes in your team’s change log or ticketing system.
- Avoid using elevated roles for non-admin tasks.

## Troubleshooting
- If you don’t see the roles in PIM, contact your security team to verify role assignment.
- If elevation fails, check for pending MFA or expired role eligibility.
- For PowerShell issues, ensure modules are up-to-date and your session is elevated.

## License
MIT License

## Contact
[LinkedIn](https://www.linkedin.com/in/jessica-anderson-84b423211/)