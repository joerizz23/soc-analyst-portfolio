# Incident Report: Suspicious PowerShell Execution

## Incident ID
SOC-002

## Alert Name
Encoded PowerShell Command Detected

## Date
March 2026

## Severity
High

## Status
Escalated

## Summary
A PowerShell process was executed using an encoded command. Encoded PowerShell is commonly used by attackers to obfuscate malicious commands and evade detection. This activity is suspicious and may indicate malware execution or post-exploitation activity.

## Detection Source
Microsoft Sentinel / Endpoint process logs (simulated)

## Investigation Steps
1. Reviewed process execution logs
2. Identified PowerShell launched with encoded command
3. Checked parent process for suspicious origin
4. Evaluated command-line behavior
5. Assessed host activity around execution time

## Evidence Observed

| Field | Value |
|------|------|
| Hostname | WIN-USER01 |
| User | test.user |
| Process | powershell.exe |
| Parent Process | winword.exe |
| Command Line | powershell.exe -EncodedCommand SQBmACgA... |
| Time | 14:32 UTC |

## Analysis
PowerShell executed with an encoded command is a strong indicator of suspicious activity. Additionally, the parent process was Microsoft Word, which is commonly abused in phishing-based malware delivery. This suggests a possible malicious document executed PowerShell to download or execute payloads.

This behavior aligns with known attacker techniques involving script-based execution and obfuscation.

## MITRE ATT&CK Mapping

Technique: Command and Scripting Interpreter  
Technique ID: T1059.001  
Tactic: Execution  

Additional Technique: Obfuscated/Compressed Files  
Technique ID: T1027  

## Recommended Actions

- Isolate affected host
- Terminate suspicious PowerShell process
- Run endpoint malware scan
- Review network connections from host
- Investigate user email activity
- Check for persistence mechanisms

## Escalation Decision

Escalate to Tier 2. The use of encoded PowerShell combined with suspicious parent process suggests possible malware execution and requires deeper forensic analysis.

## Lessons Learned

Encoded PowerShell usage should always be treated as suspicious. Monitoring parent-child process relationships is critical for identifying phishing-based attacks and malicious document execution.
