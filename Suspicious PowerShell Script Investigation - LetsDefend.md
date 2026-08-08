# Suspicious PowerShell Script Investigation 2 - LetsDefend

## Overview

This project documents a real-world SOC investigation completed on the LetsDefend platform. The investigation focused on a malicious PowerShell script that was downloaded, executed, and attempted to retrieve an additional payload from external infrastructure.

---

## Platform

- Platform: LetsDefend
- Alert Rule: SOC153 - Suspicious PowerShell Script Executed
- Category: Malware
- Severity: Medium

---

# Objective

Investigate a suspicious PowerShell execution, determine whether the script executed successfully, identify any malicious network activity, contain the affected endpoint, and document the incident.

---

# Alert Information

| Field | Value |
|--------|-------|
| Event ID | 238 |
| Hostname | Tony |
| IP Address | 172.16.17.206 |
| File Name | payload_1.ps1 |
| File Path | C:\Users\LetsDefend\Downloads\payload_1.ps1 |
| AV/EDR Action | Detected |

---

# Investigation Process

## Step 1 – Alert Review

The alert indicated that a PowerShell script named `payload_1.ps1` was executed on the endpoint.

Initial information collected:

- Hostname
- Endpoint IP
- File path
- SHA-256 hash
- EDR detection status

---

## Step 2 – Threat Intelligence

The SHA-256 hash was investigated using VirusTotal.

**SHA-256**

```
db8be06ba6d2d3595dd0c86654a48cfc4c0c5408fdd3f4e1eaf342ac7a2479d0
```

### Result

- 35 / 62 security vendors detected the file as malicious.

Conclusion:

The script has a high-confidence malicious reputation.

---

## Step 3 – Download Analysis

Proxy logs showed:

- Process: chrome.exe
- URL:

```
https://files-ld.s3.us-east-2.amazonaws.com/payload_1.ps1
```

Conclusion:

The PowerShell script was downloaded through the user's web browser.

---

## Step 4 – Process Investigation

Process creation logs confirmed:

- powershell.exe executed
- payload_1.ps1 launched successfully

PowerShell Event ID 4104 showed:

```
IEX(IWR ...)
```

Meaning:

- Invoke-WebRequest downloaded remote content.
- Invoke-Expression executed the downloaded content.

This behavior is commonly associated with malware downloaders.

---

## Step 5 – Network Investigation

VirusTotal identified an additional malicious URL:

```
https://kionagranada.com/upload/beauty.exe
```

DNS logs confirmed:

- Domain queried:
  - kionagranada.com

Resolved IP:

```
161.22.46.148
```

Conclusion:

The malware attempted communication with external infrastructure to retrieve an additional payload.

---

## Step 6 – Endpoint Response

No evidence was found that the malware had been quarantined or cleaned.

The affected endpoint was isolated using the EDR platform to prevent further compromise.

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| SHA-256 | db8be06ba6d2d3595dd0c86654a48cfc4c0c5408fdd3f4e1eaf342ac7a2479d0 |
| File | payload_1.ps1 |
| Domain | kionagranada.com |
| URL | https://kionagranada.com/upload/beauty.exe |
| IP Address | 161.22.46.148 |

---

# MITRE ATT&CK Techniques

| Technique | Description |
|-----------|-------------|
| T1059.001 | PowerShell |
| T1105 | Ingress Tool Transfer |
| T1071 | Application Layer Protocol |
| T1055 | Command and Scripting Interpreter |
| T1106 | Native API |

---

# Tools Used

- LetsDefend
- VirusTotal
- Endpoint Detection & Response (EDR)
- Proxy Logs
- Sysmon Logs
- DNS Logs
- PowerShell Logs

---

# Skills Demonstrated

- SOC Alert Triage
- Threat Intelligence
- Malware Analysis
- PowerShell Investigation
- Process Analysis
- DNS Investigation
- Network Analysis
- IOC Identification
- Endpoint Containment
- Incident Documentation

---

# Lessons Learned

- PowerShell is a common tool abused by attackers.
- VirusTotal helps validate file reputation but should be combined with log analysis.
- Proxy, Sysmon, PowerShell, and DNS logs together provide a complete attack timeline.
- Detecting malware is different from confirming it was quarantined.
- Endpoint isolation is an important containment step after confirming malicious activity.

---

# Final Outcome

The investigation confirmed that a malicious PowerShell script was downloaded and executed on the endpoint. The script attempted to communicate with external infrastructure to retrieve an additional payload. The endpoint was contained using EDR, and the incident was documented and closed.

---

## Author

**Danar Hirany**

Software Engineering Student  
Aspiring SOC Analyst | Blue Team | Incident Response | Threat Detection

