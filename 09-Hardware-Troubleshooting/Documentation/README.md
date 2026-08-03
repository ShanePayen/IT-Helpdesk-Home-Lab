# IT Helpdesk Ticketing Workflow & Troubleshooting Documentation

## Overview
This document details real-world troubleshooting scenarios completed during the Helpdesk Lab and technical support environments. Each case demonstrates systematic problem-solving methodology—moving from initial issue identification through root cause investigation, resolution, and verification. 

It is designed to simulate a real-world enterprise environment for Tier 1 and Tier 2 Helpdesk scenarios.

---

## Standard Troubleshooting Methodology

All technical support issues documented here followed a structured 7-step ITSM (IT Service Management) workflow:

1. **Identify the Issue:** Capture initial symptom reports and user impact.
2. **Gather Information:** Interview user, review log files, and observe system behavior.
3. **Analyze Root Causes:** Formulate hypotheses and isolate variables.
4. **Test Solutions:** Apply minimal-impact tests in a controlled manner.
5. **Implement Fix:** Execute the permanent fix or system replacement.
6. **Verify System Functionality:** Perform full end-to-end testing with the user/system.
7. **Document Resolution:** Record steps taken and update technical knowledge bases.

---

### Ticket #001: Remote Desktop Access Issue (CLIENT01)
**Status:** Resolved | **Priority:** Medium | **Category:** Active Directory / Network

**Issue Description:**
A domain user attempting to connect remotely to CLIENT01 received the error: "The requested session access is denied." The same account successfully connected to CLIENT02, confirming the issue was isolated to CLIENT01.

**Troubleshooting Steps Taken:**
* Ran `gpresult /r` to check Group Policy results and found CLIENT01 was missing the required policy settings.
* Checked the Remote Desktop Users group via the command `net localgroup "Remote Desktop Users"`.
* Identified that CLIENT02 had the expected groups (HR_Users, IT_Users, Managers) applied, while CLIENT01 was missing them.
* Discovered CLIENT01 was located in the incorrect Active Directory Organizational Unit (OU), preventing the necessary Group Policy Objects (GPOs) from applying.

**Resolution:**
Applied a temporary fix by manually adding `LAB\Domain Users` to the Remote Desktop Users permissions to restore immediate access. The permanent fix was completed by moving the CLIENT01 computer account into the correct OU in Active Directory, allowing the GPO to apply automatically. 

---

### Ticket #002: DHCP Address Assignment Failure (CLIENT01)
**Status:** Resolved | **Priority:** High | **Category:** Network / Hyper-V

**Issue Description:**
CLIENT01 failed to obtain an IP address automatically from the DHCP server and was assigned an APIPA address (`169.254.x.x`). 

**Troubleshooting Steps Taken:**
* Ran `ipconfig /all` to verify the current network configuration on the client.
* Attempted to test network communication by running `ping 192.168.1.10` (Domain Controller), which failed.
* Reviewed the Hyper-V network adapter settings for both virtual machines.
* Identified that CLIENT01 and DC01 were connected to completely different Hyper-V virtual switches, blocking DHCP broadcasts and DNS/Domain communication.

**Resolution:**
Reconfigured the Hyper-V network adapter for CLIENT01 to use the same Internal Hyper-V Switch as DC01. Upon reconnecting, CLIENT01 successfully received IP address `192.168.1.101` from the DHCP server and DNS communication was restored.

---

### Ticket #003: Group Policy Not Applying
**Status:** Resolved | **Priority:** Medium | **Category:** Active Directory

**Issue Description:**
A newly created Group Policy on the Domain Controller was successfully applying to CLIENT02 but was failing to apply to CLIENT01.

**Troubleshooting Steps Taken:**
* Ran `gpresult /r` on both client machines to compare the applied policies.
* Verified that the GPO was active and linked on the domain controller.
* Reviewed the computer account locations within Active Directory Users and Computers (ADUC).
* Discovered CLIENT01 was placed in the wrong OU where the policy was not linked.

**Resolution:**
Moved the CLIENT01 computer object into the correct Organizational Unit. After forcing a policy update, CLIENT01 successfully received the targeted Group Policy settings.

---

### Ticket #004: User Missing Network Drive
**Status:** Resolved | **Priority:** Medium | **Category:** Active Directory / File Share

