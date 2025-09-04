# BOTS V2 Playbooks
## Overview
21-day Splunk learning with BOTS V2 dataset. Daily case studies for SOC skills: SPL, incident response, playbooks. Uses `botsv2` index, `earliest=0`.

## Structure
- **/Day1/**: Amber’s web activity investigation with screenshots.
- Future: Day2, Day3, etc.
- Files: Reports (.md), queries (.txt), screenshots (.png).

## Day 1: Unusual Web Activity
**Date**: September 04, 2025  
**Scenario**: Amber (`amber`) browsed external sites post-acquisition failure. Used `stream:http` in `botsv2`.  
**Findings**: IP: 10.0.2.107; No competitor domain found. Monitor Amber’s activity.  
**Files**:  
- `Day1/Day1_Report.md`: Report with screenshots.  
- `Day1/Day1_Queries.txt`: SPL queries.  
- `Day1/Query1_Indexes.png` to `Query5_Time_Spans.png`: Results visuals.  

## Tools
- Splunk Enterprise (Ubuntu).  
- BOTS V2: [Download](https://s3.amazonaws.com/botsdataset/botsv2/botsv2_data_set.tgz).  
- GitHub: Tracks progress.

## Future
- 21 case studies.  
- Build playbooks, dashboards.  
- Prep for L1 SOC interviews.

## Contact
Open an issue for feedback.
