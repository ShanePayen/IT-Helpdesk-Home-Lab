# Windows Server Configuration

## Overview

This section covers the initial configuration and preparation of the Windows Server virtual machine within the Hyper-V lab environment.

The server was verified, configured with essential network services, and prepared for Active Directory deployment.

---

## Completed Tasks

- Verified Windows Server installation.
- Checked server information.
- Verified administrator access.
- Configured DNS Server role.
- Configured DHCP Server role.
- Prepared the server for Active Directory Domain Services.

---

## Server Roles Configured

### DNS Server

DNS was configured to provide name resolution within the network environment.

Purpose:

- Allow devices to locate network services.
- Support Active Directory communication.
- Resolve domain resources.

---

### DHCP Server

DHCP was configured to automatically provide network settings to client machines.

Purpose:

- Assign IP addresses automatically.
- Provide DNS server information.
- Simplify network management.

---

## Tools Used

- Microsoft Hyper-V
- Windows Server
- Server Manager
- DNS Manager
- DHCP Manager
- PowerShell
- Command Prompt

---

## Verification Commands Used

Check computer name:

```powershell
hostname
```

Check logged-in user:

```powershell
whoami
```

Check network and DNS information:

```cmd
ipconfig /all
```

Test DNS resolution:

```cmd
nslookup
```

Renew DHCP address:

```cmd
ipconfig /renew
```

---

## Skills Demonstrated

- Windows Server administration.
- DNS configuration.
- DHCP configuration.
- Network services management.
- Server preparation.
- Basic PowerShell troubleshooting.
- IT documentation.

---

## Documentation

Detailed configuration steps can be found here:

[Windows Server Configuration Documentation](Documentation/README.md)
