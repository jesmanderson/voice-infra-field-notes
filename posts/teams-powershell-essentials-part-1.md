# 🧰 Teams PowerShell Essentials for UC Engineers

As Microsoft Teams becomes the backbone of modern UC environments, learning PowerShell isn't just optional, it's essential. Here's a quick-start guide with practical examples I use in the field to support Teams Voice, automate admin tasks, and speed up troubleshooting.

---

## 💻 Getting Started with Teams PowerShell

### ✅ Step 1: Install the Module
```powershell
Install-Module -Name PowerShellGet -Force -AllowClobber
Install-Module -Name MicrosoftTeams -Force
```

### ✅ Step 2: Connect to Teams
```powershell
Connect-MicrosoftTeams
```
You'll be prompted for your admin credentials.

---

## 🧠 PowerShell Concepts UC Engineers Need
- **Cmdlets**: Think of them as one-liner commands like `Get-TeamsUser`
- **Pipelines**: Chain commands with `|` to filter, sort, or export
- **Scripting**: Automate repeated tasks (like phone number assignments)

---

## 🔧 Everyday Cmdlets I Use

### 📞 User & Phone Number Management
```powershell
# View all Teams users
Get-CsOnlineUser

# Filter users with a phone number
Get-CsPhoneNumberAssignment -PstnAssignmentType User

# Assign phone number to a user
Set-CsPhoneNumberAssignment -Identity user@domain.com -PhoneNumber "+15551234567" -PhoneNumberType DirectRouting
```

### 🏢 Calling Policy & Voice Config
```powershell
# List all calling policies
Get-CsCallingPolicy

# Assign policy to a user
Grant-CsCallingPolicy -Identity user@domain.com -PolicyName "AllowCalling"

# List voice routing policies
Get-CsOnlineVoiceRoutingPolicy
```

### 🧪 Troubleshooting
```powershell
# Check if a user has a valid license
Get-MsolUser -UserPrincipalName user@domain.com | Select DisplayName, Licenses

# Check Teams tenant info
Get-CsTenant

# Check dial plans
Get-CsOnlineDialPlan
```

---

## 📁 Bonus: Export Reports
```powershell
Get-CsOnlineUser | Select DisplayName, UserPrincipalName, LineUri | Export-Csv teams_users.csv -NoTypeInformation
```

---

## 🧠 Real-World Tips
- Keep a script library with frequently used cmdlets
- Use comments to explain each line (makes team sharing easier)
- Combine with scheduled tasks or GitHub Actions for automation


