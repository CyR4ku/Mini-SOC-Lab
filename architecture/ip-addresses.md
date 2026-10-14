# Mini-SOC — IP Address Table

| VM | Operating System | Interface | IP Address | Network |
|---|---|---|---|---|
| siem-host | Ubuntu Server 22.04 | ens33 | 192.168.141.142/24 | NAT |
| siem-host | Ubuntu Server 22.04 | ens34 | 192.168.174.10/24 | Host-only |
| ubuntu-web | Ubuntu Server 22.04 | Host-only adapter | 192.168.174.20/24 | Host-only |
| win-client | Windows 10 | Host-only adapter | 192.168.174.30/24 | Host-only |

## Network Configuration

- **NAT Gateway:** 192.168.141.2
- **Host-only Subnet:** 192.168.174.0/24
- **SIEM Dashboard:** https://192.168.174.10
- **Apache Web Server:** http://192.168.174.20

## Network Isolation

Only siem-host has permanent NAT connectivity.

ubuntu-web and win-client communicate with the Wazuh Manager through the isolated Host-only network. Neither endpoint has an Internet gateway.