**Issue Description:**
A user in the Finance department logged into their workstation, but their expected Finance network drive did not map automatically.

**Troubleshooting Steps Taken:**
* Checked the user's account properties and security group memberships in AD.
* Ran `gpresult /r` on the user's machine to verify if the drive-mapping Group Policy was attempting to apply.
* Identified that the user was missing from the required security group that grants access to the drive.

**Resolution:**
Added the user's account to the `GG_Finance` Active Directory security group. Instructed the user to log off and log back in to refresh Group Policy, which successfully mapped the Finance drive.

---

### Ticket #005: User Account Locked
**Status:** Resolved | **Priority:** High | **Category:** Active Directory

**Issue Description:**
A user reported they were completely unable to sign into their domain-joined workstation, receiving an error that their account was locked.

**Troubleshooting Steps Taken:**
* Verified the exact spelling of the username.
* Checked the user's account status within Active Directory Users and Computers.
* Verified the user had exceeded the maximum allowed failed login attempts defined by the domain password policy.

**Resolution:**
Unlocked the user account within the Account tab in Active Directory. The user was then able to successfully authenticate and log into their workstation.

---

### Ticket #006: Incorrect User Permissions
**Status:** Resolved | **Priority:** High | **Category:** Security / File Share

**Issue Description:**
It was discovered that a user had access to internal network resources and folders that they were not authorized to view.

**Troubleshooting Steps Taken:**
* Ran `whoami /groups` on the user's machine to verify their current group memberships and access tokens.
* Checked the Share permissions and NTFS permissions on the folder in question.
* Discovered that permissions had been assigned directly to individual user accounts rather than through role-based security groups.

**Resolution:**
Stripped the direct user assignments from the folder. Implemented Microsoft's best practice permissions model (Users → Security Groups → Resources) by creating appropriate security groups, assigning the correct NTFS permissions to the groups, and placing authorized users into those groups.

---

### Ticket #007: PowerShell Administration Syntax Issues
**Status:** Resolved | **Priority:** Low | **Category:** Software / Administration

**Issue Description:**
Administrative PowerShell scripts designed to create users, test password policies, and search groups were failing to execute or returning errors.

**Troubleshooting Steps Taken:**
* Verified that the necessary Active Directory PowerShell modules were loaded into the session.
* Checked the syntax of the group names and user objects being queried.
* Identified typographical errors in the command syntax and scripts attempting to modify objects that had not yet been verified to exist.

**Resolution:**
Corrected the syntax of the PowerShell commands. Added verification steps to ensure objects (like groups or users) actually existed in Active Directory before the script attempted to apply changes to them.

---

### Ticket #008: Desktop Hardware Repair & Rebuild
**Status:** Resolved | **Priority:** High | **Category:** Hardware Diagnostic

**Issue Description:**
A desktop workstation experienced severe instability, unexpected shutdowns, and eventually a total loss of display output (No POST / No Display) following a hardware rebuild.

**Troubleshooting Steps Taken:**
* Disassembled system and performed a visual inspection of all core hardware components.
* Inspected the CPU socket on the motherboard under magnifying lighting.
* Identified bent and missing pins on the LGA motherboard socket, causing physical connection failures to the CPU.
* Audited installed memory and discovered incompatible registered server RAM (ECC/RDIMM) had been installed instead of standard non-ECC desktop DDR memory.

**Resolution:**
* Replaced damaged motherboard with a compatible ATX desktop motherboard.
* Transferred components into a new PC chassis with proper standoff alignment.
* Swapped out incompatible server RAM for certified desktop memory modules.
* Installed an anti-sag GPU support bracket to prevent PCIe slot strain caused by GPU weight.
* Conducted stress testing and verified POST, BIOS configuration, and OS stability.

---

### Ticket #009: Microsoft Outlook Profile & Synchronization Failure
**Status:** Resolved | **Priority:** Medium | **Category:** Microsoft 365 / Client Apps

**Issue Description:**
A user experienced complete email access failure, frozen sync status, and application crashes when launching Microsoft Outlook.

**Troubleshooting Steps Taken:**
* Interviewed the user to determine recent software updates or password changes.
* Terminated hung Outlook processes via Task Manager and attempted launching in Safe Mode (`outlook.exe /safe`).
* Determined the local OST cache file / Outlook profile was corrupted.

