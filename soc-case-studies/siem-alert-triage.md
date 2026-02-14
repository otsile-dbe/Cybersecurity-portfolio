# SIEM Alert Triage & Escalation Simulation – SOC L1

## Overview
Performed alert triage within a simulated SOC environment using a SIEM-style dashboard. Reviewed multiple alerts, prioritised based on risk, classified true vs false positives, and escalated confirmed threats to Level 2.

## Alerts Investigated
- Data exfiltration
- Phishing emails
- Web scanning activity
- Spike of domain discovery commands

## Critical Case: Domain Discovery Spike

The most significant alert involved a spike in Active Directory domain discovery commands on host DMZ-MSEXCHANGE-2013 (Windows Server 2012 R2), executed under NT AUTHORITY\SYSTEM. The process chain revealed w3wp.exe spawning revshell.exe, which then launched cmd.exe. Commands observed included whoami, whoami /priv, net user, net group "Domain Admins" /domain, and nltest /dclist. This behaviour is consistent with post-exploitation reconnaissance, where an attacker enumerates privileges, domain controllers, and high-value groups after gaining initial access. The presence of a reverse shell in a public directory combined with SYSTEM-level privileges strongly indicates potential server compromise and preparation for lateral movement. Based on this evidence, the severity was escalated to Critical and the incident was assigned to a Level 2 SOC analyst for immediate containment and further investigation. Refer to image below

<img width="2762" height="1428" alt="image" src="https://github.com/user-attachments/assets/1efdd7a5-fbb7-42e0-8f67-ea55c313e7be" />


## False Positive Example: Data Exfiltration (Zoom)

One alert initially flagged potential data exfiltration activity. Upon investigation, outbound traffic volume was found to closely match inbound traffic, reducing the likelihood of abnormal data transfer. Further analysis of ports, hostnames, and URLs confirmed that the destination infrastructure belonged to Zoom. The communication pattern aligned with legitimate video conferencing activity, and no anomalous indicators were observed. Based on contextual verification and log correlation, the alert was correctly classified as a false positive.

## Key Skills Demonstrated
- SIEM alert triage
- Log correlation
- Process lineage analysis
- Severity classification
- Escalation reporting
- True vs false positive validation

## Lessons Learned

This exercise reinforced the importance of context in security operations. Alerts alone do not provide complete visibility, and accurate triage requires combining log analysis, identity awareness, and situational understanding. I learned that communication and verification are essential when determining whether activity is malicious or legitimate. Effective SOC work requires structured reasoning, evidence-based decisions, and clear escalation when indicators suggest compromise.



