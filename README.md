
# 🛡️ BOTS V2 Playbooks – 21-Day SOC Analyst Sprint  
**Author:** Mohan Kumar  
**Environment:** Splunk Enterprise on Ubuntu  
**Dataset:** BOTS V2 (`index=botsv2`)  
**Goal:** Build a public SOC analyst portfolio with daily investigations, SPL queries, dashboards, and MITRE ATT&CK-aligned playbooks.

---

## 📅 Training Schedule Overview (Sep 04–Sep 24, 2025)

| Day | Case Study | Focus | MITRE Tactics |
|-----|------------|-------|----------------|
| Day 1 | Unusual Web Activity | `stream:http`, IP analysis | Reconnaissance, Collection |
| Day 2 | Suspicious Email Activity | `stream:smtp`, attachments, recipients | Initial Access, Exfiltration, C2 |
| Day 3 | Login Attempts | `wineventlog:security`, brute force | Credential Access |
| Day 4 | SSL Traffic Analysis | `stream:ssl`, certs | Command and Control |
| Day 5 | DNS Tunneling | `stream:dns`, anomalies | Exfiltration |
| Day 6 | File Transfers | `stream:ftp`, `stream:scp` | Collection, Exfiltration |
| Day 7 | Time Sync Audit | All sourcetypes | Detection Engineering |
| Day 8–14 | Threat Detection | Malware, insider threats, phishing | Multiple tactics |
| Day 15–21 | Dashboards & Playbooks | Visualizations, alerts, IR docs | Detection, Response, Recovery |

---

## 📁 Folder Structure

```
BOTS-V2-Playbooks/
├── Day1/
│   ├── Day1_Report.md
│   ├── Query-1.png
│   └── ...
├── Day2/
│   ├── Day2_Report.md
│   ├── Query-1.png
│   └── Query-6.png
...
├── Dashboards/
├── Playbooks/
└── README.md
```

---

## 🔍 Sample SPL Query (Day 2 – Email Investigation)

```spl
index=botsv2 sourcetype=stream:smtp | stats count by recipient
```

> Used to identify high-volume recipients and potential exfiltration targets.

---

## 🎯 MITRE ATT&CK Mapping (Example: Day 2)

| Tactic | Technique | ID | Description |
|--------|-----------|----|-------------|
| Initial Access | Phishing: Spearphishing Attachment | T1566.001 | Malicious attachments used to gain access |
| Initial Access | Phishing: Spearphishing Link | T1566.002 | Links in emails leading to malicious sites |
| Exfiltration | Exfiltration Over Email | T1048.003 | Data sent out via email channels |
| Execution | User Execution | T1204 | User opens malicious attachment triggering execution |
| Command and Control | Application Layer Protocol: Email | T1071.003 | Email used for C2 communication |

---

## 🧠 Interview Prep Focus

- SPL fluency and detection logic
- MITRE-aligned triage and escalation
- Dashboard and alert design
- Clear, reproducible documentation
- GitHub-based portfolio visibility

---

## 🚀 Next Steps

- Complete all 21 case studies
- Build dashboards for SMTP, login, and malware activity
- Publish playbooks for phishing, brute force, and insider threats
- Prepare for L1 SOC interviews with scenario-based answers

---

## 📬 Contact

**GitHub:** [mohan2004kumar](https://github.com/mohan2004kumar)  
**Email:** mohantyping123@gmail.com  

