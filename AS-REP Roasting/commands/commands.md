# AS-REP Roasting Lab — Command Reference

Lab details:
- Domain: `corp.local`
- NetBIOS domain: `CORP`
- Domain controller: `DC01`
- DC IP: `192.168.56.101`
- Test account: `asrep-test`
- Testing system: Kali Linux
- Tool: Impacket `GetNPUsers`

> Use only in your authorized, isolated lab. Do not share full ticket/hash output publicly.

## 1. Connectivity and DNS checks (Kali)

```bash
ping -c 3 192.168.56.101
nc -vz 192.168.56.101 88
nc -vz 192.168.56.101 389
getent hosts corp.local
getent hosts dc01.corp.local
```

Notes:
- TCP port 88 is used by Kerberos.
- TCP port 389 is commonly used by LDAP.
- An `inverse host lookup failed` warning from `nc` can appear even when the port check succeeds.
- An LDAP bind error does not by itself indicate whether a Kerberos request will succeed.

## 2. Check Impacket command syntax (Kali)

Use whichever form is available in your installation:

```bash
impacket-GetNPUsers -h
GetNPUsers.py -h
python3 GetNPUsers.py -h
```

## 3. Inspect the account setting (PowerShell on DC01)

```powershell
Get-ADUser "asrep-test" -Properties DoesNotRequirePreAuth |
    Select-Object SamAccountName, Enabled, DoesNotRequirePreAuth
```

Check all domain users for the setting:

```powershell
Get-ADUser -Filter * -Properties DoesNotRequirePreAuth |
    Select-Object SamAccountName, Enabled, DoesNotRequirePreAuth
```

## 4. Initial AS-REP validation (Kali)

Target the known lab account:

```bash
python3 GetNPUsers.py 'corp.local/asrep-test' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local \
  -request \
  -no-pass
```

Interpretation:
- Output beginning with `$krb5asrep$23$` means AS-REP ticket material was returned.
- If output says the user does not have `UF_DONT_REQUIRE_PREAUTH` set, pre-authentication is enabled for the account and the vulnerable condition is not present at that time.
- Record the observed output and redact the full ticket/hash material in any shared report.

## 5. Remediation (PowerShell on DC01)

Re-enable Kerberos pre-authentication for the lab test account:

```powershell
Set-ADAccountControl -Identity "asrep-test" -DoesNotRequirePreAuth $false
```

Verify the setting:

```powershell
Get-ADUser "asrep-test" -Properties DoesNotRequirePreAuth |
    Select-Object SamAccountName, Enabled, DoesNotRequirePreAuth
```

Expected after remediation:
- `Enabled`: `True` (if the account is intended to remain enabled)
- `DoesNotRequirePreAuth`: `False`

## 6. Retest (Kali)

Repeat the same command from Section 4:

```bash
python3 GetNPUsers.py 'corp.local/asrep-test' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local \
  -request \
  -no-pass
```

A passing retest should not return `$krb5asrep$23$...` ticket material for the account. Save the observed output as evidence. If troubleshooting is needed, record the exact error before changing unrelated settings.

## 7. Evidence checklist

- [ ] Connectivity screenshot (ping and Kerberos port check)
- [ ] Initial GetNPUsers output (redact ticket/hash material before sharing)
- [ ] PowerShell remediation command
- [ ] PowerShell verification showing `DoesNotRequirePreAuth = False`
- [ ] Post-remediation Kali retest output
- [ ] Final report with captions and a concise conclusion

## 8. Lab report notes

Record:
1. Objective and scope.
2. Commands executed and tool version.
3. Observed initial result.
4. Remediation performed.
5. Verified account configuration.
6. Retest output and whether it passed.
7. Any limitations or evidence not captured.

Do not claim that a password was cracked or an account was compromised unless that was actually demonstrated.
