# Phishing Email Investigation 1 - LetsDefend

## Overview

This project documents a phishing email investigation completed on the LetsDefend SOC platform. The investigation followed a real-world Security Operations Center (SOC) workflow, including alert triage, threat intelligence analysis, log analysis, endpoint containment, and incident documentation.

---

## Platform

- LetsDefend
- Scenario: SOC282 - Phishing Alert - Deceptive Mail Detected
- Incident Type: Email Phishing

---

## Objective

Investigate a phishing email alert, determine whether the user was compromised, contain the affected endpoint, and document the incident.

---

# Investigation Process

## 1. Alert Review

Reviewed the phishing alert and collected the following information:

- Event ID: 257
- Alert Rule: SOC282 - Phishing Alert - Deceptive Mail Detected
- Sender: free@coffeeshooop.com
- Recipient: Felix@letsdefend.io
- Subject: Free Coffee Voucher
- Sender IP: 103.80.134.63
- Device Action: Allowed

---

## 2. Email Analysis

Reviewed the email content.

### Findings

- Social engineering theme
- "Free Coffee Voucher"
- Malicious ZIP attachment
- Password-protected archive
- Embedded phishing URL

---

## 3. Threat Intelligence

### Sender IP

Checked using VirusTotal.

Result:

- 9/91 security vendors detected the sender IP as malicious/suspicious.

---

### Attachment

Attachment:

```
free-coffee.zip
```

Analyzed using VirusTotal.

Result:

- 11/92 detections
- Multiple vendors identified the attachment as malware.

---

## 4. Delivery Verification

Verified the email security action.

Device Action:

```
Allowed
```

Conclusion:

The email was successfully delivered to the recipient's mailbox.

---

## 5. Log Investigation

Identified the malicious Command and Control (C2) server.

C2 IP

```
37.120.233.226
```

Searched the IP address in Log Management.

Firewall logs showed multiple outbound connections from the internal endpoint.

Source Host

```
172.16.20.151
```

Destination

```
37.120.233.226
```

Conclusion:

The endpoint communicated with the attacker's infrastructure.

---

## 6. Incident Response

Completed the following response actions:

- Deleted the phishing email from the user's mailbox
- Contained the compromised endpoint using EDR
- Added Indicators of Compromise (IOCs)
- Documented investigation notes
- Closed the incident

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Sender Email | free@coffeeshooop.com |
| Sender IP | 103.80.134.63 |
| Attachment | free-coffee.zip |
| C2 IP | 37.120.233.226 |

---

# Tools Used

- LetsDefend SIEM
- VirusTotal
- Firewall Logs
- Endpoint Detection & Response (EDR)
- Email Security
- Threat Intelligence

---

# MITRE ATT&CK Techniques

- T1566.001 – Phishing: Spearphishing Attachment
- T1105 – Ingress Tool Transfer
- T1071 – Application Layer Protocol
- T1078 – Valid Accounts (Potential)
- T1583 – Acquire Infrastructure

---

# Skills Demonstrated

- SOC Alert Triage
- Email Security Analysis
- Threat Intelligence
- VirusTotal Investigation
- IOC Analysis
- Firewall Log Analysis
- Incident Response
- Endpoint Containment
- Security Documentation

---

# Lessons Learned

- Never trust a single indicator.
- Use multiple sources of evidence before reaching a conclusion.
- Threat intelligence improves confidence but does not replace investigation.
- Firewall logs can confirm communication with malicious infrastructure.
- EDR containment is critical after confirming endpoint compromise.
- Proper documentation is an essential part of every SOC investigation.

---

# Final Outcome

The phishing email successfully reached the user's mailbox and contained a malicious ZIP attachment. Firewall logs confirmed communication with the attacker's Command and Control (C2) server, indicating that the endpoint was compromised. The malicious email was removed, the endpoint was isolated using EDR, and the incident was successfully contained and documented.

---

**Author**

**Danar Hirany**

Software Engineering Student  

Salahaddin University

