# PowerShell Administration Documentation

## Overview

This document explains the PowerShell commands used throughout the Active Directory Helpdesk Lab.

PowerShell was used to verify configurations, retrieve information, and perform administrative checks within the Windows Server environment.

---

# Objective

The objectives of this stage were:

- Understand basic PowerShell administration.
- Verify Windows Server information.
- Check Active Directory configuration.
- Review user and security settings.
- Use commands for troubleshooting and verification.

---

# Environment

## Server

- Windows Server Domain Controller
- Active Directory Domain Environment

## Tool Used

- Windows PowerShell

---

# Step 1: Checking Computer Name

## Purpose

The computer name was checked to identify the server within the environment.

## Command Used

```powershell
hostname
```

## Result

The command displayed the current computer name.

This is useful when identifying devices and servers during troubleshooting.

---

# Step 2: Checking Logged-In User

## Purpose

The current user session was checked to confirm which account was being used.

## Command Used

```powershell
whoami
```

## Result

The command displayed the currently logged-in user account.

This helps administrators verify account access and permissions.

---

# Step 3: Checking Active Directory Domain Information

## Purpose

PowerShell was used to verify Active Directory domain information.

## Command Used

```powershell
Get-ADDomain
```

## Information Checked

The command displays:

- Domain name.
- Domain information.
- Domain configuration details.

## Result

The Active Directory domain configuration was successfully verified.

---

# Step 4: Checking User Information

## Purpose

PowerShell can be used to retrieve information about Active Directory user accounts.

## Command Used

```powershell
Get-ADUser -Identity username
```

## Information Retrieved

- User account details.
- Account status.
- User properties.

## Result

User account information was successfully retrieved.

---

# Step 5: Checking Domain Password Policy

## Purpose

PowerShell was used to verify password and account security settings configured through Group Policy.

## Command Used

```powershell
Get-ADDefaultDomainPasswordPolicy
```

## Information Checked

- Password complexity.
- Minimum password age.
- Maximum password age.
- Password history.
- Account lockout settings.

## Result

The domain password policy settings were displayed successfully.

---

# Step 6: Applying Group Policy Updates

## Purpose

After changing Group Policy settings, the policy was refreshed to apply updates immediately.

## Command Used

```powershell
gpupdate /force
```

## Result

Group Policy updates were successfully applied.

---

# Troubleshooting Uses

PowerShell can assist with common helpdesk tasks such as:

- Checking user accounts.
- Verifying permissions.
- Confirming system information.
- Reviewing domain settings.
- Troubleshooting configuration issues.

---

# Outcome

PowerShell was successfully used to manage and verify the Active Directory lab environment.

The commands demonstrated how administrators can quickly collect information and troubleshoot Windows environments.

---

# Screenshots

Evidence to include:

- PowerShell window showing commands.
- `hostname` output.
- `whoami` output.
- `Get-ADDomain` output.
- `Get-ADDefaultDomainPasswordPolicy` output.

---

# Skills Demonstrated

- PowerShell administration.
- Active Directory management.
- System troubleshooting.
- Command-line tools.
- Windows Server administration.
- IT documentation.
