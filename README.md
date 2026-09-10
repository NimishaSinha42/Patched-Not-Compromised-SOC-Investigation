# Patched ≠ Not Compromised — SOC Investigation Lab

## Overview
This project is a Blue Team / SOC investigation lab based on the idea:

**“A vulnerability being patched does not automatically mean the system was never compromised.”**

The objective was to simulate suspicious activity, apply a patch event, and then investigate whether signs of compromise existed before patching.

## Objective
- Review authentication activity
- Analyze running processes
- Check CPU usage
- Identify suspicious files
- Review network activity
- Compare suspicious activity with patch timing
- Correlate multiple indicators
- Generate a risk verdict
- Create a Sigma detection rule

## Lab Environment
- Kali Linux
- Python 3
- Linux Journal Logs
- SSH
- Host-Only Network for normal login testing

## Case 1 — Suspicious Activity Before Patch
A controlled simulation was created using normal and suspicious log events.

Observed indicators included:
- Failed login attempts
- Successful privileged login
- Suspicious process: `suspicious-updater`
- Suspicious file: `/tmp/.soc-lab/update.sh`
- High CPU activity
- Unexpected service on port `8080`
- Security patch applied after suspicious activity

The automated SOC script detected multiple indicators and returned:

**Risk Level: HIGH**

## Case 2 — Normal Activity
A normal SSH login was performed from the Windows host to the Kali VM using a Host-Only network.

No suspicious process, file, or malicious activity was created.

The purpose of this case was to compare normal behavior with the suspicious scenario.

## Automated SOC Investigation Script
The Python script checks:

- Authentication logs
- Failed and privileged logins
- Patch timing
- Running processes
- CPU usage
- Suspicious files
- Listening network ports
- Risk score
- Final SOC verdict

Run the script using:

```bash
python3 soc_auto_check.py
