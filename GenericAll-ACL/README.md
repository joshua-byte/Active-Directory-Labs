# AD-GenericAll-ACL-Assessment

Hands-on Active Directory security assessment performed in an isolated lab using BloodHound.

## Lab

- Domain: `corp.local`
- Domain Controller: `**DC01**`
- DC IP: `**192**.**168**.56.**101**`
- Workstation: Windows 10
- Attacker: Kali Linux
- Tool: BloodHound CE
- Collector: `bloodhound-python`

## What I Practiced

- BloodHound data collection
- Active Directory relationship analysis
- **ACL** analysis
- GenericAll permissions
- Group membership analysis
- Privilege escalation path validation
- Remediation and re-testing

## Finding

BloodHound identified:

```text Bob → GenericAll → IT → Domain Admins ```

Bob was able to add himself to the `IT` group and obtain `Domain Admins` membership.

The excessive **ACL** permission was removed and the path was no longer present after re-testing.


## Scope

All testing was performed against an authorized Active Directory lab environment.
