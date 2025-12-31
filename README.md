# 🛡️ Cybersecurity Threat Modeling (NIST SP 800-30)

> **Project Type:** Theoretical framework study refined with a Python Notebook for risk scoring automation.

This repository documents threat sources, threat events, and risk evaluation concepts based on the **NIST SP 800-30** framework. It serves as a professional reference for cybersecurity students, SOC analysts, and risk management experts to bridge the gap between compliance theory and technical application.

---

## 📂 Threat Sources

| Type | Examples | Description |
| :--- | :--- | :--- |
| **Standard user** | Employee, Customer | May accidentally or intentionally exploit cyber resources. |
| **Privileged user** | System administrator | Greater access, higher risk of misuse or misconfiguration. |
| **Group** | Competitor, Supplier | External entities with potential malicious intent. |
| **Nation state / APT** | Hacker, Hacktivist, APT | Advanced persistent threats with significant resources. |
| **Hardware/Software** | Storage, OS, Networking | Failures or malicious software impacting systems. |
| **Operational env.** | Power outages, Weather | Non-human accidental factors causing disruptions. |

---

## ⚡ Threat Events

| Example Event | Description |
| :--- | :--- |
| **Reconnaissance** | Scans or observes vulnerabilities to prepare an attack. |
| **Exfiltration** | Stealing sensitive data using malicious software. |
| **Alter/Delete** | Data manipulation impacting business operations. |
| **Counterfeit Certs** | Compromise of a certificate authority for impersonation. |
| **Network Sniffing** | Long-term monitoring of network traffic to capture info. |
| **Denial of Service** | Overwhelming systems to prevent user access. |
| **Man-in-the-Middle** | Eavesdropping and relaying communications deceptively. |

---

## 📊 Risk Evaluation (Likelihood vs Severity)

To quantify risk, we use qualitative and quantitative scales from NIST SP 800-30.

### 1. Likelihood
* **High (3):** Almost certain to occur; threat source has high motivation and capability.
* **Moderate (2):** Somewhat likely; potential vulnerabilities exist.
* **Low (1):** Highly unlikely; minor/negligible effects.

### 2. Severity (Impact)
* **High (3):** Severe/catastrophic impact on assets and mission-critical operations.
* **Moderate (2):** Significant reduction in organizational functionality.
* **Low (1):** Minor/negligible impact on operations.

---

## 🛠️ Risk Scorer - NIST SP 800-30 Log Analyzer

This script quantifies the risk associated with cybersecurity events detected in system logs, such as those identified during a vulnerability analysis.

### 1. Calculation Logic
The script uses a simplified methodology based on the product of likelihood and severity:  
**Risk Score = Likelihood × Severity** (Scale of 1 to 9).

### 2. Usage
The Python script below automates this calculation to prioritize incidents:

```python
def calculate_risk(likelihood, severity):
    """
    Calculates the risk score based on NIST SP 800-30.
    Values: High=3, Moderate=2, Low=1
    """
    return likelihood * severity

# Example: Analysis for a Denial of Service (DoS) attack
# Likelihood: Moderate (2) | Severity: High (3)
score = calculate_risk(likelihood=2, severity=3)
print(f"Risk Score for DoS attack: {score}/9")
```
---

### 3. Practical Application (Case Studies)
Here is how to apply this script to events extracted from logs to prioritize interventions:

* **Case A: Unusual Administrator Login** *Likelihood: 2 | Severity: 3* -> **Score: 6 (High Risk)**
* **Case B: Sensitive Data Manipulation** *Likelihood: 3 | Severity: 3* -> **Score: 9 (Critical Risk)**
* **Case C: Failed Login Attempts (Brute Force)** *Likelihood: 3 | Severity: 1* -> **Score: 3 (Low Risk)**



---

### 4. Escalation Recommendations
Based on these scores, the security team should handle alerts in the following order of priority:

1. **Critical Priority (Score 9):** Immediate intervention (**Incident Response**) for **Case B**.
2. **High Priority (Score 6):** Deep investigation for **Case A** to check for potential account compromise.
3. **Low Priority (Score 1-3):** Automated monitoring and password policy hardening for **Case C**.

---

