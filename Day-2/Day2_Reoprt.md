
```markdown
# 📧 Day 2: Suspicious Email Activity Investigation  
**Date:** September 05, 2025  
**Analyst:** Mohan Kumar  
**Dataset:** BOTS V2 (`index=botsv2`)  
**Sourcetype:** `stream:smtp`  
**Environment:** Splunk Enterprise on Ubuntu  
**Goal:** Investigate suspicious email activity by verifying SMTP data, identifying sent emails, checking for attachments and recipients, and confirming time spans.

---

## ✅ Investigation Summary

This case focused on analyzing outbound email traffic using the `stream:smtp` sourcetype. The objective was to identify potential misuse of email services, such as unauthorized attachments or mass mailing to external domains. The investigation confirmed data coverage, extracted sender/recipient patterns, and flagged suspicious attachments.

---

## 🔍 SPL Queries & Findings

### 🔹 Query 1: Confirm Index and Sourcetypes  
```spl
| tstats count where index=botsv2 by sourcetype
```
**Result:** Verified presence of `stream:smtp` among active sourcetypes.  
📸 Screenshot: `Query-1.png`

---

### 🔹 Query 2: Search All SMTP Events  
```spl
index=botsv2 sourcetype=stream:smtp earliest=0
```
**Result:** Retrieved full SMTP traffic logs for analysis.  
📸 Screenshot: `Query-2.png`

---

### 🔹 Query 3: Identify Sent Emails by Specific User  
```spl
index=botsv2 sourcetype=stream:smtp sender="*@domain.com" earliest=0
```
**Result:** Filtered emails sent by a specific user. Replace `*@domain.com` with actual sender for targeted analysis.  
📸 Screenshot: `Query-3.png`

---

### 🔹 Query 4: Investigate Attachments  
```spl
index=botsv2 sourcetype=stream:smtp attachment_filename=* earliest=0
```
**Result:** Found emails containing attachments. Flagged `.zip` and `.docm` files for deeper review.  
📸 Screenshot: `Query-4.png`

---

### 🔹 Query 5: List Recipients and Email Volume  
```spl
index=botsv2 sourcetype=stream:smtp | stats count by recipient
```
**Result:** Identified high-volume recipients and external domains.  
📸 Screenshot: `Query-5.png`

---

### 🔹 Query 6: Confirm Time Span of Email Activity  
```spl
index=botsv2 sourcetype=stream:smtp | stats earliest(_time) as First latest(_time) as Last
```
**Result:** Verified ingestion window and confirmed consistent timestamp coverage.  
📸 Screenshot: `Query-6.png`

---

## 🧠 MITRE ATT&CK Mapping

| Tactic | Technique | ID | Description |
|--------|-----------|----|-------------|
| **Initial Access** | Phishing: Spearphishing Attachment | T1566.001 | Malicious attachments used to gain access |
| **Initial Access** | Phishing: Spearphishing Link | T1566.002 | Links in emails leading to malicious sites |
| **Exfiltration** | Exfiltration Over Email | T1048.003 | Data sent out via email channels |
| **Execution** | User Execution | T1204 | User opens malicious attachment triggering execution |
| **Command and Control** | Application Layer Protocol: Email | T1071.003 | Email used for C2 communication |

> These mappings align your detection logic with adversary behavior and support playbook development.

---

## 📁 Artifacts

- `Day2_Report.md` – This report  
- `Query-1.png` to `Query-6.png` – Screenshots of SPL results  
- GitHub Path: `mohan2004kumar/BOTS-V2-Playbooks/Day2/`

---

## 🧠 Interview Notes

Be prepared to explain:
- How you used SPL to isolate suspicious email behavior
- What fields in `stream:smtp` were most useful (`sender`, `recipient`, `attachment_filename`)
- How MITRE mapping strengthens your detection and response strategy
- How you would escalate this case in a real SOC (e.g., alerting, IR playbook)

---

## 📌 Next Steps

- Begin **Day 3: Login Attempts Investigation**
- Create a phishing IR playbook based on today's findings
- Build a dashboard to monitor SMTP anomalies
```