**Resolution:**
* Navigated to Control Panel > Mail > Show Profiles.
* Created a fresh Outlook profile linked to the user's Microsoft 365 account and removed the corrupt profile.
* Launched Outlook, allowing a clean resynchronization of the mailbox from Exchange Online.
* Verified send/receive capabilities and cached folder updating.

---

### Ticket #010: Active Directory User Provisioning & Group Assignment
**Status:** Resolved | **Priority:** Low | **Category:** Active Directory / Identity

**Issue Description:**
A new employee required provisioning in Active Directory with specific organizational rights, network share access, and password parameters.

**Troubleshooting Steps Taken:**
* Reviewed onboarding ticket parameters for department placement and group requirements.
* Opened Active Directory Users and Computers (ADUC) on the Domain Controller.
* Created user object within the designated Organizational Unit (OU) using standard naming conventions.

**Resolution:**
Configured account parameters (enabling "User must change password at next logon") and added the account to relevant Global Security Groups to grant role-based resource permissions. Verified login capability on a test domain client machine and confirmed correct token assignment.

---

### Ticket #011: Group Policy Refresh & Domain Security Verification
**Status:** Resolved | **Priority:** Medium | **Category:** Group Policy / Security

**Issue Description:**
Updated domain-wide password complexity and account lockout policies were required to be pushed immediately and verified across member workstations.

**Troubleshooting Steps Taken:**
* Configured updated baseline rules within Group Policy Management Console (GPMC) under Default Domain Policy.
* Forced immediate policy propagation across local and network targets via PowerShell using `gpupdate /force`.
* Verified effective default password policy applied across Active Directory using PowerShell: `Get-ADDefaultDomainPasswordPolicy`.

**Resolution:**
Policy update succeeded. Confirmed that lockout thresholds and password complexity rules were properly enforced domain-wide.

---

### Ticket #012: DNS Resolution Failure Troubleshooting
**Status:** Resolved | **Priority:** High | **Category:** Network / DNS

**Issue Description:**
Domain client workstations were unable to reach internal network resources or resolve Domain Controller names, resulting in domain authentication failures.

**Troubleshooting Steps Taken:**
* Audited local IP configuration using Command Prompt: `ipconfig /all`.
* Discovered local network adapter had an invalid or public DNS server IP assigned instead of the internal Domain Controller DNS IP.
* Executed DNS lookup queries to diagnose resolution paths: `nslookup dc01.lab.local`.

**Resolution:**
* Reconfigured static/DHCP network adapter properties to direct primary DNS queries to the Domain Controller IP (`192.168.1.10`).
* Flushed local DNS cache using `ipconfig /flushdns`.
* Confirmed successful host resolution and restored internal resource accessibility.

---

### Ticket #013: DHCP Lease Allocation & Scope Troubleshooting
**Status:** Resolved | **Priority:** High | **Category:** Network / DHCP

**Issue Description:**
Newly connected client workstations were unable to join the network automatically, reverting to APIPA addresses (`169.254.x.x`).

**Troubleshooting Steps Taken:**
* Verified client IP binding with: `ipconfig /all`.
* Checked DHCP Server Manager console on Windows Server to audit scope status, active leases, and address pool availability.
* Verified network switch bindings to ensure DHCP broadcast traffic was reaching the server.

**Resolution:**
* Resolved DHCP binding issue on the server adapter and expanded the active address pool.
* Forced client machines to release bad leases and request fresh IP configurations using `ipconfig /release` and `ipconfig /renew`.

---

## Summary of Core Skills Demonstrated

* **Service Management:** Structured ITSM methodology, technical documentation, root-cause analysis, and ticketing workflows.
* **Hardware & Systems:** Component diagnostics, LGA socket inspection, RAM compatibility auditing, chassis rebuilding.
* **Identity & Access Management:** Active Directory provisioning, Security Groups, Organizational Units, Password Policies, role-based access control (RBAC).
* **Network Infrastructure:** Hyper-V Virtual Networking, DNS resolution (`nslookup`), DHCP scopes & APIPA recovery, TCP/IP troubleshooting.
* **System Administration:** Group Policy Management, NTFS and Share Permissions, PowerShell scripting, M365 client support.

---

## Evidence
*(Screenshots representing hardware rebuilds, AD configurations, Group Policy enforcement, PowerShell executions, and networking configuration are stored natively within the respective repository folders.)*
