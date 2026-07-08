# Lab Architecture

## Overview

This project simulates a small enterprise security operations center (SOC) environment designed for security monitoring, threat detection, and incident investigation.

The environment was built using VirtualBox and consists of a centralized Wazuh SIEM server monitoring a Windows Active Directory environment. Endpoint telemetry is collected using Sysmon and forwarded to Wazuh for analysis.

The goal of this lab is to practice real-world SOC analyst workflows including:

- Security event collection
- Alert monitoring
- Threat investigation
- MITRE ATT&CK technique mapping
- Incident documentation

---

# Network Architecture

```
                         Host Machine
                              |
                         VirtualBox
                              |
              Host-Only Network (192.168.56.0/24)
                              |
              --------------------------------
              |                              |
           WAZUH01                         DC01
        Ubuntu Server                 Windows Server 2022
        192.168.56.30                192.168.56.10
              |                              |
      Wazuh Manager                  Active Directory
      Wazuh Indexer                  Domain Controller
      Wazuh Dashboard                DNS Server
                                     Sysmon
                                     Wazuh Agent
```

---

# Systems

## WAZUH01

### Operating System

Ubuntu Server

### IP Address

```
192.168.56.30
```

### Role

Centralized security monitoring server.

### Installed Components

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- SSH remote administration

### Responsibilities

WAZUH01 is responsible for:

- Receiving security telemetry from endpoints
- Processing security events
- Applying detection rules
- Generating security alerts
- Providing centralized log analysis

---

# DC01

## Operating System

Windows Server 2022

## IP Address

```
192.168.56.10
```

## Domain

```
LAB.local
```

## Role

Active Directory Domain Controller and monitored endpoint.

## Installed Components

- Active Directory Domain Services
- DNS
- Wazuh Agent
- Sysmon

## Responsibilities

DC01 provides:

- User authentication
- Domain services
- Windows security events
- Endpoint telemetry
- Attack simulation environment

---

# Security Monitoring Stack

## Wazuh

### Purpose

Wazuh acts as the SIEM platform for collecting, analyzing, and alerting on security events.

### Capabilities Used

- Windows event log collection
- Sysmon event monitoring
- Alert generation
- Security rule analysis
- MITRE ATT&CK mapping

---

## Sysmon

### Purpose

Sysmon provides detailed endpoint telemetry that is not available through standard Windows logging.

### Events Monitored

Examples include:

| Event ID | Description |
|----------|-------------|
| 1 | Process Creation |
| 7 | Image Loaded |
| 10 | Process Access |
| 11 | File Created |
| 13 | Registry Modification |

### Data Collected

- Process execution
- Command line arguments
- File creation
- Registry changes
- Process relationships
- Hash values

---

# Data Flow

The security monitoring workflow operates as follows:

```
1. User activity occurs on DC01

              ↓

2. Sysmon records endpoint activity

              ↓

3. Wazuh Agent collects Windows/Sysmon events

              ↓

4. Events are forwarded to WAZUH01

              ↓

5. Wazuh Manager analyzes events

              ↓

6. Detection rules generate alerts

              ↓

7. Alerts are investigated and documented
```

---

# Network Configuration

## Virtual Network

VirtualBox Host-Only Network

```
Network:
192.168.56.0/24
```

## Hosts

| Hostname | IP Address | Purpose |
|----------|------------|---------|
| WAZUH01 | 192.168.56.30 | SIEM Server |
| DC01 | 192.168.56.10 | Domain Controller |

---

# Lab Objectives

This environment was created to practice:

- Security monitoring using a SIEM
- Windows event analysis
- Endpoint detection concepts
- Active Directory security monitoring
- Attack simulation
- Incident response documentation

---

# Current Detection Capabilities

The lab currently detects:

- PowerShell execution
- Process creation
- File creation events
- Windows authentication events
- Security-related endpoint activity

Future improvements include:

- Brute force detection
- Account creation monitoring
- Persistence technique detection
- Additional MITRE ATT&CK simulations
