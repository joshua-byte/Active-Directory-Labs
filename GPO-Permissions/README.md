# Active Directory GPO Security Lab

## Overview

A hands-on Active Directory security lab built using VirtualBox, Windows Server 2022, Windows 10, and Kali Linux.

The project demonstrates how excessive Group Policy Object (GPO) permissions can create security risks, how to validate permissions from Kali Linux, and how to remediate and retest a misconfiguration.

## Lab Environment

- **Domain Controller:** Windows Server 2022
- **Workstation:** Windows 10
- **Testing Machine:** Kali Linux
- **Virtualization:** Oracle VirtualBox
- **Domain:** `adlab.test`

## Objectives

- Configure an Active Directory test environment.
- Identify GPO permissions and group memberships.
- Validate GPO and SYSVOL access from Kali Linux.
- Demonstrate a controlled GPO permissions misconfiguration.
- Remediate excessive permissions and repeat the test.

## Test Scenario

A dedicated GPO, `LAB-GPO-Permissions-Test`, was used to test the permissions assigned to the `GPO-Editors` security group.

Alice was a member of this group.

Before remediation, Alice could upload a harmless temporary file to the test GPO's SYSVOL directory. After the group's GPO permission was removed, the repeated upload attempt returned:

`NT_STATUS_ACCESS_DENIED`

A benign registry preference was also used to verify that the test GPO applied to the Windows 10 workstation.

## Tools Used

- `ldapsearch` — LDAP enumeration
- `smbclient` — SYSVOL access validation
- `samba-tool` — Samba GPO management and inspection
- PowerShell Group Policy cmdlets — GPO permission management
- `gpupdate` and `gpresult` — Group Policy validation

## Key Findings

- Alice's membership in `GPO-Editors` was confirmed through LDAP.
- The group's `GpoEdit` permission was verified on the test GPO.
- Initial SYSVOL write access was demonstrated using a temporary file.
- The excessive permission was removed.
- The repeated write attempt was denied.

## Repository Contents

- Lab setup and configuration notes
- GPO permissions testing workflow
- Remediation and retest evidence
- Security assessment report

## Scope and Disclaimer

This project was conducted in an isolated VirtualBox lab for educational and defensive security testing.

Only systems owned or explicitly authorized for testing should be assessed. The default domain policies were not used as test targets.
