# 🎓 21-Day SOC Analyst Training Guide – BOTS V2 on Splunk  
**Author:** Mohan Kumar  
**Environment:** Splunk Enterprise on Ubuntu  
**Dataset:** BOTS V2 (`index=botsv2`)  
**Purpose:** Help beginners master SOC analyst skills using daily case studies, SPL queries, MITRE ATT&CK mapping, and reproducible documentation.

---

## 🗓️ Daily Breakdown & Learning Objectives

---

### 📘 Day 1: Unusual Web Activity Investigation  
**Goal:** Learn how to verify data ingestion and analyze HTTP traffic.  
**Tasks:**
- Confirm `botsv2` index exists.
- List sourcetypes using `| tstats count where index=botsv2 by sourcetype`.
- Search for `stream:http` events.
- Identify user IPs and analyze web traffic.
- Look for visits to competitor domains.
- Check time span of data using `earliest(_time)` and `latest(_time)`.

**MITRE Tactics:**  
- **Reconnaissance** (T1595) – External browsing behavior  
- **Collection** (T1119) – Gathering web-based data

---

### 📘 Day 2: Suspicious Email Activity Investigation  
**Goal:** Investigate outbound emails, attachments, and recipients.  
**Tasks:**
- Search `stream:smtp` sourcetype.
- Identify sender and recipient fields.
- Look for suspicious attachments (`attachment_filename=*`).
- Count emails per recipient.
- Confirm time span of email activity.

**MITRE Tactics:**  
- **Initial Access** (T1566.001/.002) – Phishing via email  
- **Exfiltration** (T1048.003) – Data sent via email  
- **Execution** (T1204) – User opens malicious attachment  
- **Command and Control** (T1071.003) – Email used for C2

---

### 📘 Day 3: Login Attempts Investigation  
**Goal:** Detect brute force and failed login patterns.  
**Tasks:**
- Search `wineventlog:security` for `EventCode=4625` (failed logins).
- Group by `Account_Name`, `Source_Network_Address`.
- Count login attempts per user.
- Identify brute force indicators.

**MITRE Tactics:**  
- **Credential Access** (T1110) – Brute force login attempts  
- **Defense Evasion** (T1078) – Use of valid accounts

---

### 📘 Day 4: SSL Traffic Analysis  
**Goal:** Analyze encrypted traffic and suspicious certificates.  
**Tasks:**
- Search `stream:ssl` sourcetype.
- Extract fields like `ssl_subject`, `ssl_issuer`.
- Identify self-signed or expired certs.
- Look for unusual destinations.

**MITRE Tactics:**  
- **Command and Control** (T1041, T1071.001) – Encrypted C2 channels

---

### 📘 Day 5: DNS Tunneling Detection  
**Goal:** Spot abnormal DNS queries and tunneling behavior.  
**Tasks:**
- Search `stream:dns` sourcetype.
- Look for long domain names or frequent queries.
- Use `stats count by query` to find anomalies.

**MITRE Tactics:**  
- **Exfiltration** (T1048.002) – DNS used for data exfiltration  
- **Command and Control** (T1071.004) – DNS-based C2

---

### 📘 Day 6: File Transfer Monitoring  
**Goal:** Investigate FTP/SCP activity for data movement.  
**Tasks:**
- Search `stream:ftp` and `stream:scp`.
- Identify file names and transfer sizes.
- Flag large or sensitive file transfers.

**MITRE Tactics:**  
- **Collection** (T1119) – Gathering files  
- **Exfiltration** (T1041) – File transfer out of network

---

### 📘 Day 7: Time Synchronization Audit  
**Goal:** Validate timestamp consistency across logs.  
**Tasks:**
- Compare `_time` across multiple sourcetypes.
- Use `stats earliest(_time)` and `latest(_time)` per sourcetype.
- Identify time drift issues.

**MITRE Tactics:**  
- **Detection Engineering** – Ensuring reliable log correlation

---

### 📘 Day 8: Malware Beaconing Detection  
**Goal:** Detect periodic outbound traffic patterns.  
**Tasks:**
- Search `stream:http` or `stream:tcp`.
- Use `timechart count by dest_ip` to find regular intervals.
- Flag beacon-like behavior.

**MITRE Tactics:**  
- **Command and Control** (T1071) – Beaconing to external IPs

