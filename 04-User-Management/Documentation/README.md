# User Management Documentation

## Overview

This document explains the process of creating and managing user accounts within the Active Directory lab environment.

In a real organisation, IT support teams use Active Directory to create accounts for new employees, manage access permissions, and maintain user security.

---

# Objective

The objectives of this stage were:

- Create user accounts in Active Directory.
- Configure user account information.
- Assign users to security groups.
- Understand basic account management tasks performed by helpdesk teams.

---

# Environment

## Server

- Windows Server Domain Controller

## Tools Used

- Active Directory Users and Computers
- PowerShell

---

# Step 1: Opening Active Directory Users and Computers

## Process Completed

1. Opened Server Manager.
2. Accessed Active Directory Users and Computers.
3. Navigated through the domain structure.
4. Located the appropriate organisational unit (OU).

---

# Step 2: Creating a User Account

## Process Completed

1. Right-clicked the required organisational unit.
2. Selected **New → User**.
3. Entered user information:

- First name
- Last name
- Username
- Account details

4. Created the user account.
5. Set an initial password.
6. Applied account settings.

---

# Step 3: Managing User Properties

## Process Completed

User properties were reviewed and configured.

Settings that can be managed include:

- User information.
- Password settings.
- Account status.
- Group membership.

---

# Step 4: Assigning Security Groups

## Purpose

Security groups allow administrators to control access to resources.

## Process Completed

1. Opened user properties.
2. Selected the **Member Of** tab.
3. Added the user to the required security groups.
4. Verified group membership.

---

# Step 5: Verifying User Account Creation

## Verification Completed

The account was checked to confirm:

- User appeared in Active Directory Users and Computers.
- User properties were correct.
- Group membership was applied.

---

# PowerShell Verification

PowerShell can also be used to check Active Directory users.

Example command:

```powershell
Get-ADUser -Identity username
