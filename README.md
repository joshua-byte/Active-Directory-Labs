# Active Directory Lab

Hands-on Active Directory security lab documenting enumeration, authentication, and controlled attack techniques in an isolated environment.

## Lab

- Domain: `corp.local`
- Domain Controller: `DC01.corp.local`
- DC IP: `192.168.56.101`
- Workstation: Windows 10 / `Windows.corp.local`
- Attacker: Kali Linux
- Domain user: `CORP\alice`

### Lab Environment

The lab was initially configured under `corp.local`. After moving to a new computer, I rebuilt the environment using `adlab.test` for subsequent testing. Domain names and configurations may therefore differ between individual lab projects.

## What I Practiced

- Nmap service enumeration
- LDAP enumeration
- User and group enumeration
- Computer enumeration
- RPC enumeration
- SMB share enumeration
- SYSVOL and NETLOGON analysis
- Group Policy enumeration
- Kerberos fundamentals
- SPN enumeration
- Kerberoasting
- Offline password auditing