Aspiring SOC Analyst | Blue Team | Incident Response | Threat Detection | Cybersecurity

..................................................................................................................................................................


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

...................................................................................................................................................................

# RDP Brute Force Investigation 3 - LetsDefend

## Overview

This project documents a Security Operations Center (SOC) investigation of an RDP brute-force attack detected on the LetsDefend platform. The objective was to determine whether an external attacker successfully compromised a Windows endpoint through repeated Remote Desktop Protocol (RDP) login attempts.

---

## Platform

- Platform: LetsDefend
- Alert Rule: SOC176 - RDP Brute Force Detected
- Category: Authentication Attack
- Severity: Medium

---

# Objective

Investigate an RDP brute-force alert, verify the attacker's reputation, analyze authentication logs, determine whether the attack was successful, and document the findings.

---

# Alert Information

| Field | Value |
|--------|-------|
| Event ID | 234 |
| Rule | SOC176 - RDP Brute Force Detected |
| Source IP | 218.92.0.56 |
| Destination IP | 172.16.17.148 |
| Hostname | Matthew |
| Protocol | RDP |
| Firewall Action | Allowed |

---

# Investigation Process

## Step 1 – Alert Review

Reviewed the SIEM alert and identified:

- External source IP
- Target endpoint
- RDP protocol
- Firewall action
- Alert trigger reason

The alert indicated repeated failed login attempts using multiple non-existent usernames.

---

## Step 2 – Source IP Investigation

The source IP was investigated using VirusTotal.

**IP Address**

218.92.0.56

### Result

- Detected as suspicious by **8/91** security vendors.

Conclusion:

The IP address has a malicious reputation and required further investigation.

---

## Step 3 – Log Analysis

Searched Log Management for:

218.92.0.56

Verified:

- RDP connection attempts
- Destination host: Matthew
- Firewall allowed inbound RDP traffic

Conclusion:

The attacker successfully reached the RDP service.

---

## Step 4 – Scope of the Attack

Investigated whether the attacker targeted multiple systems.

Result:

- Only one endpoint (Matthew) was targeted.

Conclusion:

The activity appeared to be focused on a single host rather than a network-wide brute-force campaign.

---

## Step 5 – Authentication Analysis

Reviewed Windows Security logs.

Important Event IDs:

- Event ID 4625 – Failed Logon
- Event ID 4624 – Successful Logon

Findings:

- Multiple Event ID 4625 entries identified.
- No Event ID 4624 events from the attacker's IP.

Conclusion:

The brute-force attack was **unsuccessful**.

No evidence of unauthorized access was identified.

---

# Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Source IP | 218.92.0.56 |
| Protocol | RDP (TCP/3389) |

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1110 | Brute Force |
| T1021.001 | Remote Desktop Protocol (RDP) |
| T1078 | Valid Accounts (Attempted) |

---

# Tools Used

- LetsDefend
- VirusTotal
- Log Management (SIEM)
- Windows Security Logs

---

# Skills Demonstrated

- SOC Alert Triage
- Threat Intelligence
- IP Reputation Analysis
- Authentication Log Analysis
- Windows Event Log Investigation
- RDP Attack Investigation
- Brute Force Detection
- Incident Documentation

---

# Lessons Learned

- An allowed firewall connection does not mean authentication was successful.
- Windows Event ID 4625 indicates failed login attempts.
- Windows Event ID 4624 indicates a successful login.
- IP reputation should always be validated using threat intelligence.
- Authentication logs are essential for determining whether a brute-force attack resulted in account compromise.

---

# Final Outcome

The investigation confirmed an external RDP brute-force attack originating from IP address **218.92.0.56**. The attacker attempted multiple RDP logins against the endpoint **Matthew**, but all authentication attempts failed. No successful logon events were identified, and there was no evidence of account compromise. The incident was documented and closed as an unsuccessful brute-force attempt.

---

## Author

**Danar Hirany**

Software Engineering Student  
Aspiring SOC Analyst | Blue Team | Incident Response | Threat Detection

...................................................................................................................................................................

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








