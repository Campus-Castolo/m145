# Cisco

## 1. Navigating IOS

The question mark `?` provides context-sensitive help:

* `?` lists all available commands.
* `t?` shows all commands beginning with "t" (e.g., `telnet`, `terminal`, `traceroute`).
* `te?` further narrows the choices (e.g., `telnet`, `terminal`).

Upon starting, you are in User EXEC Mode (`S1>`).
Enter `enable` to switch to Privileged EXEC Mode (`S1#`).

Example:

* `S1> enable` → `S1#`
* `S1> en<Tab>` completes the command to `enable`, if unique.

No auto-completion occurs if multiple commands share the same prefix.

In Privileged EXEC Mode, enter configuration mode using `configure` or `conf`.
Input: `S1# configure` → then press Enter; the prompt changes to `S1(config)#`.

Return to EXEC mode with:

* `exit`, `end`, or `Ctrl+Z`.

View the current time:

```bash
S1# show clock
```

Set the clock:

```bash
S1# clock set 15:00:00 31 Jan 2035
```

To verify:

```bash
S1# show clock
```

Error messages for incorrect or incomplete commands:

* `% Incomplete command`
* `% Invalid input detected at '^' marker`

Examples:

* `S1# cl<Tab>` → no completion possible
* `S1# clock` → `% Incomplete command`
* `S1# clock set 25:00:00` → `% Invalid input`
* `S1# clock set 15:00:00 32` → `% Invalid input`

## 2. Switch Basic Configuration

### Basic Setup

Configure Switch S1 and S2 similarly:

```bash
enable
configure terminal
hostname S1
line console 0
password letmein
login
exit
enable password c1$c0
enable secret itsasecret
banner motd "Unauthorized Access"
service password-encryption
exit
copy running-config startup-config
```

## 3. Network Diagnostics

Example Configuration:

Switch S1:

```bash
enable
configure terminal
hostname S1
banner motd "Unauthorized Access"
line console 0
password cisco
login
exit
enable secret class
exit
configure terminal
interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
copy running-config startup-config
```

Switch S2:

```bash
enable
configure terminal
hostname S2
banner motd "Unauthorized Access"
line console 0
password cisco
login
exit
enable secret class
exit
configure terminal
interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
copy running-config startup-config
```

PC Configuration:

```
PC1: 192.168.1.1 255.255.255.0
PC2: 192.168.1.2 255.255.255.0
```

## 4. Subnetting and Routing

### 4.1 Local Communication (Ping within Same Subnet)

| Gerät           | Ziel-MAC             | Quell-MAC            | Quell-IP    | Ziel-IP     |
| --------------- | -------------------- | -------------------- | ----------- | ----------- |
| **172.16.31.5** | 00:0C:85\:CC:1D\:A7  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.2 |
| **Switch1**     | 00:0C:85\:CC:1D\:A7  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.2 |
| **Hub**         | 00:0C:85\:CC:1D\:A7  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.2 |
| **172.16.31.2** | 00\:D0\:D3:11\:C7:88 | 00:0C:85\:CC:1D\:A7  | 172.16.31.2 | 172.16.31.5 |

#### Extras

**Ping from 172.16.31.3 to 172.16.31.2**

| Gerät           | Ziel-MAC            | Quell-MAC           | Quell-IP    | Ziel-IP     |
| --------------- | ------------------- | ------------------- | ----------- | ----------- |
| **172.16.31.3** | 00:0C:85\:CC:1D\:A7 | 00:60:70:36:28:49   | 172.16.31.3 | 172.16.31.2 |
| **Hub**         | 00:0C:85\:CC:1D\:A7 | 00:60:70:36:28:49   | 172.16.31.3 | 172.16.31.2 |
| **172.16.31.2** | 00:60:70:36:28:49   | 00:0C:85\:CC:1D\:A7 | 172.16.31.2 | 172.16.31.3 |


**Ping from 172.16.31.5 to 172.16.31.4**

