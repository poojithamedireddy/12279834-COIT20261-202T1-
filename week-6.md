


##  Objective
To observe how the ARP (Address Resolution Protocol) table on Host A changes as it communicates with other hosts in the same network.

##  Network Topology
- Four hosts: A, B, C, D
- Connected via a Layer 2 switch
- Same subnet: `192.168.0.0/24`


##  Commands Used
ip addr show
ip neigh show
ping -c 3 destination_ip

## ARP Table Observations (Host A)

###  Initial State
- Command: `ip neigh show`
- **Result:**
  - No ARP entries present
- **Explanation:**
  - Host A has not communicated with any device yet, so no IP-to-MAC mappings exist.
    
###  After Pinging 192.168.0.3 (Host C)
ping -c 3 192.168.0.3
**Result:**
  - 3 packets transmitted, 3 received (0% packet loss)
  - Low latency (~0.02–0.04 ms)
**ARP Change:**
  - Entry added for `192.168.0.3`
**Explanation:**
  - Host A sends an ARP request (broadcast)
  - Host C replies with its MAC address
  - Mapping is stored in ARP cache

### After Pinging 192.168.0.1
ping -c 3 192.168.0.1
- **Result:**
  - 3 packets transmitted, 3 received (0% packet loss)
  - Latency ~0.12–0.44 ms
- **ARP Change:**
  - Entry added for `192.168.0.1`
- **Explanation:**
  - Another ARP request/reply cycle occurs
  - Multiple entries now exist in ARP table
## Summary of ARP Behavior
- ARP table starts empty
- Entries are added dynamically after communication
- Each new IP requires ARP resolution
- Entries are cached temporarily and may expire
- ARP reduces repeated broadcasts after initial resolution
## Key Networking Insights
- All hosts are in the same subnet → direct communication
- No router is required
- Switch forwards ARP broadcast to all devices
- Communication occurs using MAC addresses after ARP resolution
##  Reflection
This lab helped me understand how ARP works in a practical environment rather than just theory. Initially, I assumed devices could communicate directly using IP addresses, but this exercise showed that MAC address resolution is a necessary step in local networks.

One important observation was that the ARP table is empty before any communication. This highlights that ARP is a dynamic protocol that only stores information when needed. After performing ping operations, I could see how entries were created automatically, which made the process much clearer.

Another key takeaway is the role of broadcasts in ARP. When Host A needed to find another device, it sent a broadcast request to all devices in the network. This demonstrated how switches handle broadcast traffic and how only the correct host responds.

I also noticed that once an ARP entry is created, subsequent communication becomes more efficient because the MAC address is already known. This reduces network overhead and improves performance.

