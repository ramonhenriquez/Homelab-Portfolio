## Project Overview

This project integrates **Suricata IDS/IPS** with **Wazuh SIEM** to provide centralized monitoring, alerting, and threat analysis.

The goal is to simulate a Security Operations Center (SOC) environment where network activity and system events can be monitored from a single dashboard.

---

# Environment

## Infrastructure

| Component | Purpose |
|------------|----------|
| Proxmox VE | Hypervisor hosting virtual machines |
| Wazuh Server | SIEM platform |
| Suricata | Network IDS/IPS |
| Kali Linux | Security testing workstation |
| Active Directory | Authentication and user management |

---

# How It Works

## Suricata

Suricata monitors network traffic and looks for:

- Suspicious connections
- Network scans
- Malware traffic
- Protocol anomalies
- Intrusion attempts

## Wazuh

Wazuh collects and analyzes security events from systems and security tools.

Examples:

- Failed logins
- Successful logins
- File modifications
- Process execution
- Suricata alerts

# Integration Process

## 1. Install Suricata

Suricata was installed on the Wazuh server.

Verify service status:

```bash
sudo systemctl status suricata
```

---

## 2. Verify Suricata Logging

Confirm EVE JSON logging:

```bash
ls -lh /var/log/suricata
```

Expected file:

```text
eve.json
```

---

## 3. Configure Wazuh

Edit:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add:

```xml
<localfile>
  <log_format>json</log_format>
  <location>/var/log/suricata/eve.json</location>
</localfile>
```

---

## 4. Restart Wazuh

```bash
sudo systemctl restart wazuh-manager
```

Verify:

```bash
sudo systemctl status wazuh-manager
```

---

## 5. Confirm Integration

Search:

```bash
suricata
```

inside:

```text
Threat Intelligence → Threat Hunting → Events
```

If alerts appear, integration is successful.

---

# Testing Performed

## Test 1 – Network Traffic Detection

Traffic generated from Kali Linux.

Result:

- Suricata detected network events
- Events written to eve.json
- Wazuh ingested events successfully

Status:

✅ Successful

---

## Test 2 – Failed Authentication

### Scenario

The Wazuh server was locked.

Multiple incorrect passwords were intentionally entered.

### Purpose

Verify that Wazuh detects failed authentication attempts.

### Alerts Generated

Rule ID:

```text
2501
```

Description:

```text
syslog: User authentication failure
```

Rule Level:

```text
5
```

Additional Alert:

Rule ID:

```text
5557
```

Description:

```text
unix_chkpwd: Password check failed
```

---

# Alert Analysis

## What Happened?

The Linux authentication system received an incorrect password.

User:

```text
ramon
```

Result:

```text
Authentication Failed
```

---

## Why Is This Important?

Failed logins can indicate:

- Mistyped passwords
- Password guessing
- Brute force attacks
- Credential stuffing
- Unauthorized access attempts

---

## Investigation

Questions asked:

##### Was the login successful?

No.

##### Which user was targeted?

ramon

##### Was the activity expected?

Yes.

---

## Analyst Conclusion

Classification:

```text
Benign Test Activity
```

Reason:

```text
Authorized user intentionally generated failed logins
to verify SIEM detection capabilities.
```

Disposition:

```text
Closed
```
