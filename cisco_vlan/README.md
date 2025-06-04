# Cisco VLAN

## Auftrag 7 - VLAN Configuration

[Abgabe 7](./07_VLAN%20Configuration.pka)

### S1

```bash
enable
configure terminal
vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 30
name Rayan(Default)
vlan 99
name Management&Native
vlan 150
name VOICE
```

### S2

```bash
enable
configure terminal
vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 30
name Rayan(Default)
vlan 99
name Management&Native
vlan 150
name VOICE

interface f0/11
switchport mode access
switchport access vlan 10
interface f0/18
switchport mode access
switchport access vlan 20
interface f0/6
switchport mode access
switchport access vlan 30

```

### S3

```bash
enable
configure terminal
vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 30
name Rayan(Default)
vlan 99
name Management&Native
vlan 150
name VOICE

interface f0/11
switchport mode access
switchport access vlan 10
interface f0/18
switchport mode access
switchport access vlan 20
interface f0/6
switchport mode access
switchport access vlan 30
interface f0/11
mls qos trust cos
switchport voice vlan 150
```

## Auftrag 8 - Configure Trunks

[Abgabe 8](./08_Configure%20Trunks.pka)

### S1

```bash
enable
configure terminal
interface range g0/1 - 2
switchport mode trunk

switchport trunk native vlan 99

interface range G0/1 - 2
switchport mode trunk
```

### S2

```bash
enable
configure terminal
interface Gig0/1
switchport trunk native vlan 99
```


### S3

```bash
enable
configure terminal
interface Gig0/2
switchport trunk native vlan 99
```

## Auftrag 9 - Implement VLANs and Trunking

[Abgabe 9](./09_Implement%20VLANs%20and%20Trunking.pka)

### SWA

```bash
enable
  configure terminal
  vlan 10
  name Admin
  vlan 20
  name Accounts
  vlan 30
  name HR
  vlan 40
  name Voice
  vlan 99
  name Management
  vlan 100
  name Native

  interface vlan99
  ip address 192.168.99.252 255.255.255.0
  no shutdown

  interface Gig0/1
  switchport mode trunk
  switchport nonegotiate
  switchport trunk native vlan 100

interface Gig0/2
switchport mode dynamic desirable
switchport trunk native vlan 100

```


### SWB

```bash
enable
configure terminal
vlan 10
name Admin
vlan 20
name Accounts
vlan 30
name HR
vlan 40
name Voice
vlan 99
name Management
vlan 100
name Native

interface FastEthernet0/1
switchport mode access
switchport access vlan 10

interface FastEthernet0/2
switchport mode access
switchport access vlan 20

interface FastEthernet0/3
switchport mode access
switchport access vlan 30

interface vlan99
ip address 192.168.99.253 255.255.255.0
no shutdown

interface Gig0/1
switchport mode trunk
switchport nonegotiate
switchport trunk native vlan 100

```

### SWC

```bash
enable
configure terminal
vlan 10
name Admin
vlan 20
name Accounts
vlan 30
name HR
vlan 40
name Voice
vlan 99
name Management
vlan 100
name Native

interface FastEthernet0/1
switchport mode access
switchport access vlan 10

interface FastEthernet0/2
switchport mode access
switchport access vlan 20

interface FastEthernet0/3
switchport mode access
switchport access vlan 30

interface FastEthernet0/4
switchport mode access
switchport access vlan 10
switchport voice vlan 40

interface vlan99
ip address 192.168.99.254 255.255.255.0
no shutdown

interface Gig0/2
switchport trunk native vlan 100
```

## Auftrag 10 - Investigate a VLAN Implementation

1. **Were the pings successful? Explain. (PC1 to PC6)**
   No, they are in different VLANs.

2. **Where did S3 send the packet after receiving it?**
   Only to the ports in VLAN 10, not to PC6.

3. **Were the pings successful? Explain. (PC1 to PC4)**
   Yes, both are in VLAN 10.

4. **When the packet reached S1, why does it also forward the packet to PC7?**
   PC7 is also in VLAN 10, and the switch doesn't know the MAC address yet → broadcast.

5. **What command is used to delete the startup configuration of the switches?**
   `erase startup-config`

6. **Where is the VLAN file stored in the switches?**
   In Flash/NVRAM.

7. **What command deletes the VLAN file stored in the switches?**
   `delete flash:vlan.dat`

8. **If a PC in VLAN 10 sends a broadcast message, which devices receive it?**
   PC1, PC4, PC7

9. **If a PC in VLAN 20 sends a broadcast message, which devices receive it?**
   PC2, PC5, PC8

10. **If a PC in VLAN 30 sends a broadcast message, which devices receive it?**
    PC3, PC6, PC9

11. **What happens to a frame sent from a PC in VLAN 10 to a PC in VLAN 30?**
    It does not get delivered – VLANs are separated.

12. **In terms of ports, what are the collision domains on the switch?**
    Each port is its own collision domain.

13. **In terms of ports, what are the broadcast domains on the switch?**
    By default: one. With VLANs: one per VLAN.


## Auftrag 11 - Inter-VLAN Routing Challenge

[Abgabe 11](./11_Inter-VLAN%20Routing%20Challenge.pka)

### R1

```bash
enable
configure terminal

interface Gig0/0
ip address 172.17.25.2 255.255.252.0
no shutdown

interface Gig0/1
no shutdown

interface Gig0/1.10
encapsulation dot1Q 10
ip address 172.17.10.1 255.255.255.0

interface Gig0/1.20
encapsulation dot1Q 20
ip address 172.17.20.1 255.255.255.0

interface Gig0/1.30
encapsulation dot1Q 30
ip address 172.17.30.1 255.255.255.0

interface Gig0/1.88
encapsulation dot1Q 88 native
ip address 172.17.88.1 255.255.255.0

interface Gig0/1.99
encapsulation dot1Q 99
ip address 172.17.99.1 255.255.255.0
```

### S1

```bash
enable
configure terminal

vlan 10
name Faculty/Staff

vlan 20
name Students

vlan 30
name Rayan(Default)

vlan 88
name Native

vlan 99
name Management

interface vlan 99
ip address 172.17.99.10 255.255.255.0
no shutdown

ip default-gateway 172.17.99.1

interface range FastEthernet0/11-17
switchport mode access
switchport access vlan 10

interface range FastEthernet0/18-24
switchport mode access
switchport access vlan 20

interface range FastEthernet0/6-10
switchport mode access
switchport access vlan 30

interface Gig0/1
switchport mode trunk
switchport nonegotiate
switchport trunk native vlan 88

interface range FastEthernet0/1-5, Gig0/2
shutdown
```
