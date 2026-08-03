# Helpdesk Troubleshooting Documentation

## Overview

This document contains troubleshooting scenarios completed during the Active Directory Helpdesk Lab and technical support practice.

Each case follows a structured troubleshooting approach:

- Issue identification
- Investigation
- Root cause analysis
- Resolution
- Outcome
- Skills demonstrated

---

# Ticket 001 - Remote Desktop Access Issue (CLIENT01)

## Issue

A domain user attempting to connect remotely to CLIENT01 received:

"The requested session access is denied."

The same account successfully connected to CLIENT02, confirming the issue was isolated to CLIENT01.

## Investigation

Checked Group Policy results:

```powershell
gpresult /r
```

Findings:

- CLIENT02 received the expected Remote Desktop policies.
- CLIENT01 was missing the required policy settings.

Checked Remote Desktop Users group:

```cmd
net localgroup "Remote Desktop Users"
```

Findings:

CLIENT02:
- HR_Users
- IT_Users
- Managers

CLIENT01:
- Missing expected Group Policy permissions.

## Root Cause

CLIENT01 was located in the incorrect Active Directory Organizational Unit (OU).

Because the computer account was outside the correct OU:

- Required Group Policy Objects were not applied.
- Remote Desktop permissions were not configured automatically.

## Resolution

Temporary fix:

Added:

```
LAB\Domain Users
```

to the Remote Desktop Users permissions.

Permanent fix:

Move CLIENT01 into the correct OU so Group Policy applies automatically.

## Result

Remote Desktop access was restored.

## Skills Demonstrated

- Active Directory
- Group Policy
- Remote Desktop troubleshooting
- OU management

---

# Ticket 002 - DHCP Address Assignment Failure (CLIENT01)

## Issue

CLIENT01 failed to obtain an IP address automatically.

The device received:

```
169.254.x.x
```

## Investigation

Checked:

```cmd
ipconfig /all
```

Tested communication:

```cmd
ping 192.168.1.10
```

Reviewed Hyper-V network adapter settings.

## Root Cause

CLIENT01 and DC01 were connected to different Hyper-V virtual switches.

This prevented:

- DHCP broadcasts reaching the server.
- DNS communication.
- Domain communication.

## Resolution

Moved CLIENT01 onto the same Internal Hyper-V Switch as DC01.

## Result

CLIENT01 received:

IP Address:
```
192.168.1.101
```

DHCP Server:
```
192.168.1.10
```

DNS Server:
```
192.168.1.10
```

## Skills Demonstrated

- Hyper-V networking
- DHCP troubleshooting
- TCP/IP troubleshooting
- Windows Server administration

---

# Ticket 003 - Group Policy Not Applying

## Issue

A Group Policy created on the Domain Controller was not applying to CLIENT01.

## Investigation

Compared:

```powershell
gpresult /r
```

Findings:

- CLIENT02 received the policy.
- CLIENT01 did not.

## Root Cause

CLIENT01 was placed in the wrong OU.

## Resolution

Reviewed the computer account location in Active Directory Users and Computers.

Moved the device into the correct OU.

## Result

CLIENT01 successfully received Group Policy settings.

## Skills Demonstrated

- Active Directory
- Group Policy
- Computer account management

---

# Ticket 004 - User Missing Network Drive

## Issue

A Finance user logged in but the Finance network drive was missing.

## Investigation

Checked:

- User account.
- Security group membership.
- Group Policy application.

Command:

```powershell
gpresult /r
```

## Resolution

Added the user to:

```
GG_Finance
```

Refreshed Group Policy.

## Result

The Finance drive became available.

## Skills Demonstrated

- Active Directory groups
- Group Policy
- File access troubleshooting

---

# Ticket 005 - User Account Locked

## Issue

User unable to sign into domain workstation.

## Investigation

Checked:

- Username.
- Account status.
- Failed login attempts.

## Resolution

Unlocked the account in Active Directory.

## Result

User successfully logged back in.

## Skills Demonstrated

- Account administration
- Active Directory support
- User troubleshooting

---

# Ticket 006 - Incorrect User Permissions

## Issue

A user had access to resources they should not have.

## Investigation

Checked:

- Active Directory groups.
- NTFS permissions.
- Share permissions.

Command:

```cmd
whoami /groups
```

## Root Cause

Permissions were assigned directly to users instead of security groups.

## Resolution

Changed permissions model:

Users → Security Groups → Resources

## Result

Correct access control was restored.

## Skills Demonstrated

- NTFS permissions
- Security groups
- Access control

---

# Ticket 007 - PowerShell Administration Issues

## Issue

PowerShell commands were used for Active Directory administration.

Examples:

- Creating users.
- Testing password policies.
- Searching groups.

## Investigation

Verified:

- Active Directory modules.
- Group names.
- User objects.

## Resolution

Corrected command syntax and verified objects existed before applying changes.

## Skills Demonstrated

- PowerShell
- Active Directory administration
- Automation concepts

---

# Overall Skills Demonstrated

- Helpdesk troubleshooting
- Active Directory administration
- Group Policy troubleshooting
- DNS and DHCP troubleshooting
- Hyper-V networking
- User account management
- PowerShell administration
- Technical documentation
