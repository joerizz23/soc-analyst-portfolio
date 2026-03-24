# Incident Report: Brute-Force Login Attempt

## Incident ID
SOC-001

## Alert Name
Multiple Failed Logins Followed by Success

## Date
March 2026

## Severity
High

## Status
Escalated

## Summary
An account experienced multiple failed login attempts from a single source IP within a short period, followed by a successful login. This pattern is consistent with a potential brute-force or credential stuffing attack and may indicate account compromise.

## Detection Source
Microsoft Sentinel / simulated authentication logs

## Investigation Steps
1. Reviewed failed login activity associated with the user account
2. Identified repeated failures from the same IP address
3. Confirmed that a successful login occurred shortly after the failures
4. Evaluated whether the source IP, login timing, and login pattern appeared suspicious

## Evidence Observed
| Field | Value |
|---|---|
| Source IP | 185.XX.XX.10 |
| Username | test.user |
| Hostname | DC-01 |
| Failed Attempts | 18 |
| Successful Login | Yes |
| Time Window | 10 minutes |

## Analysis
The sequence of repeated failed logins followed by a success strongly suggests password guessing or credential stuffing. This activity is suspicious because the failure volume exceeded normal user behavior and the successful login indicates the attacker may have guessed valid credentials.

## MITRE ATT&CK Mapping
- Technique: Brute Force
- Technique ID: T1110
- Tactic: Credential Access

## Recommended Actions
- Disable or lock the affected account temporarily
- Force a password reset
- Investigate whether MFA was enabled
- Block or monitor the source IP
- Review subsequent account activity for persistence or lateral movement

## Escalation Decision
Escalate to Tier 2. The successful login following repeated failures raises the likelihood of account compromise and requires deeper investigation into post-authentication behavior.

## Lessons Learned
This case highlights the importance of correlating failed and successful logins rather than reviewing them separately. It also reinforces the need for MFA and threshold-based alerting.
