## 🛡️ LetsDefend Incident Investigation Summary

| Investigation | Category | Key Artifacts & IOCs | Key Findings | Verdict |
| :--- | :--- | :--- | :--- | :--- |
| **Malicious Macro Investigation 4** | Phishing / Weaponized Macro | **MD5:** `f2d0c66b801244c059f636d08a474079`<br>**URL:** `filetransfer.io`<br>**Technique:** VBA `AutoOpen()`, PowerShell | Obfuscated VBA macro auto-executed on open, attempting to invoke PowerShell to download a secondary payload. | **True Positive** |
| **RDP Brute Force Investigation 3** | Credential Access / RDP | **Attacker IP:** `218.92.0.56`<br>**Target User:** `Matthew`<br>**Port:** `3389`<br>**Event ID:** `4625`, `4624 (Logon Type 10)` | External brute-force attempt resulted in compromised credentials. Attacker logged in via RDP and ran host enumeration commands (`whoami`, `net user`). | **True Positive** |
| **Suspicious PowerShell Script Investigation** | Defense Evasion / Execution | **SHA256:** `970c7834e58b6...`<br>**File:** `EDR-Freeze_1.0.exe`<br>**Child Proc:** `WerFaultSecure.exe` | Abuse of PowerShell to fetch `EDRFreeze` from GitHub (designed to bypass EDR controls) and spawn living-off-the-land system binaries. | **True Positive** |
