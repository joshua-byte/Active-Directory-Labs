# BloodHound Commands

## 1. Collect Data

```bash
bloodhound-python -u 'alice' -p -d corp.local -ns 192.168.56.101 -dc DC01.corp.local -c All
```

## 2. Check Files

```bash
ls -lh *.json
```

## 3. Start BloodHound

```bash
bloodhound-start
```

## 4. Check Domain Admins

```powershell
Get-ADGroupMember -Identity "Domain Admins"
```

## 5. Add IT to Domain Admins

```powershell
Add-ADGroupMember -Identity "Domain Admins" -Members "IT"
```

## 6. Remove IT from Domain Admins

```powershell
Remove-ADGroupMember -Identity "Domain Admins" -Members "IT" -Confirm:$false
```

## 7. BloodHound Path

Source:
`ALICE@CORP.LOCAL`

Target:
`DOMAIN ADMINS@CORP.LOCAL`

Observed path:

```text
ALICE@CORP.LOCAL -> IT@CORP.LOCAL -> DOMAIN ADMINS@CORP.LOCAL
```

After remediation:

```text
Path not found
```

## Notes

All commands were performed against an authorized Active Directory lab environment.
