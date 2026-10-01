# SOC Home Lab — Wazuh SIEM

Built and operated a Security Operations Center in a home lab: a live **Wazuh SIEM** that detects simulated attacks, with a Tier-1 incident report for each investigation.

## What I built
- Self-hosted Wazuh (indexer + manager + dashboard) on an Ubuntu VM
- Enrolled a live endpoint agent reporting into the manager
- Generated attack telemetry and verified detection end to end

## Highlight: SSH brute-force detection
Simulated an SSH brute-force attack (**MITRE ATT&CK T1110**). Wazuh correlated the individual failed logins into a single high-severity **level-10 alert (rule 5712)** — turning a stream of low-level noise into one actionable signal. Confirmed there was no successful login afterward (true positive, no breach).

## Skills
Wazuh SIEM · log analysis · detection engineering · MITRE ATT&CK · incident response

## Files
- [`incident-report.md`](./incident-report.md) — Tier-1 incident report for the brute-force detection

> **Tip:** add your own screenshots of the Wazuh dashboard and the brute-force alerts to this folder — visual evidence makes the project land.
