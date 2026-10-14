# Mini-SOC Lab - Week 1

## Project Overview

This project implements an isolated Mini Security Operations Center (SOC) using Wazuh SIEM, Docker, Linux, Windows, and Sysmon.

The objective is to collect endpoint telemetry, detect security events, and investigate alerts through a centralized dashboard.

## Lab Architecture

| Machine | Role | IP Address | Network |
|---|---|---|---|
| siem-host | Wazuh SIEM Server | 192.168.174.10 | NAT + Host-only |
| ubuntu-web | Linux Endpoint / Apache | 192.168.174.20 | Host-only |
| win-client | Windows Endpoint / Sysmon | 192.168.174.30 | Host-only |

Hypervisor: VMware Workstation

Wazuh Version: 4.14.8

## Wazuh Components

- Wazuh Manager - Receives and analyzes endpoint events.
- Wazuh Indexer - Stores and indexes security alerts.
- Wazuh Dashboard - Provides an interface for monitoring and investigation.
- Wazuh Agents - Collect security telemetry from endpoints.

## Docker Memory Usage

Idle measurements:

| Container | Memory Usage |
|---|---|
| Wazuh Manager | 1.02 GiB |
| Wazuh Indexer | 1.459 GiB |
| Wazuh Dashboard | 208.8 MiB |

## Starting the Lab

1. Start the siem-host virtual machine.
2. Verify that Docker is running.
3. Start the Wazuh stack if it is not already running.
4. Start ubuntu-web and win-client.
5. Verify that both Wazuh agents are Active.
6. Open the Wazuh Dashboard at https://192.168.174.10.

Commands on siem-host:

```bash
cd ~/wazuh-docker/single-node
sudo docker compose up -d
sudo docker compose ps
```

## Stopping the Lab

1. Shut down win-client.
2. Shut down ubuntu-web.
3. Stop the Wazuh containers on siem-host.
4. Shut down siem-host.

```bash
cd ~/wazuh-docker/single-node
sudo docker compose stop
sudo poweroff
```

## Security Events Verified

1. Failed SSH Login
2. Sudo Command Execution
3. Linux User Creation
4. Windows Process Creation
5. Failed Windows Login

Supporting screenshots are stored in the evidence/ directory.

## Persistence Testing

Docker containers were stopped and restarted. The SIEM host was also rebooted.

Both Wazuh agents reconnected successfully, and previously generated alerts remained available.

## Security Considerations

- All endpoints use an isolated Host-only network.
- Only siem-host has a permanent NAT interface.
- Default Wazuh administrator credentials were changed.
- Passwords, private keys, and certificates are excluded from version control.
- HTTPS is used for accessing the Wazuh Dashboard with a lab-generated certificate.
-The HTTPS certificate warning appears because the Wazuh Dashboard uses a self-signed or lab-generated certificate that the browser does not trust by default.
