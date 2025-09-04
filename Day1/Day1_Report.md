```markdown
# Day 1: Unusual Web Activity Investigation
**Date**: September 04, 2025  
**Environment**: BOTS V2; Index: botsv2; Time: All Time (earliest=0)  
**Goals**: Verify `botsv2` index and sourcetypes, identify Amber Turing’s IP and web activity, confirm data time spans.  

**Tasks Performed**:  
- Confirmed `botsv2` index exists.  
- Listed sourcetypes to verify `stream:http`.  
- Found Amber’s IP.  
- Analyzed Amber’s web traffic for competitor sites.  
- Checked web log time spans (~August 2017).  

**SPL Queries**:  
1. **List Indexes**: Verified `botsv2`.  
   ```spl
   | tstats count where index=* by index
   ```
   See [Query1_Indexes.png](Query1_Indexes.png).  
2. **List Sourcetypes**: Confirmed `stream:http`.  
   ```spl
   | tstats count where index=botsv2 by sourcetype
   ```
   See [Query2_Sourcetypes.png](Query2_Sourcetypes.png).  
3. **Amber Search**: Identified IP.  
   ```spl
   index=botsv2 earliest=0 amber
   ```
   See [Query3_Amber_Search.png](Query3_Amber_Search.png).  
4. **Web Traffic**: Checked for competitor sites.  
   ```spl
   index=botsv2 earliest=0 src_ip=10.0.2.107 sourcetype=stream:http
   ```
   See [Query4_Web_Traffic.png](Query4_Web_Traffic.png).  
5. **Time Spans**: Confirmed dates.  
   ```spl
   index=botsv2 earliest=0 src_ip=10.0.2.107 sourcetype=stream:http|stats count by src_ip
   ```
   See [Query5_Time_Spans.png](Query5_Time_Spans.png).  

**Case Investigated**: Alert about Amber Turing (`amber`) browsing external sites post-acquisition failure, suspecting insider risk or phishing.  

**Enrichment Results**: None (internal logs only).  

**Decisions/Evidence**:  
- Amber’s IP: `10.0.2.107` (Query 3).  
- Web Activity: No competitor domain found (Query 4).  
- Evidence: Confirmed Amber’s web activity, but no clear malicious intent.  
- MITRE ATT&CK: TA0007 (Discovery).  

**Escalation Notes**: No competitor domain; monitor Amber’s activity. No escalation.  

**Playbook Updates**: Saved Query 4 as “Amber_Web_Traffic”.  

**Next Actions**: Check Amber’s emails (`sourcetype=stream:smtp`) for phishing or data sharing (Day 2).
```

