# Malicious Macro Investigation 4 - LetsDefend

## Overview

This project documents a Security Operations Center (SOC) investigation of a malicious Microsoft Word macro detected on a Windows endpoint. The investigation focused on determining whether the document executed malicious code, identifying its network activity, and containing the affected endpoint.

---

## Platform

- Platform: LetsDefend
- Alert Rule: SOC205 - Malicious Macro has been executed
- Category: Malware
- Severity: Medium

---

# Objective

Investigate a malicious Office document, determine whether the macro executed, identify command-and-control (C2) infrastructure, analyze endpoint and network logs, and document the incident.

---

# Alert Information

| Field | Value |
|--------|-------|
| Event ID | 231 |
| Rule | SOC205 - Malicious Macro has been executed |
| Hostname | Jayne |
| IP Address | 172.16.17.198 |
| File Name | edit1-invoice.docm |
| File Path | C:\Users\LetsDefend\Downloads\edit1-invoice.docm |
| SHA-256 | 1a819d18c9a9de4f81829c4cd55a17f767443c22f9b30ca953866827e5d96fb0 |
| AV/EDR Action | Detected |

---

# Investigation Process

## Step 1 – Alert Review

Reviewed the alert details and identified a suspicious Microsoft Word document containing VBA macros.

The file was located in the user's Downloads folder and detected by the endpoint protection platform.

---

## Step 2 – Malware Analysis

The SHA-256 hash was analyzed using VirusTotal.

Findings:

- The document contained VBA macros (`vbaProject.bin`).
- Multiple antivirus engines detected the file as malicious.

---

## Step 3 – C2 Identification

Threat intelligence analysis identified the following infrastructure:

**Domain**

www.greyhathacker.net

**Resolved IP**

92.204.221.16

---

## Step 4 – Endpoint Investigation

Windows Event Logs confirmed:

### Event ID 4688

A new process was created:

powershell.exe

### Event ID 4104

PowerShell executed a script containing:

DownloadFile()

This confirmed the malicious macro launched PowerShell.

---

## Step 5 – DNS Analysis

Sysmon Event ID 22 recorded:

DNS Query

www.greyhathacker.net

↓

92.204.221.16

This demonstrated that the endpoint resolved the malicious domain before attempting network communication.

---

## Step 6 – Proxy Log Analysis

Proxy logs recorded:

GET

http://www.greyhathacker.net/tools/messbox.exe

Process:

powershell.exe

HTTP Status:

404 Not Found

Although the payload was unavailable, the endpoint attempted outbound communication to attacker-controlled infrastructure.

---

## Step 7 – Containment

The affected endpoint was contained using the EDR platform to prevent additional malicious activity.

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| SHA-256 | 1a819d18c9a9de4f81829c4cd55a17f767443c22f9b30ca953866827e5d96fb0 |
| Domain | www.greyhathacker.net |
| IP Address | 92.204.221.16 |
| Process | powershell.exe |

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1566.001 | Phishing: Spearphishing Attachment |
| T1204.002 | User Execution: Malicious File |
| T1059.001 | PowerShell |
| T1105 | Ingress Tool Transfer |
| T1071.001 | Application Layer Protocol (HTTP) |

---

# Tools Used

- LetsDefend
- VirusTotal
- Log Management (SIEM)
- Endpoint Security (EDR)
- Sysmon Logs
- PowerShell Operational Logs
- Proxy Logs

---

# Skills Demonstrated

- SOC Alert Triage
- Malware Investigation
- Office Macro Analysis
- PowerShell Log Analysis
- Threat Intelligence
- DNS Investigation
- Proxy Log Analysis
- IOC Identification
- Endpoint Containment
- Incident Documentation

---

# Lessons Learned

- Microsoft Office macros can execute PowerShell commands.
- PowerShell Event ID 4104 provides valuable visibility into executed scripts.
- Sysmon DNS events help identify malicious infrastructure.
- Proxy logs can confirm outbound malware communications.
- Even if malware download fails (HTTP 404), the execution attempt is still a security incident.
- Combining endpoint, DNS, and proxy logs provides a complete attack timeline.

---

# Attack Timeline

1. User opened `edit1-invoice.docm`.
2. The embedded macro executed.
3. The macro launched `powershell.exe`.
4. PowerShell attempted to download `messbox.exe`.
5. DNS resolved `www.greyhathacker.net` to `92.204.221.16`.
6. The proxy recorded an HTTP GET request.
7. The server returned HTTP 404.
8. The endpoint was contained.

---

# Final Outcome

The investigation confirmed that a malicious Microsoft Word document executed PowerShell and attempted to download an additional payload from external infrastructure. DNS and proxy logs verified outbound communication with the malicious domain. Although the payload download returned HTTP 404, the macro executed successfully and demonstrated malicious behavior. The endpoint was contained, indicators of compromise were documented, and the incident was resolved.

---

## Author

**Danar Hirany**

Software Engineering Student

Aspiring SOC Analyst | Blue Team | Incident Response | Threat Detection