| Gerät           | Ziel-MAC             | Quell-MAC            | Quell-IP    | Ziel-IP     |
| --------------- | -------------------- | -------------------- | ----------- | ----------- |
| **172.16.31.5** | 00:0C\:CF:0B\:BC:80  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.4 |
| **Switch1**     | 00:0C\:CF:0B\:BC:80  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.4 |
| **172.16.31.4** | 00\:D0\:D3:11\:C7:88 | 00:0C\:CF:0B\:BC:80  | 172.16.31.4 | 172.16.31.5 |

### 4.2 Communication Across Subnets (via Router)

| Gerät        | Ziel-MAC                  | Quell-MAC                 | Quell-IP    | Ziel-IP     |
| ------------ | ------------------------- | ------------------------- | ----------- | ----------- |
| 172.16.31.5  | 00\:D0\:BA:8E:74:1A       | 00\:D0\:D3:11\:C7:88      | 172.16.31.5 | 10.10.10.2  |
| Switch1      | 00\:D0\:BA:8E:74:1A       | 00\:D0\:D3:11\:C7:88      | 172.16.31.5 | 10.10.10.2  |
| Router       | 00:60:2F:84:4A\:B6        | 00\:D0:58:8C:24:01        | 172.16.31.5 | 10.10.10.2  |
| Switch0      | 00:60:2F:84:4A\:B6        | 00\:D0:58:8C:24:01        | 172.16.31.5 | 10.10.10.2  |
| **Access Point** | 00\:D0:58:8C:24:02 | 00:60:2F:84:4A\:B6 | 172.16.31.5 | 10.10.10.2 |
| 10.10.10.2   | 00\:D0:58:8C:24:01 (WLAN) | 00:60:2F:84:4A\:B6 (WLAN) | 10.10.10.2  | 172.16.31.5 |

### 4.3 Reflection

1. **Were there different types of cables/media used to connect devices?**
   Yes. Copper Ethernet (twisted-pair) cables were used for wired links between PCs, switches, hubs, and the router. The wireless link between the Access Point and the remote host uses radio (Wi-Fi) media.

2. **Did the cables change the handling of the PDU in any way?**
   No. Regardless of whether the PDU was carried over copper or radio, the frame format at Layer 2 remained Ethernet (for the wired links) or 802.11 (for the wireless hop). The logical handling—encapsulation and forwarding—stayed consistent.

3. **Did the Hub lose any of the information that it received?**
   No. A hub is a physical-layer device; it regenerates and repeats every bit it hears without examining or discarding any frames.

4. **What does the Hub do with MAC addresses and IP addresses?**
   It ignores them. The hub forwards all incoming electrical signals out every other port, without any MAC- or IP-based filtering or learning.

5. **Did the wireless Access Point do anything with the information given to it?**
   It acted as a Layer 2 bridge: it stripped the radio encapsulation and forwarded the Ethernet frame over the wired side (and vice versa). It did not examine Layer 3 (IP) headers.

6. **Was any MAC or IP address lost during the wireless transfer?**
   No. Both MAC and IP addresses remained intact; only the Layer 2 encapsulation changed (Ethernet ↔ 802.11).

7. **What was the highest OSI layer that the Hub and Access Point used?**
   Both operated at Layer 1 (Hub) and Layer 2 (Access Point). Neither examined beyond the data-link layer.

8. **Did the Hub or Access Point ever replicate a PDU that was rejected with a red “X”?**
   No. Neither device filters or rejects frames; they faithfully forward everything they receive.

9. **When examining the PDU Details tab, which MAC address appeared first, the source or the destination?**
   The Destination MAC appears first, then the Source MAC.

10. **Why would the MAC addresses appear in this order?**
    Ethernet frame headers are structured as \[Destination MAC]\[Source MAC]\[EtherType]\[Payload], so destination is always listed before source.

11. **Was there a pattern to the MAC addressing in the simulation?**
    Yes. Each manufacturer/vendor prefix (the first three octets) is consistent per device type:

