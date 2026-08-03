# Troubleshooting Documentation

## Overview

This document contains troubleshooting scenarios completed during the Helpdesk Lab and real-world technical support situations.

The purpose of this documentation is to demonstrate a structured troubleshooting approach:

- Identifying problems.
- Investigating possible causes.
- Testing solutions.
- Applying fixes.
- Verifying results.
- Documenting resolutions.

---

# Troubleshooting Methodology

The troubleshooting process followed these steps:

1. Identify the issue.
2. Gather information.
3. Analyse possible causes.
4. Test components or settings.
5. Apply the solution.
6. Verify the outcome.
7. Document the resolution.

---

# Case 1: Desktop PC Hardware Failure and Rebuild

## Issue Reported

A desktop PC was experiencing:

- Random shutdowns.
- System instability.
- Failure to display after rebuilding.

The system needed investigation to identify whether the issue was caused by hardware failure or compatibility problems.

---

## Initial Investigation

The PC was inspected to identify possible causes.

Checks completed:

- Inspected internal components.
- Checked motherboard condition.
- Checked CPU installation.
- Reviewed cooling system installation.
- Checked component compatibility.

---

## Finding 1: CPU Socket Damage

During inspection, the motherboard CPU socket was found to have:

- Bent CPU pins.
- Missing CPU pins.
- Signs of previous damage.

The damaged CPU socket was identified as a likely cause of system instability and shutdown issues.

---

## Resolution Step 1: Motherboard Replacement

The original motherboard could not be replaced with the same model because it was unavailable.

Alternative components were researched based on compatibility requirements.

Replacement components selected:

- Compatible ATX motherboard.
- New PC case.
- Compatible desktop RAM.

Compatibility checks included:

- CPU support.
- Motherboard form factor.
- RAM compatibility.
- Graphics card support.

---

## Finding 2: Graphics Card Support Issue

After rebuilding the system, the graphics card weight required additional support.

Resolution:

- Installed a GPU support bracket to reduce stress on the motherboard.

---

## Finding 3: No Display After Rebuild

After powering on the rebuilt PC:

- The system switched on.
- No display output was available.

Further troubleshooting was performed.

Checks completed:

- Reseated components.
- Checked motherboard connections.
- Reviewed installed hardware.
- Tested component compatibility.

---

## Finding 4: Incorrect RAM Installed

The cause of the no-display issue was identified as incorrect RAM.

The system had been supplied with:

- Server RAM.

The motherboard required:

- Standard desktop-compatible RAM.

---

## Final Resolution

Actions completed:

- Replaced incompatible RAM.
- Tested system startup.
- Verified display output.
- Confirmed successful operation.

---

## Outcome

The PC was successfully repaired after identifying multiple hardware faults.

The troubleshooting process demonstrated:

- Fault isolation.
- Component diagnosis.
- Hardware replacement.
- Compatibility checking.
- System testing.

---

# Case 2: Outlook Troubleshooting

## Issue

A user experienced issues accessing Outlook email.

---

## Investigation

Steps completed:

- Confirmed the issue.
- Checked Outlook application status.
- Reset the Outlook profile.
- Restarted Outlook.
- Allowed mailbox synchronisation.

---

## Resolution

The Outlook profile was reset and tested.

---

## Outcome

Outlook access was restored.

---

# Case 3: Active Directory User Account Troubleshooting

## Issue

A user account required creation and configuration within the domain environment.

---

## Investigation

Steps completed:

- Opened Active Directory Users and Computers.
- Created the user account.
- Configured account details.
- Assigned required group membership.

---

## Resolution

The user account was successfully configured.

---

## Outcome

The account was available for use within the Active Directory environment.

---

# Case 4: Group Policy Verification

## Issue

Domain security settings required checking after configuration changes.

---

## Investigation

Steps completed:

- Reviewed Group Policy Management.
- Checked password policy.
- Checked account lockout settings.
- Forced policy refresh.

Command used:

```powershell
gpupdate /force
```

Verification:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

---

## Resolution

Group Policy settings were refreshed and verified.

---

## Outcome

Security policies were successfully applied within the domain.

---

# Case 5: DNS Troubleshooting

## Issue

Domain services required correct DNS resolution.

---

## Investigation

Checks completed:

- Reviewed DNS configuration.
- Checked network settings.
- Tested name resolution.

Commands used:

```cmd
ipconfig /all
```

```cmd
nslookup
```

---

## Resolution

DNS configuration was verified.

---

## Outcome

DNS successfully supported the domain environment.

---

# Case 6: DHCP Troubleshooting

## Issue

Client machines required automatic network configuration.

---

## Investigation

Checks completed:

- Reviewed DHCP scope.
- Checked IP address assignment.
- Verified client configuration.

Commands used:

```cmd
ipconfig /all
```

```cmd
ipconfig /renew
```

---

## Resolution

DHCP configuration was verified and corrected.

---

## Outcome

Client machines successfully received network settings.

---

# Skills Demonstrated

- Hardware troubleshooting.
- PC repair and rebuilding.
- Component compatibility checking.
- Windows troubleshooting.
- Active Directory support.
- DNS and DHCP troubleshooting.
- Group Policy administration.
- PowerShell verification.
- End-user support.
- Technical documentation.
