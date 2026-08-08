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