* PCs: 00D0\:D311\:xxxx
* Switches: 000C:85CC\:xxxx
* Router: 00D0:588C\:xxxx or 0060:2F84\:xxxx
* Access Point: same as router/switch pattern
* Gateway interface toward 172.16.31.0 network used 00D0\:BA8E:741A

12. **Did the switches ever replicate a PDU that was rejected with a red “X”?**
    No. Switches learn MAC addresses and forward only out the correct port; they do not generate rejects in simulation unless there’s a filtering rule.

13. **Every time that the PDU was sent between the 10 network and the 172 network, there was a point where the MAC addresses suddenly changed. Where did that occur?**
    At the router’s interfaces. When the packet left the 172.16.31.0 LAN toward 10.10.10.0, the router de-encapsulated and re-encapsulated the frame with its serial interface MAC and the next-hop MAC.

14. **Which device uses MAC addresses that start with 00D0\:BA?**
    The router’s interface on the 172.16.31.0 network (the default gateway for the PCs) – this is the destination MAC on the initial hop.

15. **What devices did the other MAC addresses belong to?**

* 00D0\:D311\:C788: Source PC (172.16.31.5)
* 000C:85CC:1DA7: Switch1
* 0060:2F84:4AB6: Router’s Fa0/0 interface toward 10.10.10.0
* Other vendor prefixes belonged to PCs, switches, or the AP as labeled in the topology.

16. **Did the sending and receiving IPv4 addresses change fields in any of the PDUs?**
    No. The IP header (source 172.16.31.5; destination 10.10.10.2) remained unchanged end-to-end.

17. **When you follow the reply to a ping, sometimes called a pong, do you see the sending and receiving IPv4 addresses switch?**
    Yes. On the echo reply, the source becomes 10.10.10.2 and the destination 172.16.31.5, reversing the IP header.

18. **What is the pattern to the IPv4 addressing used in this simulation?**
    Each LAN uses a distinct /24 network: 172.16.31.0/24 for the local PCs, 10.10.10.0/24 for the remote. Hosts are numbered .1–.5, .2 for the server.

19. **Why do different IP networks need to be assigned to different ports of a router?**
    Routers separate broadcast domains and route between networks. Each physical interface must reside in its own subnet so the router can distinguish where to forward packets.

20. **If this simulation was configured with IPv6 instead of IPv4, what would be different?**

* IPv6 addresses (128-bit) in the IP header.
* Ethernet Type field would indicate IPv6 (0x86DD).
* No ARP; instead, Neighbor Discovery (ICMPv6) would resolve link-layer addresses.
* SLAAC or DHCPv6 could provide addresses.
* Packet fragmentation handled end-to-end, not by routers.

## 5. VLAN Setup

### 5.1 ARP Requests

Ping from `172.16.31.2` to `172.16.31.3` after `arp -d`:

* Broadcast MAC: `FF:FF:FF:FF:FF:FF`
* ARP response MAC matches the target IP.

### 5.2 MAC Address Tables

Generated via traffic (ping tests). MAC tables consistent with observed traffic.

### 5.3 ARP in Routing

* ARP queries gateway IP, not destination IP, when target is in a different subnet.

## 6. Inter-VLAN Routing

### Custom Router Setup

```bash
enable
configure terminal
hostname CustomerRouter
enable secret Class123
line console 0
password Cisco123
login
exit
interface g0/0
ip address 192.168.0.1 255.255.255.192
no shutdown
exit
interface g0/1
ip address 192.168.0.65 255.255.255.192
no shutdown
exit
interface s0/1/0
ip address 209.165.201.2 255.255.255.252
no shutdown
exit
end
write memory
```

### LAN-A and LAN-B Setup

LAN-A:

```bash
enable
configure terminal
interface vlan1
ip address 192.168.0.2 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.1
end
write memory
```

LAN-B:

```bash
enable
configure terminal
interface vlan1
ip address 192.168.0.66 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.65
end
write memory
```

### PC Configurations

PC-A:

```bash
192.168.0.62 255.255.255.192 192.168.0.1
```

PC-B:

```bash
192.168.0.126 255.255.255.192 192.168.0.65
```
