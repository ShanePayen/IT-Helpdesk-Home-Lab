# Helpdesk Ticketing Workflow & Troubleshooting Documentation

## Overview
This document contains a log of troubleshooting scenarios completed during the Active Directory Helpdesk Lab. Each case follows a structured IT Service Management (ITSM) approach, documenting the initial issue, the investigation methodology, the root cause, and the final resolution.

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

### Overall Skills Demonstrated
* IT Service Management (ITSM) Helpdesk Troubleshooting
* Active Directory Administration & OU Management
* Group Policy (GPO) Deployment and Troubleshooting
* DNS, DHCP, and TCP/IP Troubleshooting
* Hyper-V Virtual Networking
* User Account & Security Group Management
* NTFS and Share Permissions
* PowerShell Administration
