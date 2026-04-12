
## Network Segmentation
* Here, This configuration helps to setting up network to this security lab    
---------------------------------------------------------------------
| Network      | CIDR           | Purpose           | Network Type  |
|--------------|----------------|-------------------|---------------|
| Management   | 10.0.0.0/24    | Admin             | NAT_N/W(1)    |
| Red Team     | 192.168.1.0/24 | Attackers         | NAT           |
| Victim-1     | 10.0.1.0/24    | Targets           | NAT_N/W(1)    |
| Blue Team    | 10.0.3.0/24    | SOC               | NAT_N/W(1)    |
| Victim-2  (optional)    | 10.0.2.0/24    | Targets (DMZ)     | NAT_N/W(2)    |
|   |                |                   |               |
---------------------------------------------------------------------

## Firewall rules :
* here the basic and important firewall rules to  manage and filter  the netwrok traffic effectively!
* (Tips): To implement seperate firewall on each domain which possess more secure ! so, try also this if you have enough capacity!
  ### Note!
    *  Ensure the connection setup and rules whenever perform attack simulation! because, any of the attack simulation makes big potential threat to your system !
    *  keep this virtual lab privately in to your host .

1.Red Team Isolation (Mandatory):
---------------------------------------------------------------------------------------------------------------------------------
| Source                         | Destination                   | Protocol / Port | Action | Notes                              |
| ------------------------------ | ----------------------------- | --------------- | ------ | ---------------------------------- |
| Red Team Network (192.168.1.0/24) | Victim DMZ (e.g., web server) | TCP 80, 443     | Allow  | Simulates external attacker access |
| Red Team Network               | Victim Internal Network       | Any             | Deny   | Prevent direct internal access     |
| Red Team Network               | Blue Team / SIEM              | Any             | Deny   | No monitoring bypass               |
| Red Team Network               | Management Network            | Any             | Deny   | Isolated from admin console        |
----------------------------------------------------------------------------------------------------------------------------------


2.Victim Network Rules:
-----------------------------------------------------------------------------------------------------------------------
| Source         | Destination      | Protocol / Port | Action         | Notes                                         |
| -------------- | ---------------- | --------------- | -------------- | --------------------------------------------- |
| Victim Network | SIEM / Blue Team | TCP 514, 12201  | Allow          | Forward syslog / Winlogbeat / logs            |
| Victim Network | Management       | SSH / RDP       | Allow          | Optional for admin access                     |
| Victim Network | Internet         | TCP 80,443      | Optional Allow | For lab updates only                          |
| Victim DMZ     | Internal Servers | TCP Any         | Deny           | Segmentation; optional specific allowed ports |
------------------------------------------------------------------------------------------------------------------------

3.Blue Team / SOC Rules:
-----------------------------------------------------------------------------------------------------------
| Source            | Destination    | Protocol / Port | Action | Notes                                   |
| ----------------- | -------------- | --------------- | ------ | --------------------------------------- |
| Blue Team Network | Victim Network | TCP 514, 12201  | Allow  | Collect logs                            |
| Blue Team         | Red Team       | Any             | Deny   | Blue Team should not initiate attacks   |
| Blue Team         | Management     | Any             | Allow  | Admin access to firewall / orchestrator |
-----------------------------------------------------------------------------------------------------------


4.Management / Admin Network Rules
-------------------------------------------------------------------------------------------------------------------------------
| Source             | Destination  | Protocol / Port | Action          | Notes                                                |
| ------------------ | ------------ | --------------- | --------------- | ---------------------------------------------------- |
| Management Network | All Networks | TCP/UDP Any     | Allow           | For lab control / Orchestration (Ansible, Terraform) |
| Management         | Red Team     | Any             | Deny by default | Only allow controlled access if needed               |
-------------------------------------------------------------------------------------------------------------------------------

## 5. Optional Rules (Enhancements)
  * **ICMP:**
     * Allow ping only from management for testing connectivity.
     * Deny ICMP from Red Team → Victim Internal Network.
  * **NAT / Port Forwarding:**
     *  Optional for Red Team to reach specific DMZ services.
  *  **VPN / Jump Box:**
     *  If Red Team is external, only allow connection via jump host.

 
