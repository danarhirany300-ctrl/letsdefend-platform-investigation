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
