# 05 - Group Policy Configuration

## Overview

Group Policy was configured within the Active Directory environment to manage security settings and user policies across the domain.

Group Policy allows administrators to centrally control settings for users and computers within an organisation. It is commonly used by IT administrators to enforce security requirements and standardise configurations.

---

# Objective

The objectives of this task were:

- Access Group Policy Management.
- Review the Default Domain Policy.
- Configure password security settings.
- Configure account lockout settings.
- Apply and verify Group Policy changes.

---

# Environment

## Server

- Windows Server Domain Controller

## Tools Used

- Group Policy Management Console (GPMC)
- Active Directory Domain Services
- PowerShell

---

# Steps Completed

## Step 1: Opening Group Policy Management

The Group Policy Management Console was opened from the Domain Controller.

Process:

1. Logged into the Domain Controller.
2. Opened Server Manager.
3. Selected **Tools**.
4. Opened **Group Policy Management**.

---

## Step 2: Accessing the Default Domain Policy

The Default Domain Policy was accessed to review and configure domain security settings.

Process:

1. Expanded the forest.
2. Expanded the domain.
3. Located **Default Domain Policy**.
4. Right-clicked the policy.
5. Selected **Edit**.

---

## Step 3: Configuring Password Policy

The password policy settings were reviewed and configured.

Location:


Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Password Policy


Settings reviewed:

- Enforce password history.
- Maximum password age.
- Minimum password age.
- Minimum password length.
- Password complexity requirements.

Purpose:

Password policies improve account security by ensuring users follow stronger password requirements.

---

## Step 4: Configuring Account Lockout Policy

Account lockout settings were reviewed to improve protection against repeated failed login attempts.

Location:


Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Account Lockout Policy


Settings reviewed:

- Account lockout threshold.
- Account lockout duration.
- Reset account lockout counter after.

Purpose:

Account lockout policies help prevent unauthorised access attempts by temporarily locking accounts after multiple failed login attempts.

---

## Step 5: Applying Group Policy Changes

After making changes, Group Policy was refreshed to apply the updated settings.

Command used:

```powershell
gpupdate /force

Purpose:

Forces Group Policy updates to apply immediately instead of waiting for the normal refresh cycle.

##Step 6: Verifying Group Policy Settings

PowerShell was used to verify the Active Directory password policy configuration.

Command used:

Get-ADDefaultDomainPasswordPolicy

The command was used to check:

Password complexity status.
Minimum password age.
Maximum password age.
Password history.
Account lockout settings.
Outcome

Group Policy was successfully reviewed, configured, and verified within the Active Directory environment.

The domain now had security controls similar to those used in business environments to manage user authentication and account security.

Screenshots

Evidence to include:

Group Policy Management Console.
Default Domain Policy settings.
Password Policy configuration.
Account Lockout Policy configuration.
PowerShell output showing:
Get-ADDefaultDomainPasswordPolicy
Skills Demonstrated
Group Policy administration.
Active Directory security management.
Password policy configuration.
Account lockout configuration.
PowerShell verification.
Enterprise security practices.
IT documentation.
