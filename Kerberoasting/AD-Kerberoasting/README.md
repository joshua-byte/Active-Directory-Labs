# Active Directory Kerberoasting Lab

## Overview

Authorized, isolated Active Directory lab demonstrating:

- Active Directory SPN enumeration
- Identification of a user-backed service account
- Kerberos TGS acquisition
- Offline auditing of TGS-derived material
- Remediation considerations and re-test planning

## Lab Environment

| Component | Details |
|---|---|
| Domain | `CORP.LOCAL` |
| Domain Controller | `DC01` — `192.168.56.101` |
| Windows 10 workstation | `192.168.56.10` |
| Kali Linux | `192.168.56.106` |
| Service account | `sqlservice` |
| SPN | `MSSQLSvc/db01.corp.local:1433` |
| Network | VirtualBox Host-Only — `192.168.56.0/24` |
| Tools | Impacket GetUserSPNs, Hashcat |

## Attack Flow

```text
Authenticated domain user
        |
        v
SPN enumeration
        |
        v
User-backed service account identified
        |
        v
Kerberos TGS requested
        |
        v
TGS-derived material captured
        |
        v
Offline password audit
        |
        v
Lab credential recovered
```

## Key Finding

The deliberately created `sqlservice` account had a user-backed SPN and a password that was recoverable through an offline dictionary audit of the captured TGS-derived material.

The lab also observed an RC4-HMAC (etype 23) service ticket.

## Security Notes

This repository is intended for an authorized lab environment.

**Do not commit:**
- Passwords
- Recovered credentials
- Raw `$krb5tgs$...` ticket material
- Private keys
- Session cookies/tokens
- Unredacted terminal screenshots containing secrets

The evidence included in this repository has been redacted for publication.

## Report

See [`report/Kerberoasting_AD_Lab_Report.docx`](report/Kerberoasting_AD_Lab_Report.docx).

## Evidence

Publication-safe screenshots are in [`evidence/`](evidence/).

## Disclaimer

All testing documented here was performed against an isolated environment owned/controlled by the lab operator.
