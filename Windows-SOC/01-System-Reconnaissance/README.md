# Lab 01: Windows System Reconnaissance and Initial Triage

## Objective
Establish an operational security baseline of a target Windows host using native command-line and PowerShell utilities to gather system intelligence during initial triage.

## Environment
* **OS:** Windows 11 Pro (Build 26100)
* **Host Model:** HP ProBook 430 G6
* **Shell:** Windows PowerShell
* **Lab Type:** SOC / Blue Team Triage

---

## SOC Investigation Log

### 1. Identity Verification (`whoami`)
* **Command:** `whoami`
* **Observation:** Active session context running under local account `timot`.
* **SOC Relevance:** Establishes initial user context to attribute process execution and file modifications during incident triage.

### 2. Group Membership & Integrity Level (`whoami /groups`)
* **Command:** `whoami /groups`
* **Observation:** Session running at Medium Integrity Level due to UAC.
* **SOC Relevance:** Identifies execution privileges to determine if privilege escalation is needed to collect restricted artifacts.

### 3. Host Identifier (`hostname`)
* **Command:** `hostname`
* **Observation:** Endpoint network identifier set to `T`.
* **SOC Relevance:** Coordinates endpoint logs with network streams and SIEM alerts.

### 4. Host Architecture & Network Profile (`systeminfo`)
* **Command:** `systeminfo`
* **Observation:** Windows 11 Pro, WORKGROUP environment, 5 hotfixes installed, active Wi-Fi and VMware virtual adapters.
* **SOC Relevance:** Uncovers patch baseline, virtualization capabilities, and active network interfaces.

### 5. Local Account Enumeration (`Get-LocalUser`)
* **Command:** `Get-LocalUser`
* **Observation:** Built-in accounts disabled; `timot` is the sole active user.
* **SOC Relevance:** Uncovers potential unauthorized local user account creation or persistence mechanisms.

---

## Command Evidence

### Identity and Group Enumeration
![Whoami Output](screenshots/whoami.png)

![Groups Output](screenshots/groups.png)

### System Details and Local Users
![System Info Output](screenshots/systeminfo.png)

![Local Users Output](screenshots/users.png)# Lab 01: Windows System Reconnaissance and Initial Triage

## Objective
Establish an operational security baseline of a target Windows host using native command-line and PowerShell utilities to gather system intelligence during initial triage.

## Environment
* **OS:** Windows 11 Pro (Build 26100)
* **Host Model:** HP ProBook 430 G6
* **Shell:** Windows PowerShell
* **Lab Type:** SOC / Blue Team Triage

---

## SOC Investigation Log

### 1. Identity Verification (`whoami`)
* **Command:** `whoami`
* **Observation:** Active session context running under local account `timot`.
* **SOC Relevance:** Establishes initial user context to attribute process execution and file modifications during incident triage.

### 2. Group Membership & Integrity Level (`whoami /groups`)
* **Command:** `whoami /groups`
* **Observation:** Session running at Medium Integrity Level due to UAC.
* **SOC Relevance:** Identifies execution privileges to determine if privilege escalation is needed to collect restricted artifacts.

### 3. Host Identifier (`hostname`)
* **Command:** `hostname`
* **Observation:** Endpoint network identifier set to `T`.
* **SOC Relevance:** Coordinates endpoint logs with network streams and SIEM alerts.

### 4. Host Architecture & Network Profile (`systeminfo`)
* **Command:** `systeminfo`
* **Observation:** Windows 11 Pro, WORKGROUP environment, 5 hotfixes installed, active Wi-Fi and VMware virtual adapters.
* **SOC Relevance:** Uncovers patch baseline, virtualization capabilities, and active network interfaces.

### 5. Local Account Enumeration (`Get-LocalUser`)
* **Command:** `Get-LocalUser`
* **Observation:** Built-in accounts disabled; `timot` is the sole active user.
* **SOC Relevance:** Uncovers potential unauthorized local user account creation or persistence mechanisms.

---

## Command Evidence

### Identity and Group Enumeration
![Whoami Output](screenshots/whoami.png)

![Groups Output](screenshots/groups.png)

### System Details and Local Users
![System Info Output](screenshots/systeminfo.png)

![Local Users Output](screenshots/users.png)
