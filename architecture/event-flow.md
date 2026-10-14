# Mini-SOC - Security Event Flow

## Event Flow

1. **Event Generation:** An activity occurs on an endpoint, such as a failed SSH login, Windows failed logon, or Sysmon process creation.

2. **Log Collection:** The Wazuh Agent collects the event from Linux log files or Windows Event Logs.

3. **Event Transmission:** The agent sends the collected event to the Wazuh Manager through the Host-only network.

4. **Analysis and Detection:** The Wazuh Manager decodes the event and evaluates detection rules. Matching rules can generate security alerts.

5. **Alert Storage:** Filebeat forwards generated alerts from the Wazuh Manager to the Wazuh Indexer, where they are indexed and stored.

6. **Visualization:** The Wazuh Dashboard queries the Indexer, allowing SOC analysts to search and investigate alerts.

## Event Flow Diagram

```text
Linux / Windows Endpoint
           |
           v
       Wazuh Agent
           |
           v
      Wazuh Manager
    (Decoders + Rules)
           |
           v
         Filebeat
           |
           v
      Wazuh Indexer
           |
           v
      Wazuh Dashboard
           |
           v
        SOC Analyst
```

## Practical Example

**Event:** Failed Windows login (Event ID 4625)

**Wazuh Rule ID:** 60122

**Rule Level:** 5

The failed login event was collected by the Windows Wazuh Agent, analyzed by the Wazuh Manager, indexed, and displayed in the Wazuh Dashboard.

**Evidence:** `evidence/05-detection/failed-windows-login1.png`
