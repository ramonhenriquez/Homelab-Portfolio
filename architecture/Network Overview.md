# Network Overview

## Objective

The homelab network is designed to simulate a small enterprise environment while providing secure access to services and administrative systems.

## Core Components

### Internet Connection

Provides external connectivity to the homelab environment.

### UniFi Gateway

Responsible for:

* Routing
* Firewall policies
* VPN access
* Network management

### VPN Access

Remote devices can securely connect to the home network using OpenVPN.

Examples:

* Fedora laptop
* Mobile devices
* Remote administration systems

## Internal Services

| Service          | Function            |
| ---------------- | ------------------- |
| Active Directory | Authentication      |
| Wazuh SIEM       | Security monitoring |
| BookStack        | Documentation       |
| Jellyfin         | Media services      |
| Odysseus AI      | AI experimentation  |

## Security Features

* VPN access
* Firewall policies
* Endpoint monitoring
* Security event logging
* IDS integration with Suricata
