
# Network Segmentation
* Here, This configuration helps to setting the security lab network connection   
```
--------------------------------------------------------------------
| Network      | CIDR           | Purpose           | Network Type  |
|--------------|----------------|-------------------|---------------|
| Management   | 10.0.0.0/24    | Admin             | NAT_N/W(1)    |
| Red Team     | 192.168.1.0/24 | Attackers         | NAT           |
| Victim-1     | 10.0.1.0/24    | Targets           | NAT_N/W(1)    |
| Blue Team    | 10.0.3.0/24    | SOC               | NAT_N/W(1)    |
| Victim-2     | 10.0.2.0/24    | Targets (DMZ)     | NAT_N/W(2)    |
|(optional)    |                |                   |               |
---------------------------------------------------------------------
```
## Note !
 *  Ensure the connection setup whenever perform attack simulation  ! and keep this virtual lab privately in to your host .
 * To implement the firewall on each domain  which possess more effective setup  ! If you have enough capacity to your system.
 
