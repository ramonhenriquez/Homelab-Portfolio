# Service Map

## Overview

This document describes the primary services running within the homelab environment and how they interact.

## Infrastructure Layer

### Proxmox

Hosts all virtual machines and containers.

## Identity Layer

### Active Directory

Provides:

* User authentication
* Group Policy management
* Centralized administration

## Security Layer

### Wazuh SIEM

Collects and analyzes:

* Authentication events
* System logs
* Security alerts
* Endpoint activity

### Suricata IDS

Monitors network traffic and generates security events that are forwarded to Wazuh.

## Documentation Layer

### BookStack

Used to document:

* Projects
* Procedures
* Configurations
* Troubleshooting steps

## Media Layer

### Jellyfin

Provides centralized media streaming services.

## AI Layer

### Odysseus AI

Dedicated environment for:

* Local AI experimentation
* LLM testing
* Self-hosted AI services

## Endpoint Systems

### Fedora Laptop

* Wazuh agent installed
* VPN-enabled remote access
* Linux administration workstation

### Windows Workstation

* Active Directory joined
* Wazuh agent installed
* Security monitoring endpoint

### Kali Linux

Used for:

* Security testing
* Network analysis
* Validation of SIEM detections
