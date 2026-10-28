# Active Directory Security Labs

A hands-on collection of Active Directory security assessments conducted in an isolated virtual lab. This repository documents enumeration, Kerberos attack techniques, directory permissions analysis, attack-path identification, security misconfigurations, and remediation validation.

The focus is on understanding how misconfigurations affect Active Directory security, reproducing findings in a controlled environment, and verifying whether remediation addresses the identified weakness.

## Lab Environment

The lab uses virtual machines to simulate a small Windows domain environment.

| Component | Configuration |
|---|---|
| Domain Controller | Windows Server 2022 |
| Workstation | Windows 10 |
| Attacker Machine | Kali Linux |
| Virtualization | Oracle VirtualBox |
| Directory Services | Active Directory Domain Services |
| Supporting Tools | Nmap, Impacket, BloodHound, LDAP utilities, SMB clients, PowerShell |

### Environment History

The original environment used the `corp.local` domain. After moving to a new computer, I rebuilt the lab using `adlab.test` for subsequent testing. Individual projects may therefore document different domain names and configurations.

Each lab's README and accompanying evidence describe the environment used for that specific exercise.

## Projects

| Project | Objective | Key Areas |
|---|---|---|
| [Active Directory Enumeration](./AD-Enumeration/) | Identify exposed services and enumerate directory information. | Nmap, LDAP, SMB, RPC, users, groups, computers, SYSVOL and NETLOGON |
| [Kerberoasting](./Kerberoasting/) | Examine service principal names and demonstrate the risks associated with Kerberos service-account password security. | SPN enumeration, Kerberos, offline password auditing |
| [AS-REP Roasting](./AS-REP%20Roasting/) | Reproduce and investigate an Active Directory pre-authentication misconfiguration. | Kerberos pre-authentication, Impacket, remediation and verification |
| [BloodHound Assessment](./BloodHound-Assessment/) | Map directory relationships and investigate potential privilege-escalation paths. | BloodHound, relationship analysis, ACLs, attack paths |
| [GPO Permissions Assessment](./GPO-Permissions/) | Assess the security implications of excessive Group Policy permissions. | GPO access control, SYSVOL permissions, remediation and retesting |
| [GenericAll ACL Assessment](./GenericAll-ACL/) | Investigate the impact of excessive `GenericAll` permissions in Active Directory. | Access control, group membership, privilege escalation, remediation |
| [LLMNR Mitigation](./LLMNR-Mitigation/) | Examine LLMNR-related risks and document mitigation measures. | Name-resolution security, configuration and validation |

Individual project directories contain their own documentation and, where available, detailed reports, screenshots, and supporting evidence.

## Skills Demonstrated

### Active Directory Enumeration
- Network and service discovery using Nmap
- LDAP directory enumeration
- SMB share and RPC enumeration
- User, group, and computer discovery
- SYSVOL and NETLOGON analysis

### Authentication and Kerberos Security
- Kerberos fundamentals
- Service Principal Name (SPN) enumeration
- Kerberoasting
- AS-REP Roasting
- Offline password auditing in a controlled lab

### Permissions and Attack-Path Analysis
- Group Policy Object (GPO) permission assessment
- Active Directory access control list (ACL) analysis
- BloodHound data collection and relationship analysis
- Identification of potential privilege-escalation paths
- Assessment of excessive permissions and their security impact

### Remediation and Validation
- Reproduction of controlled security misconfigurations
- Application of targeted remediation measures
- Retesting after configuration changes
- Comparison of pre-remediation and post-remediation results
- Documentation of findings and supporting evidence

## Testing Methodology

Where applicable, the labs follow a repeatable assessment workflow:

1. **Establish the baseline:** Document the relevant domain configuration, accounts, permissions, and security settings.
2. **Enumerate:** Identify exposed services, directory relationships, authentication settings, or excessive permissions.
3. **Validate the finding:** Reproduce the issue in the isolated lab and collect supporting evidence.
4. **Assess the impact:** Explain how the misconfiguration could affect confidentiality, integrity, or access control.
5. **Remediate:** Apply a targeted configuration change or permission correction.
6. **Retest:** Repeat the relevant checks to determine whether the original condition remains.
7. **Document:** Record the procedure, results, remediation, and verification evidence in the relevant project directory.

Not every project uses every step; individual READMEs describe the procedures performed for each assessment.

## Documentation and Evidence

The repository separates concise project READMEs from detailed technical reports.

- **README:** Summarizes the objective, environment, techniques, and outcome.
- **Detailed report:** Documents the assessment procedure, findings, impact, remediation, and verification where applicable.
- **Evidence:** Contains relevant screenshots and supporting artifacts.

Refer to each project's directory for its available documentation and evidence.

## Scope and Responsible Use

All attack demonstrations are performed in an isolated, self-managed virtual lab for educational purposes.

The techniques are intended to support defensive security learning, misconfiguration analysis, and remediation validation. Testing against systems or networks requires appropriate authorization.

## Repository Goals

This project is intended to build practical understanding of:

- Active Directory architecture and security
- Windows domain enumeration
- Kerberos authentication weaknesses
- Directory permissions and privilege relationships
- Security misconfiguration assessment
- Remediation and post-fix validation
- Technical reporting and evidence collection
