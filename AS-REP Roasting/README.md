# AS-REP Roasting — Active Directory Security Lab

## Overview

This lab demonstrates AS-REP Roasting in an Active Directory environment. The exercise examines Kerberos pre-authentication, validates the initial configuration using Impacket, applies remediation, and records the verification results.

## Lab Environment

| Component | Details |
|---|---|
| Domain | `corp.local` |
| NetBIOS Domain | `CORP` |
| Domain Controller | `DC01` |
| Domain Controller IP | `192.168.56.101` |
| Testing Machine | Kali Linux |
| Server OS | Windows Server 2022 |
| Tool | Impacket `GetNPUsers` |

## Objective

To understand how disabling Kerberos pre-authentication can expose an Active Directory account to AS-REP Roasting and to verify the remediation by repeating the original test.

## Background

Kerberos pre-authentication helps verify that a user requesting a Ticket-Granting Ticket (TGT) knows the account's secret.

When pre-authentication is disabled for an account, an unauthenticated requester may be able to obtain AS-REP ticket material. This material can be used for offline password guessing.

## Procedure

### 1. Verify Connectivity

The domain controller's reachability and Kerberos service were checked from Kali Linux.

```bash
ping -c 3 192.168.56.101
nc -vz 192.168.56.101 88
getent hosts dc01.corp.local
```

**Observed results:**
- Ping completed with 0% packet loss.
- Kerberos TCP port 88 was open.
- `dc01.corp.local` resolved to `192.168.56.101`.

### 2. Perform the Initial AS-REP Test

Impacket `GetNPUsers` was used to request ticket material for the known lab account.

```bash
python3 GetNPUsers.py 'corp.local/asrep-test' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local \
  -request \
  -no-pass
```

**Observed result:** The screenshot showed output beginning with `$krb5asrep$23$asrep-test@CORP.LOCAL`.

This confirmed that AS-REP ticket material was returned during the initial test.

### 3. Apply Remediation

On the domain controller, Kerberos pre-authentication was re-enabled for the test account.

```powershell
Set-ADAccountControl -Identity "asrep-test" -DoesNotRequirePreAuth $false
```

### 4. Verify the Configuration

The account's configuration was checked using PowerShell.

```powershell
Get-ADUser "asrep-test" -Properties DoesNotRequirePreAuth |
    Select-Object SamAccountName, Enabled, DoesNotRequirePreAuth
```

**Observed result:**

| Property | Value |
|---|---|
| SamAccountName | `asrep-test` |
| Enabled | `True` |
| DoesNotRequirePreAuth | `False` |

The output confirmed that the account remained enabled and the pre-authentication setting had been corrected.

### 5. Retest

The same Impacket request was repeated after remediation.

The retest was reported as completed. The expected passing result is that the request no longer returns AS-REP ticket material for the account.

## Findings

- The initial request returned AS-REP ticket material.
- The account's pre-authentication setting was subsequently corrected.
- PowerShell confirmed that `DoesNotRequirePreAuth` was `False`.
- The user reported completing the retest.

## Security Recommendations

- Keep Kerberos pre-authentication enabled for user accounts unless a documented exception is required.
- Audit Active Directory for accounts with pre-authentication disabled.
- Use strong, unique passwords.
- Apply the principle of least privilege to domain accounts.
- Retest after remediation to verify that the issue has been addressed.

## Detailed Report

See [AS-REP Roasting Lab Report](./AD_ASREP_Report.docx)
for the full methodology, screenshots, findings, and remediation.

## Evidence

Screenshots used to validate the test and remediation are
available in [`evidence/`](./evidence/).
