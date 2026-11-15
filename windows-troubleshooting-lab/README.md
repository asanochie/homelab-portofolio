# Windows Troubleshooting Lab

## Overview

This project was created to develop practical IT Service Desk and Help Desk troubleshooting skills within a Windows domain environment.

Using a Windows Server 2022 Domain Controller and a Windows 11 Enterprise client, I created and resolved a range of common support incidents involving Active Directory, DNS, DHCP and SMB file shares.

The objective was to practise structured troubleshooting by gathering information, forming hypotheses, identifying root causes and verifying resolutions.

---

## Environment

| Component | Details |
|------------|------------|
| Hypervisor | VMware Workstation |
| Domain Controller | Windows Server 2022 |
| Client Device | Windows 11 Enterprise |
| Domain | techcorp.local |
| Services | Active Directory, DNS, DHCP, SMB Shares |
| Administration Tools | PowerShell, Active Directory Users and Computers, DNS Manager, DHCP Manager |

---

## Troubleshooting Methodology

The following process was used for every incident:

1. Gather information
2. Identify symptoms
3. Form a hypothesis
4. Investigate the issue
5. Identify the root cause
6. Implement a resolution
7. Verify the fix
8. Document lessons learned

---

## Ticket Categories Completed

### Active Directory

- Disabled user account
- Incorrect security group assignment

### DNS

- Missing DNS record
- Incorrect DNS record

### DHCP

- Inactive DHCP scope

### SMB Share Permissions

- Share permission removed
- Explicit deny permission applied

---

## Example Investigations

### Ticket 001 - Disabled Account

A user reported that they were unable to sign in to their workstation.

#### Investigation

- Attempted to sign in using the affected account.
- Received an "Account Disabled" message.
- Queried the user account within Active Directory.

#### Root Cause

The account had been disabled in Active Directory.

#### Resolution

The account was re-enabled using:

```powershell
Enable-ADAccount -Identity "sjohnson"
```

#### Evidence

![Disabled Account](/screenshots/ad-disabled-account.png)

---

### Ticket 002 - Missing DNS Record

A user reported that a shared resource could not be located.

#### Investigation

- Verified connectivity to the domain controller.
- Performed DNS lookups against domain resources.
- Determined that fileserver could not be resolved.

#### Root Cause

The DNS A record for fileserver had been removed.

#### Resolution

Recreated the fileserver DNS A record.

#### Evidence

![Missing DNS Record](/screenshots/dns-record-missing.png)

---

### Ticket 003 - Incorrect DNS Record

A user reported they were unable to access a shared resource.

#### Investigation

- Verified name resolution.
- Determined fileserver resolved to an incorrect IP address.
- Reviewed DNS zone records.

#### Root Cause

The DNS A record existed but pointed to the wrong IP address.

#### Resolution

Removed the incorrect record and recreated it with the correct IP address.

#### Evidence

![DNS Record Repair](/screenshots/dns-record-repair.png)

---

### Ticket 004 - Incorrect Group Membership

A user reported they were unable to access departmental resources.

#### Investigation

- Verified successful user authentication.
- Confirmed access to other company resources.
- Reviewed Active Directory group membership.

#### Root Cause

The user belonged to `Finance_Users` instead of `HR_Users`.

#### Resolution

Removed the user from `Finance_Users` and added them to `HR_Users`.

#### Evidence

![Incorrect Group Membership](/screenshots/group-membership-incorrect.png)

---

### Ticket 005 - Share Permission Removed

A user received an "Access Denied" message when accessing the HR share.

#### Investigation

- Confirmed the user belonged to the correct security group.
- Reviewed SMB share permissions.
- Identified missing permissions for `HR_Users`.

#### Root Cause

The SMB share permissions for `HR_Users` had been removed.

#### Resolution

Restored Change permissions for `HR_Users`.

#### Evidence

![Share Permission Removed](/screenshots/share-permission-removed.png)

---

### Ticket 006 - Explicit Deny Permission

A user was unable to access the HR share despite belonging to the correct security group.

#### Investigation

- Verified group membership.
- Reviewed SMB share permissions.
- Identified an explicit Deny permission on the Everyone group.

#### Root Cause

An explicit Deny permission was overriding the Allow permissions assigned to HR_Users.

#### Resolution

Removed the Deny permission.

#### Evidence

![SMB Deny Permission](/screenshots/smb-deny-permission-removal.png)

---

### Ticket 007 - DHCP Scope Disabled

A workstation was unable to obtain a valid IP address automatically.

#### Investigation

- Attempted to renew the DHCP lease.
- Reviewed DHCP scope configuration.

#### Root Cause

The DHCP scope had been deactivated.

#### Resolution

Reactivated the DHCP scope.

#### Evidence

![DHCP Scope Disabled](/screenshots/dhcp-scope-inactive.png)

---

## Skills Demonstrated

- Active Directory Administration
- User and Group Management
- DNS Troubleshooting
- DHCP Troubleshooting
- SMB Share Administration
- Root w permissions.
- Group membership changes may require users to sign out and sign back in before permissions are refreshed.
- DNS issues are not always caused by missing records; incorrect records can be equally disruptive.
- Systematic troubleshooting is more effective than immediately applying fixes.
- Verifying the success of a remediation step is just as important as identifying the root cause.

---

## Reflection

This project helped me develop a structured troubleshooting methodology similar to those used in Service Desk and Help Desk environments.

By investigating and resolving issues across Active Directory, DNS, DHCP and SMB shares, I gained hands-on experience diagnosing user account, permissions and networking problems while documenting findings and validating resolutions.
