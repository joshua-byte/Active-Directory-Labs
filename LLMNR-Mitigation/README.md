# LLMNR Mitigation

## Overview

This project demonstrates how to disable Link-Local Multicast Name Resolution (LLMNR) on a Windows workstation to reduce the risk of LLMNR poisoning attacks.

## Vulnerability

LLMNR allows devices to resolve hostnames through multicast queries when normal name resolution fails. An attacker on the local network may respond with a malicious address, potentially redirecting clients and exposing authentication material.

## Environment

- **Target:** Windows 10
- **Monitoring:** Kali Linux
- **Network:** Isolated VirtualBox Host-Only Network

## Remediation

Disabled LLMNR using Windows Group Policy.

**Policy path:**

`Computer Configuration → Administrative Templates → Network → DNS Client → Turn off multicast name resolution`

**Configuration:** Enabled

Verified the registry policy value:

`HKLM\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient\EnableMulticast = 0`

## Verification

Used Wireshark and `tcpdump` to monitor LLMNR traffic over UDP port `5355`.

- **Before remediation:** LLMNR queries from the Windows workstation were observed.
- **After remediation:** No new LLMNR packets were observed during the post-remediation test.

These results support the conclusion that LLMNR was disabled on the tested workstation.

## Conclusion

Disabling LLMNR reduces the risk of name-resolution poisoning by preventing the workstation from using LLMNR for hostname resolution.

The mitigation was verified on a single Windows 10 workstation. Domain-wide enforcement and other name-resolution protocols were outside the scope of this project.

## Tools Used

- Windows Group Policy
- PowerShell
- Wireshark
- tcpdump
- Kali Linux
