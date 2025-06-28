# 🛡️ SOC Automation Project (Home Lab)

An end-to-end SOC automation pipeline using Wazuh, Shuffle (SOAR), TheHive (Case Management), and VirusTotal (Threat Intel). This project automates detection → enrichment → case creation → response.

---

## 📍 Architecture Overview

![Architecture Diagram](images/architecture-overview.png)

---

## 📦 Tools Used

- **Wazuh** – SIEM & endpoint detection
- **Shuffle** – SOAR platform
- **TheHive** – Case management
- **VirusTotal API** – Threat intelligence
- **SquareX** – Isolated browser analysis

---

## 🧩 Workflow Summary

### 🟢 Alert Detection via Wazuh

Mimikatz detection configured in Wazuh rules → triggers alert.

![Wazuh Alert](images/alert-detection.png)

---

### 🔗 Webhook Trigger in Shuffle

Configured webhook in Shuffle to receive Wazuh alerts.

![Shuffle Webhook](images/shuffle-workflow.png)

---

### 🔍 Hash Parsing with Regex + VirusTotal Lookup

Extracted hash from alert using Rex + sent to VirusTotal API.

![VirusTotal Result](images/virus-total-response.png)

---

### 📁 Case Management in TheHive

Automatically created alert → case in TheHive.

![TheHive Case](images/thehive-case.png)

---

### 🧪 Sandbox via SquareX

Analyzed phishing URLs safely with SquareX browser.

![SquareX Analysis](images/squarex-analysis.png)

---

### 🛑 Active Response

After analyst approval, source IP blocked automatically using Wazuh active response.

![Active Response](images/active-response.png)

---



