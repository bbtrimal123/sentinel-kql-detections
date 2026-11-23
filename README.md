# Microsoft Sentinel KQL Detections

A hands-on cybersecurity portfolio focused on threat detection, security monitoring, and incident investigation using Microsoft Sentinel and Kusto Query Language (KQL).

This project demonstrates my development of practical detection engineering and SOC analyst skills, with detections mapped to the MITRE ATT&CK framework.

## Tools and Technologies

- Microsoft Sentinel
- Kusto Query Language (KQL)
- Microsoft Entra ID Sign-in Logs
- Microsoft Defender XDR (planned)
- MITRE ATT&CK Framework

## Detection Library

| Detection | MITRE ATT&CK | Status |
|---|---|---|
| [Password Spray Detection](detections/password-spray.kql) | T1110.003 – Password Spraying | Query created |
| Suspicious Sign-in Activity | T1078 – Valid Accounts | Planned |
| Suspicious MFA Activity | T1556.006 – Modify Authentication Process | Planned |
| Suspicious PowerShell Execution | T1059.001 – PowerShell | Planned |

## First Detection: Password Spraying

**Objective:** Identify potential password-spraying activity against multiple user accounts from the same source IP address.

**Data source:** Microsoft Entra ID `SigninLogs`

**Detection logic:**
- Analyse failed sign-in attempts within 15-minute windows.
- Identify IP addresses targeting at least 10 distinct users.
- Flag windows containing at least 20 failed sign-in attempts.

**Investigation approach:**
1. Review the source IP address and targeted accounts.
2. Check for successful sign-ins following failed attempts.
3. Investigate unusual locations, devices, and authentication patterns.
4. Review related security alerts and determine whether escalation is required.

**Limitations:** This detection is an illustrative example. It has not yet been validated against a production or lab dataset and may require tuning to reduce false positives.

## Project Goals

- Develop practical KQL threat-detection queries.
- Understand authentication attacks and suspicious activity.
- Map detections to MITRE ATT&CK techniques.
- Document investigation steps and false-positive considerations.
- Test and improve detection logic using authorised lab data.

## About Me

I am an IT professional with five years of experience in systems support and Microsoft 365 administration, currently developing my skills in security operations and threat detection.

**Certifications:**
- Microsoft Certified: Security Operations Analyst Associate (SC-200)
- Microsoft 365 Certified: Administrator Expert

My career goal is to transition into a cybersecurity analyst or security engineering role.

## Disclaimer

This repository is an independent learning and portfolio project. It contains no employer information, confidential logs, credentials, or production security data. All examples are intended for authorised security testing and educational purposes.# sentinel-kql-detections
