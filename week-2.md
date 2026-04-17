## Task-1

![GitHub Screenshot Demo](images/week2-project.png)
![GitHub Screenshot Demo](images/week2-host2.png)
![GitHub Screenshot Demo](images/week2-host3.png)
![GitHub Screenshot Demo](images/week2-host4.png)
## Network Diagram Explanation

- The network consists of **4 hosts (PCs)** connected through a **central switch**
- The switch acts as an intermediary device that allows all hosts to communicate
- All hosts are in the same Local Area Network (LAN)
- The topology used is a **star topology**, where each host connects directly to the switch
- This setup ensures efficient communication between devices within the network

## IP Addressing Scheme

- The network uses the subnet: **10.1.1.0/24**
- Subnet mask: **255.255.255.0**
- All hosts belong to the same network, allowing direct communication

### Assigned IP Addresses:
- Host1 → 10.1.1.1
- Host2 → 10.1.1.2
- Host3 → 10.1.1.3
- Host4 → 10.1.1.4

## Explanation of IP Addressing

- Each host is assigned a **unique IP address**
- The first three octets (**10.1.1**) represent the **network portion**
- The last octet (1, 2, 3, 4) represents the **host portion**
- Since all devices share the same network portion, they can communicate directly without a router

## Communication in the Network

- When one host sends data (e.g., using ping), the packet is sent to the switch
- The switch forwards the packet to the correct destination host
- If the destination IP exists, a reply is received
- If the IP does not exist, the request times out (packet loss)

## Task-2

## Explanation of Ping Results
![GitHub Screenshot Demo](images/week2-count.png)

### 1. Simple Ping (Default)
- Command used: `ping 10.1.1.3`
- Tests basic connectivity between two hosts
- Each reply shows:
  - `icmp_seq` → packet sequence number
  - `ttl=64` → normal value for local network
  - `time` → round-trip delay (very low = fast connection)
- Result:
  - All packets sent were received
  - 0% packet loss
- Conclusion:
  - Network connection is working correctly

---

### 2. Ping to Wrong IP Address
- Command used: `ping 10.1.1.99`
- IP address does not exist in the network
- Result:
  - No replies received
  - 100% packet loss
- Conclusion:
  - Destination is unreachable
  - Helps identify incorrect IP or disconnected devices

---

### 3. Ping with Options
- Command used: `ping -c 100 -s 100 -i 0.2 10.1.1.3`
- Options used:
  - `-c 100` → send 100 packets
  - `-s 100` → increase packet size
  - `-i 0.2` → send packets every 0.2 seconds
- Result:
  - All 100 packets received
  - 0% packet loss
- Conclusion:
  - Network is stable under higher load
  - Can handle increased traffic without issues

### Overall Conclusion
- The network is correctly configured within a single subnet
- The switch enables communication between all hosts
- Proper IP addressing ensures successful connectivity
- Ping is used to test network connectivity
- Successful replies indicate a working network
- Packet loss indicates network problems
- Options allow testing of performance and reliability













