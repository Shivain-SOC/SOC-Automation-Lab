# 🛡️ SOC Automation Project (Home Lab)

This SOC Automation Home Lab simulates a real-world Security Operations Center setup using open-source tools. The project demonstrates **end-to-end threat detection, enrichment, triage, and automated response** by integrating Wazuh, Sysmon, The Hive, Shuffle, and VirusTotal APIs. The workflow detects suspicious activity like credential theft (Mimikatz), investigates file hashes, creates cases, and executes automated actions — all without manual intervention.

---

## 🎯 Objective

To build a fully automated SOC environment that:
- Detects advanced threats using Sysmon telemetry
- Enriches alerts using VirusTotal and ChatGPT
- Creates incident cases automatically in The Hive
- Executes active response (e.g., block IP, disable account)
- Includes analyst approval flow before critical action
- Uses SquareX for safe web investigation of phishing links

---

## 📦 Tech Stack

| Tool         | Role                                                             |
|--------------|------------------------------------------------------------------|
| **Wazuh**     | Host-based Intrusion Detection + Log Aggregation (SIEM)         |
| **Sysmon**    | Windows telemetry collector (processes, hashes, registry, etc.) |
| **Filebeat**  | Log shipper for Windows Events                                  |
| **Shuffle**   | SOAR platform for automation workflows                          |
| **The Hive**  | Case management system                                          |
| **VirusTotal**| Threat intelligence API (v3)                                    |

---

## 🧰 Part-by-Part Breakdown

### ✅ **Part 1: Initial Setup**
- Deployed **Wazuh Manager** on Ubuntu using DigitalOcean
- Installed **Sysmon** on a Windows 10 VM using SwiftOnSecurity config
- Set up **Filebeat** to forward Windows logs to the Wazuh manager
- Confirmed telemetry ingestion via the Wazuh dashboard
- Purpose: Lay the groundwork for agent telemetry and centralized detection

---

### 🔐 **Part 2: Mimikatz Simulation and Detection**
- Executed **Mimikatz** on the Windows VM to simulate credential theft
- Created a **custom decoder and rule** in Wazuh to detect:
  - `original_file_name: mimikatz.exe`
  - `event_id: 1` and `command_line` strings
- Confirmed that Wazuh generated accurate alerts
- Demonstrated **evasion techniques** (renamed binary) and how to detect them

---

### 📊 **Part 3: Enhanced Logging and Custom SIEM Rules**
- Enabled advanced logging:
  - Included Sysmon channels in `ossec.conf`
  - Set `logall: yes` for full archival
- Verified that renamed Mimikatz variants still triggered alerts
- Created robust detection rules based on **hashes and original file names** to mitigate evasion
- Ensured rules generated alerts regardless of filename manipulation

---

### 🤖 **Part 4: SOAR Integration and Threat Automation**

#### 🔁 Webhook + Alert Trigger
- Connected Wazuh to **Shuffle** using a webhook trigger
- Configured `ossec.conf` to send alerts to Shuffle URL
- Triggered alerts when a Mimikatz event is detected

#### 🧠 VirusTotal Hash Lookup
- Extracted file hashes using **Regex**
- Called **VirusTotal v3 API** to check hash reputation
- Debugged a 404 error by fixing the app logic (from `/report` to `/file/{id}`)

#### 📁 Case Creation in The Hive
- Created a new **organization, analyst user, and service account**
- Generated an **API key** for integration with Shuffle
- Configured the Hive App in Shuffle to create a case with alert metadata:
  - Title, severity, source IP, tag, summary, and observables

#### 👩‍💻 Analyst Interaction & Active Response
- Enabled **manual approval** in Shuffle:
  - Analyst receives prompt to approve IP block
- Once approved, Shuffle triggers **active response**:
  - Blocks the IP via `iptables` or disables account
- Logged the response in Hive case history

#### 🧪 SquareX Integration
- Demonstrated using **SquareX** to open suspicious URLs safely in a disposable browser
- Used for phishing investigation, file preview, and web behavior analysis
- Highlighted benefits of real-time browser isolation for SOC analysts

---

## ⚙️ Additional Setup

- Created firewall rules for Wazuh API to allow external testing
- Edited the Wasa API URL to use a **public IP**
- Simulated SSH brute-force attack for testing detection workflows
- Added execution arguments in Shuffle for identifying agents dynamically

---

## 📌 Learning Outcomes

- ✅ Mastered SIEM + SOAR + Case Management Integration
- ✅ Used Regex + VirusTotal for automatic enrichment
- ✅ Implemented approval-based response workflows
- ✅ Understood safe analysis of phishing via browser isolation
- ✅ Gained hands-on experience with APIs and SOC tooling

---

> _"Good analysts detect threats. Great analysts automate them."_ 💻⚡

