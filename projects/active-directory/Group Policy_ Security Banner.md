# Group Policy Deployment: Security Login Banner

## Project Overview

This project demonstrates the creation, deployment, and validation of a Windows Active Directory Group Policy Object (GPO) used to display a security warning banner before user logon.

Security banners are commonly implemented in enterprise, government, healthcare, and educational environments to notify users that systems are monitored and that unauthorized access is prohibited.

---

# Objectives

* Create a custom Group Policy Object (GPO)
* Configure an Interactive Logon Security Banner
* Deploy the policy to all domain-joined systems
* Verify successful Group Policy application
* Gain hands-on experience with Active Directory Group Policy Management

---

# Environment

| Component       | Details                                |
| --------------- | -------------------------------------- |
| Hypervisor      | Proxmox VE 9                           |
| Server OS       | Windows Server 2025                    |
| Role            | Domain Controller                      |
| Domain          | homelab.local                          |
| GPO Name        | Login Banner                           |
| Management Tool | Group Policy Management Console (GPMC) |

---

# Business Purpose

Organizations often require users to acknowledge acceptable use policies and monitoring notices before accessing systems.

Common reasons include:

* Legal compliance
* Security awareness
* Insider threat deterrence
* Unauthorized access warnings
* Audit and regulatory requirements

Examples of environments using login banners:

* Government agencies
* Courts and law enforcement
* Healthcare organizations
* Financial institutions
* Enterprise environments

---

# Creating the Group Policy Object

## Step 1: Open Group Policy Management

Navigate to:

```text
Server Manager
→ Tools
→ Group Policy Management
```

---

## Step 2: Create the GPO

Navigate to:

```text
Forest
└── Domains
    └── homelab.local
```

Right-click:

```text
homelab.local
```

Select:

```text
Create a GPO in this domain, and Link it here...
```

Name:

```text
Login Banner
```

---

# Configuring the Login Banner

## Step 1: Edit the GPO

Right-click:

```text
Login Banner
```

Select:

```text
Edit
```

Navigate to:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── Security Options
```

---

## Step 2: Configure Banner Title

Policy:

```text
Interactive logon: Message title for users attempting to log on
```

Value:

```text
Authorized Access Only
```

---

## Step 3: Configure Banner Message

Policy:

```text
Interactive logon: Message text for users attempting to log on
```

Value:

```text
This system is the property of Ramon's Homelab.

Unauthorized access is prohibited.

All activity may be monitored and logged.
```

---

# Linking the GPO

The Login Banner GPO was linked at the domain level:

```text
homelab.local
```

Result:

```text
Login Banner
Link Enabled: Yes
```

This configuration ensures the policy applies to all domain-joined systems within the domain.

---

# Applying the Policy

Open an elevated Command Prompt:

```cmd
gpupdate /force
```

Expected Output:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

---

# Validation

## Verify Applied Policies

Run:

```cmd
gpresult /r
```

Verify the following appears under Applied Group Policy Objects:

```text
Login Banner
```

---

## Test User Experience

Lock the workstation:

```text
Ctrl + Alt + Del
→ Lock
```

or sign out of Windows.

Before logon, the user receives the configured security banner and must acknowledge the message before continuing.

---

# Screenshots

## Screenshot 1

Group Policy Management Console showing:

```text
Login Banner GPO
Linked to homelab.local
```

Filename:

```text
gpo-login-banner-linked.png
```
---
