# Lab Environment

## Overview

This lab simulates a small enterprise environment consisting of a Security Information and Event Management (SIEM) server and a Windows Active Directory domain environment.

## Systems

| Hostname | Operating System | Role | IP Address |
|---|---|---|---|
| WAZUH01 | Ubuntu Server | Wazuh SIEM Manager | 192.168.56.30 |
| DC01 | Windows Server 2022 | Active Directory Domain Controller | 192.168.56.10 |

## Domain

- Domain Name: LAB.local
- Domain Controller: DC01

## Security Tools

### Wazuh
Purpose:
- Centralized security monitoring
- Alert generation
- Log analysis

### Sysmon
Purpose:
- Endpoint telemetry collection
- Process monitoring
- File and registry activity tracking

## Network

The environment uses a VirtualBox isolated lab network to allow communication between systems while keeping the environment separated from the host network.
