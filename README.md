## Dual-WAN ISP Failover & Network Resilience

What happens to your security posture when the primary ISP goes down?
A dual-WAN ISP failover setup designed to maintain business connectivity when the primary internet connection becomes unavailable, while keeping routing, NAT, firewall enforcement, and security visibility consistent across both WAN paths.

### Overview
Internet connectivity is often treated as a basic infrastructure requirement, but for businesses that depend on continuous access to cloud applications, communication platforms, remote services, and online operations, an ISP outage can quickly become an availability and security concern.

<img width="776" height="629" alt="Screenshot 2026-09-23 125125" src="https://github.com/user-attachments/assets/2983aad9-868d-4dfc-8d1a-54b3680ac19b" />

Under normal conditions, traffic uses the primary ISP. If the primary path becomes unavailable, the router automatically activates the secondary WAN connection without requiring users or administrators to manually reconnect.

**I set up:**
- Two independent ISP connections terminating on the MikroTik
- ISP 1 as the primary WAN - "`192.168.100.0/24`"
- ISP 2 as the secondary WAN - "`10.0.137.0/24`"
- Both WAN interfaces configured as DHCP clients
- Primary and backup default routes using route distance
- ISP 1 route distance: "1"
- ISP 2 route distance: "2"
- Dedicated LAN on "ether3" - "`172.16.0.10/24`"
- DHCP server for automatic client addressing
- NAT/masquerading across both WAN interfaces
- Automatic failover and failback
- Traffic-path verification using VPCS "trace"


When ISP 1 is active:

"VPC ➡️ `172.16.0.10` ➡️ `192.168.100.1` ➡️ Internet"

When ISP 1 goes offline, ISP 2 takes over:

"VPC ➡️ `172.16.0.10` ➡️ `10.0.137.1` ➡️ Internet"

<img width="735" height="746" alt="image" src="https://github.com/user-attachments/assets/1ce61898-599d-47b3-9f8c-34d4841759cc" />

<img width="896" height="756" alt="image" src="https://github.com/user-attachments/assets/f7846259-ed55-4128-b0f9-0d47659ced9b" />


