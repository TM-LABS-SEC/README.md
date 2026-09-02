# Lab 02: Windows User Account and Privilege Context Audit

## Objective
Audit local user accounts, evaluate group membership vectors, and analyze active access token privileges using native Windows utilities to establish an endpoint security baseline and evaluate privilege escalation risks.

## Purpose
User accounts and rights assignments represent critical attack surfaces on Windows endpoints. Adversaries compromising an initial footprint routinely attempt token manipulation or abuse assignment rights to escalate privileges or establish persistence.

This lab evaluates account states, group memberships, and security privileges in a non-elevated user context.

## Environment
* **OS:** Windows 11 Pro (Build 26100)
* **Architecture:** x64 Workstation
* **Shell:** Windows PowerShell (Non-Elevated Context)
* **Lab Type:** SOC / Blue Team Triage

---

## SOC Investigation Log

### 1. Session Identity Audit (`whoami`)
* **Command:** `whoami`
* **Observation:** Active session identity resolved to local domain context `[REDACTED_HOST]\[REDACTED_USER]`.
* **SOC Relevance:** Establishes session attribution for log correlation across local Security Event logs (Event ID 4624) and SIEM pipelines.

### 2. Security Privilege & Access Token Analysis (`whoami /priv`)
* **Command:** `whoami /priv`
* **Observation:** Execution yielded 5 basic user privileges (`SeShutdownPrivilege`, `SeChangeNotifyPrivilege`, `SeUndockPrivilege`, `SeIncreaseWorkingSetPrivilege`, `SeTimeZonePrivilege`). Only `SeChangeNotifyPrivilege` was set to `Enabled`. High-risk rights (`SeDebugPrivilege`, `SeImpersonatePrivilege`, `SeRestorePrivilege`) were completely absent.
* **SOC Relevance:** Verifies UAC restricted-token enforcement. The absence of high-risk rights confirms that adversaries executing code within this session context cannot perform LSASS memory dumping or token theft without invoking a UAC bypass or exploit.

---

## Command Evidence

| Investigation Stage | SOC Security Relevance |
| :--- | :--- |
| **01. Session Identity**| Baseline user context identification |
| **02. Privilege Token Audit** | Access token privilege & UAC enforcement check |

---

## Security Analysis & Findings

1. **Least Privilege Compliance:** The current session operates under a restricted Medium Integrity access token. Standard administrative rights are filtered out by UAC.
2. **Exploitation Surface:** The environment is protected against immediate privilege abuse vectors; high-risk rights commonly targeted by post-exploitation frameworks (such as Potato exploits leveraging `SeImpersonatePrivilege`) are unavailable in this session state.

## Limitations
This investigation provides a point-in-time assessment of local user token privileges. It does not inspect domain-level Group Policy Objects (GPO) or detect memory-resident process injection that bypasses native token listing utilities.q
