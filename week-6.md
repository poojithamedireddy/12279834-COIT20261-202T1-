# Task 1 


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



## task -2

### Left LAN (192.168.0.0/24)
| Device  | IP Address   | Default Gateway |
|---------|--------------|-----------------|
| Host1   | 192.168.0.2  | 192.168.0.1     |
| Host2   | 192.168.0.3  | 192.168.0.1     |
| Router1 | 192.168.0.1  | -               |

### Right LAN (192.168.1.0/24)
| Device  | IP Address   | Default Gateway |
|---------|--------------|-----------------|
| Host3   | 192.168.1.2  | 192.168.1.1   |
| Host4   | 192.168.1.3  | 192.168.1.1   |
| Router2 | 192.168.1.1  | -               |

### Host1
ip addr add 192.168.0.2/24 dev eth0
ip route add default via 192.168.0.1
### Host2
ip addr add 192.168.0.3/24 dev eth0
ip route add default via 192.168.0.1

### Host3
ip addr add 192.168.1.2/24 dev eth0
ip route add default via 192.168.1.1

### Host4
ip addr add 192.168.1.3/24 dev eth0
ip route add default via 192.168.1.1

### Router1
ip addr add 192.168.0.1/24 dev eth0
ip route add 192.168.1.0/24 via <Router2-Link-IP>

###  Router2
ip addr add 192.168.1.1/24 dev eth0
ip route add 192.168.0.0/24 via <Router1-Link-IP>

### Test Ping
ping 192.168.1.2

### Expected Result
- Successful communication between subnets
- 0% packet loss

## Key Concept
- Devices in different subnets **cannot communicate directly**
- Traffic must go through a router (default gateway)
- Each subnet has its own gateway:
  - Left LAN - 192.168.0.1
  - Right LAN - 192.168.1.1

##Reflection

During this lab, I initially configured the same default gateway (192.168.0.1) for all hosts, but this caused communication issues for devices in the 192.168.1.0 network. This helped me realize that a default gateway must always belong to the same subnet as the host.

After correcting the gateway for Host3 and Host4 to 192.168.1.1, the network started working correctly. This demonstrated the importance of proper IP addressing and gateway configuration.

I also learned that routers act as intermediaries between networks, and without correct routing and gateway settings, devices cannot communicate across subnets.




