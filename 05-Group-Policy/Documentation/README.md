# Group Policy Configuration Documentation

## Overview

This document explains the configuration and verification of Group Policy settings within the Active Directory lab environment.

Group Policy is used by organisations to centrally manage security settings and user configurations across domain-connected computers.

---

# Objective

The objectives of this stage were:

- Access Group Policy Management.
- Configure domain security settings.
- Apply password requirements.
- Configure account lockout settings.
- Verify the applied policies.

---

# Environment

## Server

- Windows Server Domain Controller

## Tools Used

- Group Policy Management Console
- Active Directory Users and Computers
- PowerShell

---

# Step 1: Opening Group Policy Management

## Process Completed

1. Logged into the Domain Controller.
2. Opened Server Manager.
3. Accessed Group Policy Management.
4. Located the domain policies.

---

# Step 2: Reviewing Default Domain Policy

## Purpose

The Default Domain Policy controls important security settings that apply across the domain.

Settings reviewed included:

- Password requirements.
- Account lockout policies.
- User authentication settings.

---

# Step 3: Configuring Password Policy

## Process Completed

Password policy settings were reviewed and configured.

Settings include:

- Password complexity requirements.
- Minimum password length.
- Password history requirements.
- Password expiration settings.

These settings help improve account security.

---

# Step 4: Configuring Account Lockout Policy

## Purpose

Account lockout policies help protect accounts from repeated failed login attempts.

Settings configured include:

- Lockout threshold.
- Lockout duration.
- Reset account lockout counter.

---

# Step 5: Updating Group Policy

After making policy changes, Group Policy can be refreshed using:

```powershell
gpupdate /force

Purpose

This command forces client computers to immediately apply updated Group Policy settings.

# Step 6: Verifying Password Policy

PowerShell was used to confirm the domain password policy.

Command Used
Get-ADDefaultDomainPasswordPolicy
Information Verified

The command displays:

Password complexity status.
Minimum password age.
Maximum password age.
Password history requirements.
Account lockout settings.
Outcome

Group Policy settings were successfully configured and verified.

The domain environment was prepared with basic security controls similar to those used in business environments.

Screenshots

Evidence to include:

Group Policy Management Console.
Password policy settings.
Account lockout settings.
PowerShell output from:
Get-ADDefaultDomainPasswordPolicy
Skills Demonstrated
Group Policy management.
Active Directory security.
Password policy configuration.
PowerShell verification.
Domain administration.
Security best practices.
