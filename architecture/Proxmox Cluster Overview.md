# Proxmox Cluster Overview

## Objective

The Proxmox cluster serves as the foundation of the homelab environment. It provides centralized virtualization, resource management, and the ability to host multiple services and operating systems.

## Hardware

### Primary Proxmox Host

* Hosts production virtual machines and containers
* Provides storage and compute resources

### Secondary Proxmox Host

* Used for workload distribution
* Supports future high-availability and migration testing

## Virtual Machines

| VM                  | Purpose                              |
| ------------------- | ------------------------------------ |
| Active Directory    | Identity and authentication services |
| Wazuh SIEM          | Security monitoring and log analysis |
| Windows Workstation | Endpoint monitoring and testing      |
| Linux Workstation   | Linux administration and testing     |

## Containers

| Container           | Purpose                     |
| ------------------- | --------------------------- |
| BookStack           | Documentation platform      |
| Jellyfin            | Media server                |
| Additional Services | Future projects and testing |
