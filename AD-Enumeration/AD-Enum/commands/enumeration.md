# AD Enumeration Commands

## Nmap
```bash
nmap -sC -sV 192.168.56.101
```

## LDAP — RootDSE
```bash
ldapsearch -x -H ldap://192.168.56.101 -s base -b "" namingContexts
```

## LDAP — Users
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "DC=corp,DC=local" -s subtree "(objectClass=user)" sAMAccountName
```

## LDAP — Groups
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "DC=corp,DC=local" -s subtree "(objectClass=group)" sAMAccountName member
```

## LDAP — Alice
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "CN=Alice,CN=Users,DC=corp,DC=local" -s base "(objectClass=*)" "*"
```

## LDAP — Computers
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "DC=corp,DC=local" -s subtree "(objectClass=computer)" sAMAccountName dNSHostName operatingSystem operatingSystemVersion userAccountControl
```

## LDAP — GPOs
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "CN=Policies,CN=System,DC=corp,DC=local" -s subtree "(objectClass=groupPolicyContainer)" displayName name distinguishedName gPCFileSysPath
```

## LDAP — SPNs
```bash
ldapsearch -x -H ldap://192.168.56.101 -D "alice@corp.local" -W -b "DC=corp,DC=local" -s subtree "(&(objectCategory=person)(servicePrincipalName=*))" sAMAccountName servicePrincipalName
```

## SMB
```bash
smbclient -L //192.168.56.101 -U "CORP/alice"
smbclient //192.168.56.101/SYSVOL -U "CORP/alice"
```

## SMBMap
```bash
smbmap -H 192.168.56.101 -u alice -p '[ALICE_PASSWORD]' -d CORP
```

## RPC
```bash
rpcclient -U "CORP/alice" 192.168.56.101
```

Inside rpcclient:
```text
enumdomusers
enumdomgroups
queryuser alice
queryusergroups 0x44f
```

> All commands in this repository were used only against the authorized lab environment.
