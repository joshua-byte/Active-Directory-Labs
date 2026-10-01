# Active Directory BloodHound Assessment

Hands-on Active Directory security assessment performed in an isolated lab using BloodHound.

## Lab

- Domain: `corp.local`
- Domain Controller: `DC01.corp.local`
- DC IP: `192.168.56.101`
- Workstation: Windows 10
- Attacker: Kali Linux
- Tool: BloodHound CE
- Collector: `bloodhound-python`

## What I Practiced

- BloodHound data collection
- Active Directory relationship analysis
- Group membership analysis
- Privilege path analysis
- ACL analysis
- Identification of privileged group relationships
- Remediation and verification

## Assessment Finding

BloodHound identified the following privilege path:

```text
Alice → IT → Domain Admins
