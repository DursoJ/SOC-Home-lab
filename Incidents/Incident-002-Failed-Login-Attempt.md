# Incident 002 - Failed Login Attempt Detection

## Incident Overview

| Field | Details |
|---|---|
| Incident ID | INC-002 |
| Date | July 8, 2026 |
| Severity | Low |
| Status | Closed |
| Host | DC01 |
| Domain | LAB.local |
| Target Account | LAB\Administrator |
| Detection Source | Wazuh + Windows Security Logs |

---

# Summary

Wazuh detected multiple failed authentication attempts against the Administrator account on the Windows Domain Controller (DC01).

The detection was generated from Windows Security Event ID 4625, which records failed logon attempts. This event is commonly investigated during potential brute-force attacks, password spraying attempts, or unauthorized access attempts.

The activity was generated as part of a controlled security simulation to verify authentication monitoring capabilities within the SOC lab environment.

---

# Detection Details

## Event Information

**Event ID**

```
4625
```

**Event Description**

```
An account failed to log on.
```

**Provider**

```
Microsoft-Windows-Security-Auditing
```

**Computer**

```
DC01.lab.local
```

---

# Event Data

## Target Account

```
Username:
Administrator

Domain:
LAB
```

---

## Failure Information

```
Failure Reason:
Unknown user name or bad password.
```

```
Status:
0xC000006D
```

```
Sub Status:
0xC000006A
```

The authentication attempt failed because an incorrect password was provided.

---

## Logon Information

```
Logon Type:
7
```

Logon Type 7 represents an unlock attempt.

The failed authentication occurred after locking the workstation and attempting to unlock it using an incorrect password.

---

## Source Information

```
Source Address:
127.0.0.1
```

```
Workstation:
DC01
```

The authentication attempt originated locally from the Domain Controller rather than a remote system.

---

## Authentication Details

```
Authentication Package:
Negotiate
```

```
Logon Process:
User32
```

```
Process:
C:\Windows\System32\svchost.exe
```

These values are consistent with normal Windows authentication behavior.

---

# Investigation

The alert was investigated by reviewing the following information:

- Windows Security Event ID
- Target account
- Source address
- Logon type
- Failure reason
- Authentication process
- Frequency of attempts

The failed login attempts were correlated with a controlled security test performed against the DC01 system.

Multiple incorrect passwords were entered intentionally to verify that authentication failures were collected by the Wazuh monitoring system.

---

# Analysis

## Indicators Reviewed

| Indicator | Finding |
|---|---|
| Target Account | Administrator account |
| Source IP | 127.0.0.1 |
| Logon Type | 7 (Unlock) |
| Authentication Package | Negotiate |
| Failure Reason | Incorrect password |
| Source Host | DC01 |

---

## Findings

The activity did not contain indicators of malicious behavior.

Reasons:

- Authentication attempts originated locally from DC01.
- The targeted account was the known administrator account.
- The event occurred during authorized security testing.
- No external source IP address was identified.
- No account compromise indicators were observed.

---

# MITRE ATT&CK Mapping

| Technique | ID | Description |
|---|---|---|
| Brute Force | T1110 | Attempts to gain access by guessing credentials |

Although this event maps to a brute-force technique, additional context is required before determining whether activity is malicious.

---

# Response Actions

Actions taken:

- Reviewed authentication failure events.
- Confirmed activity was generated during a controlled test.
- Verified Wazuh successfully collected Windows Security logs.
- Classified the alert as benign.

---

# Verdict

## Benign Activity

The alert was classified as expected administrative testing activity.

No remediation actions were required.

---

# Lessons Learned

This investigation demonstrated:

- How Windows Security Event Logs are collected by Wazuh.
- How failed authentication events are analyzed.
- How logon type provides important investigation context.
- How security analysts differentiate malicious behavior from normal activity.
- The importance of documenting findings after investigating alerts.

---

# Future Improvements

Future tests for this detection capability include:

- Simulating remote failed login attempts.
- Testing multiple usernames.
- Creating password spraying scenarios.
- Developing Wazuh correlation rules for repeated failures.
