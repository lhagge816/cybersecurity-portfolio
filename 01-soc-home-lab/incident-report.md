# Incident Report #1 — SSH Brute-Force Detection

A Wazuh SIEM detected and correlated an SSH brute-force attack against the lab server. Access was never granted — a true positive with no breach.

## Alert

| Field | Value |
| --- | --- |
| Date / time | ~17:42–17:44 (lab time) |
| Primary detection | Wazuh rule 5712 (level 10) — "sshd: brute force trying to get access to the system" |
| Supporting alerts | Wazuh rule 5710 (level 5) — "attempt to log in using a non-existent user" |
| Source IP | 192.168.64.2 |
| Target account | `hacker` (non-existent user) |
| Volume | ~9 failed logins across 3 sessions in ~2 minutes |
| MITRE ATT&CK | T1110 — Brute Force |
| Outcome | Failed — no successful login |

## Analysis
Repeated failed logins from a single source against an account that does not exist is a classic brute-force / credential-guessing pattern. Each attempt fired rule 5710 (level 5, low). Wazuh's correlation engine saw the burst stack up from one source in a short window and escalated it to rule 5712 — a single level-10 (high-severity) brute-force alert. No successful-login event followed, so the attempt did not succeed.

## Verdict
True positive — a genuine brute-force attempt. No compromise; access was never granted.

## Response
1. Block the source IP at the host or perimeter firewall.
2. Confirm the targeted account does not exist and that no users or SSH keys were added.
3. Enforce key-based SSH authentication, disable password login, and add rate-limiting (e.g. fail2ban).
4. In production, escalate if the source is external or recurring and add it to a watchlist.
