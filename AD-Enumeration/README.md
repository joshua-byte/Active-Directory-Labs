# Active Directory Enumeration Lab

Hands-on Active Directory enumeration lab performed from a low-privileged domain user perspective in an isolated environment.

## Lab

- Domain: `corp.local`
- Domain Controller: `DC01.corp.local`
- DC IP: `192.168.56.101`
- Workstation: Windows 10
- Attacker: Kali Linux
- Domain User: `CORP\alice`

## What I Practiced

- Nmap service enumeration
- LDAP RootDSE enumeration
- LDAP user and group enumeration
- Computer enumeration
- User attribute analysis
- SMB share enumeration
- SYSVOL and NETLOGON analysis
- SMBMap permission mapping
- RPC enumeration
- Group Policy enumeration
- SPN enumeration
- Basic Kerberos concepts

## Key Findings

- Enumerated domain users, groups, computers, and services.
- Identified Alice as a low-privileged domain user and member of the `IT` group.
- Identified accessible SMB shares and their permissions.
- Analyzed `SYSVOL` and `NETLOGON`.
- Enumerated Group Policy objects and security settings.
- Identified domain Kerberos SPNs.
- No normal user-backed SPN was identified during the refined SPN enumeration.
