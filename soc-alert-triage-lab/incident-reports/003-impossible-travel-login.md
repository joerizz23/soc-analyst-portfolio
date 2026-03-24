# Incident Report: Impossible Travel Login

## Incident ID
SOC-003

## Alert Name
Impossible Travel Login Detected

## Date
March 2026

## Severity
Medium-High

## Status
Escalated

## Summary
A user account authenticated from two geographically distant locations within a short time frame. The travel time between the two locations is not feasible, indicating potential credential compromise or unauthorized access.

## Detection Source
Microsoft Sentinel / Azure AD Sign-in Logs (simulated)

## Investigation Steps

1. Reviewed login events for the affected user
2. Identified two successful login attempts from different countries
3. Compared timestamps of both authentication events
4. Determined travel between locations was not possible
5. Evaluated user behavior and login pattern
6. Checked for additional suspicious activity

## Evidence Observed

| Field | Value |
|------|------|
| Username | test.user |
| Login 1 Location | Atlanta, USA |
| Login 2 Location | Berlin, Germany |
| Time Between Logins | 12 minutes |
| Authentication Type | Successful |
| Device | Unknown |
| IP Address 1 | 104.22.xx.xx |
| IP Address 2 | 185.199.xx.xx |

## Analysis

The user authenticated successfully from Atlanta, USA and then from Berlin, Germany within 12 minutes. Travel between these locations in such a short time is not physically possible.

This behavior is consistent with:

- Credential compromise  
- Token theft  
- Session hijacking  
- VPN-based attacker access  

The login originated from an unknown device, increasing suspicion. No previous login history from Germany was observed for this user.

This alert indicates a potential unauthorized account access.

## MITRE ATT&CK Mapping

Technique: Valid Accounts  
Technique ID: T1078  
Tactic: Initial Access  

Additional Technique: Account Compromise  
Technique ID: T1098  

## Recommended Actions

- Force password reset for affected user
- Revoke active sessions
- Require multi-factor authentication
- Review user activity after login
- Check for mailbox access
- Investigate file access activity
- Block suspicious IP address

## Escalation Decision

Escalate to Tier 2. The impossible travel pattern strongly suggests credential compromise and requires further investigation into user activity, potential lateral movement, and persistence mechanisms.

## Lessons Learned

Impossible travel alerts are strong indicators of account compromise. Monitoring login geography and enforcing MFA are critical for preventing unauthorized access. Analysts should also verify device fingerprints and session tokens.
