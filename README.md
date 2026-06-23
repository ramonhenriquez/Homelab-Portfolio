# Active Directory Homelab Project

## Installing and Configuring Active Directory Domain Services on Windows Server 2025

### Project Overview

This project documents the deployment of a Windows Server 2025 Domain Controller within a Proxmox homelab environment. The goal is to create a centralized identity management system using Active Directory Domain Services (AD DS), providing authentication, authorization, DNS services, Group Policy management, and a foundation for future cybersecurity and system administration projects.

---

# Objectives

* Deploy Windows Server 2025 as a Domain Controller
* Install Active Directory Domain Services (AD DS)
* Create a new Active Directory Forest
* Configure DNS services
* Prepare the environment for:

  * Group Policy Management
  * User and Computer Administration
  * Windows Domain Joining
  * Security Monitoring (Wazuh)
  * Remote Management (Tactical RMM)

---

# Environment

| Component   | Details                                 |
| ----------- | --------------------------------------- |
| Hypervisor  | Proxmox VE 9                            |
| Guest OS    | Windows Server 2025 Standard Evaluation |
| Server Name | DC01                                    |
| Role        | Domain Controller                       |
| Domain      | homelab.local                           |
| DNS         | Integrated with Active Directory        |

---

# Prerequisites

Before installing Active Directory:

* Windows Server 2025 installed
* Administrative privileges available
* Static IP address configured
* Server hostname configured

Example:

Hostname:

```text
DC01
```

Domain:

```text
homelab.local
```

---

# Step 1 – Configure a Static IP Address

### Why?

Domain Controllers should always use a static IP address to ensure reliable DNS and authentication services.

### Procedure

1. Open Server Manager.
2. Select Local Server.
3. Click the network adapter link.
4. Open adapter properties.
5. Select Internet Protocol Version 4 (TCP/IPv4).
6. Configure a static IP.

Example:

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
Preferred DNS: 192.168.1.10
```

### Validation

Open Command Prompt:

```powershell
ipconfig
```

Verify the assigned IP address.

---

# Step 2 – Rename the Server

### Why?

Using descriptive hostnames simplifies administration and troubleshooting.

### Procedure

1. Open Server Manager.
2. Select Local Server.
3. Click the current computer name.
4. Select Change.
5. Rename the server:

```text
DC01
```

6. Reboot the server.

### Validation

Open PowerShell:

```powershell
hostname
```

Expected output:

```text
DC01
```

---

# Step 3 – Install Active Directory Domain Services

### Procedure

1. Open Server Manager.
2. Select Add Roles and Features.
3. Click Next until reaching Server Roles.
4. Check:

```text
Active Directory Domain Services
```

5. Select Add Features.
6. Continue through the wizard.
7. Click Install.

### Expected Result

Installation completes successfully and displays:

```text
Configuration required.
Installation succeeded on DC01.
```

---

# Step 4 – Promote the Server to a Domain Controller

### Procedure

1. Open Server Manager.
2. Click the Notifications flag.
3. Select:

```text
Promote this server to a domain controller
```

4. Choose:

```text
Add a new forest
```

5. Enter:

```text
homelab.local
```

### Domain Controller Options

Enable:

```text
DNS Server
Global Catalog (GC)
```

Create and store a DSRM password securely.

### DNS Options

A DNS Delegation warning may appear.

This can safely be ignored in a homelab environment.

---

# Step 5 – Configure Active Directory Settings

### NetBIOS Name

The wizard automatically generates:

```text
HOMELAB
```

Accept the default.

### Database Paths

Leave the default locations:

```text
Database: C:\Windows\NTDS
Logs: C:\Windows\NTDS
SYSVOL: C:\Windows\SYSVOL
```

### Install

Review the configuration and click:

```text
Install
```

The server will automatically reboot.

---

# Step 6 – Verify Active Directory Deployment

### Login

After reboot:

```text
HOMELAB\Administrator
```

or

```text
administrator@homelab.local
```

### Verify Installed Tools

Open:

```text
Server Manager → Tools
```

Confirm the following tools are available:

* Active Directory Users and Computers
* Active Directory Administrative Center
* DNS Manager
* Group Policy Management
* Active Directory Sites and Services
