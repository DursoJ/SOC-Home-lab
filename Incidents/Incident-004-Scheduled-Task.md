# Incident 03 - Scheduled Task Persistence Detection

## Overview

This incident demonstrates detection of scheduled task creation activity using Sysmon telemetry collected by Wazuh.

Scheduled tasks are commonly abused by attackers to establish persistence by automatically executing malicious programs at startup, login, or scheduled intervals.

MITRE ATT&CK Technique:

- T1053 - Scheduled Task/Job

---

# Lab Environment

Affected Host:

- DC01.lab.local

Operating System:

- Windows Server 2022

Monitoring:

- Wazuh SIEM
- Sysmon
- Windows Event Logs

---

# Attack Simulation

A scheduled task was created on the domain controller to simulate attacker persistence behavior.

Command executed:
