# Alert Investigation Report — SSH Brute Force

## Alert Summary

| Field | Details |
|---|---|
| Date | July 20, 2026 |
| Time | 11:55 UTC |
| Severity | Level 10 |
| Agent | wazuh-server (000) |
| Source IP | 192.168.1.100 (Ubuntu Desktop) |
| Target | 192.168.1.50 (Ubuntu Server) |
| Attack type | SSH Brute Force |

## Alerts Triggered

| Rule | Level | Description | MITRE |
|---|---|---|---|
| 5710 | 5 | SSH login attempt non-existent user | T1110.001 |
| 5503 | 5 | PAM authentication failure | T1110.001 |
| 2502 | 10 | Multiple password failures | T1110 |

## Investigation Steps

### Step 1 — Alert Triage
Multiple SSH authentication failures detected
from 192.168.1.100 targeting 192.168.1.50.
Pattern consistent with brute force attack
(multiple attempts in short timeframe).

### Step 2 — Source Analysis
Source IP 192.168.1.100 is Ubuntu Desktop VM
on internal LabNet. In a real environment
this would indicate insider threat or
compromised internal machine.

### Step 3 — MITRE ATT&CK Mapping
Tactic: Credential Access
Technique: T1110 — Brute Force
Sub-tech: T1110.001 — Password Guessing
Also seen: T1021.004 — SSH (Lateral Movement)

### Step 4 — Verdict
CONFIRMED ATTACK — SSH brute force simulation
successfully detected by Wazuh SIEM.

### Step 5 — Recommended Response
1. Block source IP at firewall level
2. Implement SSH key-based auth only
3. Disable password authentication in SSH
4. Add fail2ban for automatic IP blocking
5. Alert SOC team for investigation

## Lessons Learned
This simulation confirmed Wazuh correctly
detects SSH brute force attempts using
built-in rules 5710, 5503, and 2502 with
accurate MITRE ATT&CK mapping.

Add SSH brute force alert investigation report
