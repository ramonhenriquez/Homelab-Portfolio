## Objective

Deploy a Wazuh agent to a remote Fedora workstation connected to the homelab through OpenVPN and verify security telemetry collection.

## Environment

* Wazuh Manager: Ubuntu Server VM
* Agent: Fedora Workstation
* VPN: UniFi OpenVPN
* SIEM: Wazuh
* IDS: Suricata

## Validation Tests

### VPN Authentication

Detected successful OpenVPN connection from remote workstation.

Observed:

* Source IP address
* Source port
* VPN authentication event
* Connection timestamp

### Privilege Escalation Monitoring

Executed sudo commands on Fedora.

Detected:

* PAM Login Session Opened
* User account performing elevation
* Root privilege assignment
* Timestamp of elevation

### Results

Successfully confirmed:

* Agent registration
* Remote log collection
* VPN event monitoring
* Authentication monitoring
* Privilege escalation monitoring

## Lessons Learned

Wazuh can monitor both user activity and system activity across remote endpoints connected through VPN tunnels. Authentication events, VPN logins, and administrative actions are centrally collected and searchable from the Wazuh dashboard.

## Status

Operational.
Ready for threat simulation and investigation exercises.
