# Custom Detection Rules Documentation

## Overview
Three custom rules written for Project 2 lab
to detect common attack patterns.

## Rule 100001 — Port Scan Detection

| Field | Value |
|---|---|
| Rule ID | 100001 |
| Level | 10 (High) |
| MITRE | T1046 — Network Service Discovery |
| Tactic | Discovery |
| Trigger | Port scan signature detected |

**Why this rule exists:**
Port scanning is always the first step
in an attack. Attackers use tools like Nmap
to discover open services before exploiting
them. Detecting scans early gives defenders
time to respond before the actual attack.

---

## Rule 100002 — Brute Force Detection

| Field | Value |
|---|---|
| Rule ID | 100002 |
| Level | 12 (Critical) |
| MITRE | T1110 — Brute Force |
| Tactic | Credential Access |
| Trigger | 3+ auth failures in 120 seconds |

**Why this rule exists:**
A single failed login is normal. Three
failures in two minutes indicates automated
password guessing. Level 12 ensures SOC
analysts are immediately notified.

---

## Rule 100003 — SSH Brute Force Detection

| Field | Value |
|---|---|
| Rule ID | 100003 |
| Level | 12 (Critical) |
| MITRE | T1110 — Brute Force |
| Tactic | Credential Access |
| Trigger | 3+ SSH failures same IP in 120 seconds |

**Why this rule exists:**
SSH on port 22 is the most attacked service
on Linux servers. Attackers constantly try
default credentials. Same source IP check
prevents false positives from multiple
legitimate users having issues simultaneously.

---

## Detection Engineering Lessons

**if_matched_sid vs if_matched_group:**
- if_matched_sid watches ONE specific rule
- if_matched_group watches ALL rules in a group
- Group-based matching provides broader coverage
- This is a key detection engineering concept

**Frequency and timeframe tuning:**
- Too sensitive = alert fatigue
- Too loose = miss real attacks
- 3 failures in 120 seconds = balanced for lab
- Production environments tune based on baseline

Add custom detection rules documentation
with MITRE ATT&CK mapping and engineering notes
