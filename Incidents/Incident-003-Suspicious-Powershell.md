# Incident 003 - Suspicious PowerShell Execution

## Incident Overview

| Field | Details |
|---|---|
| Incident ID | INC-003 |
| Date | July 8, 2026 |
| Severity | Medium |
| Status | Closed |
| Host | DC01 |
| Domain | LAB.local |
| User | LAB\Administrator |
| Detection Source | Wazuh + Sysmon |

---

# Summary

Wazuh detected PowerShell activity containing command-line arguments commonly associated with malicious activity.

The detection was generated through Sysmon process creation monitoring and forwarded to Wazuh for analysis.

PowerShell is frequently abused by attackers for execution, reconnaissance, and payload delivery because it is a built-in Windows utility capable of running scripts and commands.

The activity was investigated to determine whether the PowerShell execution represented malicious behavior or authorized administrative activity.

---

# Detection Details

## Event Information

**Detection Source**

```
Wazuh
```

**Telemetry Source**

```
Microsoft Sysmon
```

**Event Type**

```
Sysmon Event ID 1 - Process Creation
```

---

## MITRE ATT&CK Mapping

| Technique | ID | Description |
|---|---|---|
| Command and Scripting Interpreter: PowerShell | T1059.001 | Attackers may use PowerShell to execute commands and scripts |

---

# Process Information

## Executed Process

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

---

## User Context

```
LAB\Administrator
```

The command was executed using an administrative account with elevated privileges.

---

## Command Line

```
powershell.exe -ExecutionPolicy Bypass -Command "..."
```

---

# Why This Was Investigated

The following indicators required investigation:

## Execution Policy Bypass

```
-ExecutionPolicy Bypass
```

PowerShell execution policy controls script execution restrictions.

Attackers commonly use the bypass option to avoid script execution restrictions during post-exploitation activity.

---

## Elevated Privileges

The process executed under:

```
LAB\Administrator
```

Administrative privileges increase the potential impact of malicious PowerShell activity.

---

# Investigation

The alert was investigated by reviewing:

- PowerShell command line arguments
- Executing user
- Parent process
- Sysmon event details
- File creation activity
- Host context

The activity was correlated with a controlled security simulation performed within the SOC home lab.

---

# Evidence

## Screenshot Evidence

### Wazuh PowerShell Detection

```
Evidence:
INC003-powershell-alert.png
```

The screenshot demonstrates:

- Sysmon Event ID 1 detection
- PowerShell process creation
- Command-line arguments
- Executing user

---

# Analysis

The PowerShell command contained characteristics commonly associated with attacker behavior, specifically the use of:

```
-ExecutionPolicy Bypass
```

However, additional context was reviewed before determining severity.

The investigation showed:

- The command originated from the known administrator account.
- The activity occurred on the controlled lab Domain Controller.
- No unknown users or remote sources were involved.
- No malicious payload was executed.

---

# Findings

| Indicator | Result |
|---|---|
| Suspicious PowerShell | Confirmed |
| Unauthorized User | No |
| External Source | No |
| Malicious File Created | No |
| Lab Simulation | Yes |

---

# Response Actions

Actions performed:

1. Reviewed Sysmon process creation logs.
2. Examined PowerShell command-line arguments.
3. Verified the user responsible for execution.
4. Confirmed activity was part of authorized testing.
5. Closed the alert as benign.

---

# Verdict

## Benign Activity - Authorized Security Testing

The alert represented expected activity generated during a controlled SOC lab exercise.

No remediation actions were required.

---

# Lessons Learned

This investigation demonstrated:

- Monitoring PowerShell activity using Sysmon.
- Reviewing command-line telemetry.
- Identifying suspicious execution patterns.
- Applying MITRE ATT&CK techniques.
- Performing SOC alert triage.
- Differentiating suspicious behavior from malicious activity.

---

# Future Improvements

Potential future enhancements:

- Configure additional Wazuh detection rules for suspicious PowerShell behavior.
- Monitor encoded PowerShell commands.
- Detect PowerShell downloads.
- Add correlation rules for repeated suspicious executions.
- Integrate threat intelligence enrichment.
