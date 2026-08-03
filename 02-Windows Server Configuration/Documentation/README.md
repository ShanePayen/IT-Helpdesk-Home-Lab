# Windows Server Configuration Documentation

## Overview

This document explains the configuration checks performed after installing Windows Server in the Hyper-V lab environment.

Before deploying Active Directory Domain Services, the server needed to be verified and prepared for use as part of the network environment.

---

## Objective

The objectives of this stage were:

- Verify Windows Server was installed correctly.
- Confirm server information.
- Check the current user account.
- Prepare the server for Active Directory installation.

---

## Environment

### Server

- Windows Server Virtual Machine
- Hosted using Microsoft Hyper-V

### Planned Role

The server would later be configured as:

- Domain Controller
- Active Directory server
- User and policy management server

---

# Step 1: Accessing Windows Server

## Process Completed

After the Windows Server installation was completed:

- Logged into the server.
- Reviewed the Windows Server desktop.
- Confirmed the operating system was working correctly.

---

# Step 2: Verifying Server Name

## Purpose

The server name was checked to identify the machine before further configuration.

A clear naming convention helps administrators identify systems within a network.

## PowerShell Command Used

```powershell
hostname
```

## Outcome

The server hostname was displayed and verified.

---

# Step 3: Verifying Logged-In User

## Purpose

The current user session was checked to confirm which account was being used for administration.

## PowerShell Command Used

```powershell
whoami
```

## Outcome

The current logged-in user was displayed successfully.

---

# Step 4: Reviewing Server Manager

## Process Completed

Server Manager was opened to confirm the server was ready for role installation.

Checked:

- Server status.
- Available roles and features.
- Server management options.

---

# Step 5: Preparing for Active Directory

The server was prepared for the next stage of the project:

- Active Directory Domain Services installation.
- Domain Controller promotion.
- Domain creation.
- User management.

---

# Outcome

The Windows Server virtual machine was successfully verified and prepared for Active Directory deployment.

---

# Screenshots

Evidence to include:

- Windows Server desktop.
- Server Manager.
- PowerShell output:
  - `hostname`
  - `whoami`

---

# Skills Demonstrated

- Windows Server administration.
- Basic PowerShell usage.
- System verification.
- Server preparation.
- IT documentation.

---

# Next Steps

The next stage was installing and configuring:

- Active Directory Domain Services.
- Domain Controller.
- Domain environment.
