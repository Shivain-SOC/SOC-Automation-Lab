# 🛡️ SOC Automation Project (Home Lab)

An end-to-end SOC automation pipeline using Wazuh, Shuffle (SOAR), TheHive (Case Management), and VirusTotal (Threat Intel). This project automates detection → enrichment → case creation → response.

---

## 📍 Architecture Overview

![image](https://github.com/user-attachments/assets/2896b434-dcdd-4263-81eb-244657043d90)


---

## 📦 Tools Used

- **Wazuh** – SIEM & endpoint detection
- **Shuffle** – SOAR platform
- **TheHive** – Case management
- **VirusTotal API** – Threat intelligence

---

## 🧩 Workflow Summary

### 🟢 Alert Detection via Wazuh

Mimikatz detection configured in Wazuh rules → triggers alert.

![image](https://github.com/user-attachments/assets/02b8ba26-6707-40ea-af4b-7becfb4de7b8)

---
![image](https://github.com/user-attachments/assets/87f8ebb9-343a-4005-a2f5-0b9aaeef5643)

---

### 🔗 Webhook Trigger in Shuffle

Configured webhook in Shuffle to receive Wazuh alerts.

![image](https://github.com/user-attachments/assets/4cccedb1-8c90-442d-846d-0ad72b81b7c4)


---

### 🔍 Hash Parsing with Regex + VirusTotal Lookup

Extracted hash from alert using Rex + sent to VirusTotal API.

![image](https://github.com/user-attachments/assets/bbd54325-fc21-4415-b36a-99f1f15927fe)

---

![image](https://github.com/user-attachments/assets/a9df37b6-d7ca-4c79-a67f-48ae486725ce)

---

![image](https://github.com/user-attachments/assets/24253e32-5bf8-4291-9b03-41c723f522aa)

---

### 📁 Case Management in TheHive

Automatically created alert → case in TheHive.

![image](https://github.com/user-attachments/assets/94dfbe92-bc1e-4436-afdb-d364c03d202d)

---
![image](https://github.com/user-attachments/assets/3d1205c3-06ad-4097-83e2-3e472b4d2d67)

---


### 🛑 Active Response

After analyst approval, source IP blocked automatically using Wazuh active response.

![image](https://github.com/user-attachments/assets/e8b98fc1-871e-411b-b812-1c0f149fcb6a)

![image](https://github.com/user-attachments/assets/c37ef8d6-cd5d-46c8-bcf2-5e2fc54d6f6b)

![image](https://github.com/user-attachments/assets/fdd65875-3ce1-49d1-9704-f9bd8b52d53b)


---



