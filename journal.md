**Mini-SOC - Week 1 Lab Journal
Project: LabShop Mini-SOC
Platform: VMware Workstation, Wazuh 4.14.8**

**Entry 1 - Wazuh Administrator Password Issue**
Problem: After changing the default administrator password, authentication failed with HTTP 401.
Investigation: Checked the administrator password hash and Docker configuration.
Solution: Restored the clean environment, regenerated the password hash, verified that it matched the new password, and applied the updated security configuration.
Result: The new password returned HTTP 200, while the old password returned HTTP 401.

**Entry 2 - Docker Network Failure**
Problem: Wazuh Dashboard became inaccessible even though all three Docker containers were running.
Investigation: Checked Docker logs, HTTPS connectivity, container IP addresses, and the Linux routing table. The Docker bridge route was missing.
Solution: Configured systemd-networkd to leave Docker interfaces unmanaged and restarted the network and Docker services.
Result: Docker bridge routing was restored, and the Dashboard became accessible again.

**Entry 3 - Linux NAT and Package Installation**
Problem: The temporary NAT adapter on ubuntu-web did not receive an IP address. Later, APT returned HTTP 404 during package installation.
Investigation: Checked network interfaces, Netplan configuration, and package repository information.
Solution: Enabled DHCP for the NAT interface using Netplan and refreshed the APT package lists.
Result: Network connectivity and package installation worked successfully.

**Entry 4 - Windows Agent Installation**
Problem: The WazuhSvc service was not found after the initial Windows Agent installation attempt.
Investigation: Checked the MSI installer, Windows services, and the msiexec process.
Solution: Reinstalled Wazuh Agent with MSI logging and verified the installation exit code.
Result: Installation returned ExitCode 0, and WazuhSvc entered the Running state.

**Entry 5 - Sysmon Event Visibility and Time Synchronization**
Problem: Sysmon generated Windows events, but some recent events were difficult to locate in Wazuh Discover.
Investigation: Checked the Sysmon Operational log, Wazuh Agent configuration, event timestamps, and time zones.
Solution: Corrected the Windows time zone to Azerbaijan Standard Time and aligned the system clock with the SIEM server.
Result: Sysmon Process Creation events were successfully located in Wazuh Discover.

**Entry 6 - Persistence Verification**
Objective: Verify that Wazuh configuration, agents, and alerts survive service restarts and system reboot.
Actions: Stopped and started the Wazuh Docker containers, then rebooted siem-host.
Result: All Wazuh components returned to operation, both agents were Active, and previous security alerts remained available.

**Lessons Learned**
Verify infrastructure and network connectivity before troubleshooting applications.
Container status alone does not guarantee service availability.
Accurate time synchronization is essential for SIEM investigations.
Raw events and security alerts are not the same.
Snapshots significantly reduce recovery time.
Clear documentation makes troubleshooting and rebuilding easier.