---

### 📘 Day 9: Insider Threat Investigation  
**Goal:** Track privileged user behavior and anomalies.  
**Tasks:**
- Search `wineventlog:security` for admin logins.
- Correlate with `stream:filesys` for file access.
- Identify unusual access times or file types.

**MITRE Tactics:**  
- **Privilege Escalation** (T1078)  
- **Collection** (T1005) – Sensitive file access

---

### 📘 Day 10: Phishing Email Detection  
**Goal:** Identify malicious senders and payloads.  
**Tasks:**
- Search `stream:smtp` for suspicious domains.
- Look for `.docm`, `.exe`, `.zip` attachments.
- Correlate with `stream:http` for clicked links.

**MITRE Tactics:**  
- **Initial Access** (T1566)  
- **Execution** (T1204)

---

### 📘 Day 11: Lateral Movement Detection  
**Goal:** Correlate login events across hosts.  
**Tasks:**
- Search `wineventlog:security` for `EventCode=4624`.
- Track user logins across multiple machines.
- Identify unusual access paths.

**MITRE Tactics:**  
- **Lateral Movement** (T1021) – Remote logins  
- **Credential Access** (T1550)

---

### 📘 Day 12: Data Exfiltration via HTTP  
**Goal:** Detect large outbound transfers.  
**Tasks:**
- Search `stream:http` for large `content_length`.
- Identify destination IPs and domains.
- Flag unusual upload behavior.

**MITRE Tactics:**  
- **Exfiltration** (T1041)

---

### 📘 Day 13: MITRE ATT&CK Mapping Practice  
**Goal:** Align detections with MITRE techniques.  
**Tasks:**
- Review previous cases.
- Map each detection to MITRE TTPs.
- Document mappings in playbooks.

**MITRE Tactics:**  
- All relevant tactics from prior days

---

### 📘 Day 14: Alert Tuning & False Positive Reduction  
**Goal:** Refine SPL queries to reduce noise.  
**Tasks:**
- Review alert logic.
- Add filters for known safe behavior.
- Use `where`, `regex`, `searchmatch` to tune results.

**MITRE Tactics:**  
- **Detection Engineering**

---

### 📘 Day 15: Dashboard Design  
**Goal:** Build visualizations for SOC KPIs.  
**Tasks:**
- Use `timechart`, `top`, `stats` in panels.
- Create dashboards for login attempts, SMTP, malware.
- Save and export dashboard views.

**MITRE Tactics:**  
- **Detection** (T1070) – Visual monitoring

---

### 📘 Day 16: Alerting Framework  
**Goal:** Create SPL-based alerts.  
**Tasks:**
- Convert queries into saved searches.
- Set thresholds and trigger conditions.
- Configure email or webhook alerts.

**MITRE Tactics:**  
- **Detection**  
- **Response**

---

### 📘 Day 17: Phishing IR Playbook  
**Goal:** Document steps to respond to phishing.  
**Tasks:**
- Define detection logic.
- Outline triage, containment, and escalation.
- Include MITRE mapping and SPL queries.

**MITRE Tactics:**  
- **Initial Access**, **Execution**, **Response**

---

### 📘 Day 18: Malware IR Playbook  
**Goal:** Document steps to respond to malware.  
**Tasks:**
- Define indicators of compromise.
- Outline investigation and remediation steps.
- Include MITRE mapping and SPL queries.

**MITRE Tactics:**  
- **Execution**, **Persistence**, **C2**, **Response**

---

### 📘 Day 19: GitHub Sync & Review  
**Goal:** Upload all reports and screenshots.  
**Tasks:**
- Organize folders by day.
- Push `.md` files and `.png` screenshots.
- Review commit history and structure.

---

### 📘 Day 20: Interview Simulation  
**Goal:** Practice L1 SOC interview questions.  
**Tasks:**
- Prepare self-introduction.
- Answer technical and HR questions.
- Use case studies as examples.

---

### 📘 Day 21: Final Portfolio Review  
**Goal:** Polish documentation and dashboards.  
**Tasks:**
- Review all `.md` files for clarity.
- Ensure screenshots are linked correctly.
- Final push to GitHub for public visibility.

---

## 🧠 Tips for Beginners

- Use `index=botsv2
