# Incident 001 - PowerShell Execution Detection

## Incident Overview

| Field | Details |
|---|---|
| Incident ID | INC-001 |
| Date | July 8, 2026 |
| Severity | Low |
| Status | Closed |
| Host | DC01 |
| User | LAB\Administrator |
| Detection Source | Wazuh + Sysmon |

---

# Summary

Wazuh detected PowerShell execution activity on the Windows Domain Controller (DC01).

The event was generated through Sysmon Event ID 1 (Process Creation), which records the creation of new processes and provides additional telemetry such as command line arguments, parent processes, user context, and hashes.

---

# Detection Details

## Event Information

**Detection:**

PowerShell execution

**MITRE ATT&CK Technique:**

T1059.001 - PowerShell

**Source:**

Sysmon Event ID 1

**Process:**

```
powershell.exe
```

**Command Line:**

```
powershell.exe -ExecutionPolicy Bypass -Command Get-Process
```

**User:**

```
LAB\Administrator
```

---

# Investigation

The alert was investigated by reviewing:

- Process creation details
- Executed command
- User context
- Parent process
- Hash information
- Associated Sysmon events

The command executed was:

```
Get-Process
```

This command retrieves currently running processes from the Windows system.

The activity was performed by the authorized domain administrator account during security testing of the monitoring environment.

---

# Analysis

Although PowerShell is frequently used by attackers for execution and post-exploitation activity, the observed behavior did not contain indicators of malicious activity.

Observed characteristics:

- Executed by authorized administrator account
- Command was a standard Windows administration command
- No suspicious download activity observed
- No persistence mechanisms identified
- No malicious files created

---

# Verdict

## Benign Activity

The alert was classified as expected administrative activity.

No further remediation was required.

---

# Lessons Learned

This investigation demonstrated:

- How Sysmon captures PowerShell activity
- How Wazuh receives endpoint telemetry
- How to investigate process execution alerts
- The importance of analyzing context before determining maliciousness

PowerShell alerts require investigation because legitimate administrators and attackers both commonly use PowerShell.
