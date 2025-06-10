# GNS3 Configurations

## Task 1

### SW1

```bash
/system identity set name=SW1

/interface bridge add name=bridge1 protocol-mode=none vlan-filtering=yes

/interface bridge port add bridge=bridge1 comment="VLAN 101 – Accounting" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether4 pvid=101
/interface bridge port add bridge=bridge1 comment="VLAN 102 – Development" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether5 pvid=102
/interface bridge port add bridge=bridge1 comment="VLAN 103 – Sales" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether6 pvid=103

/interface bridge port add bridge=bridge1 frame-types=admit-only-vlan-tagged hw=no interface=ether8

/interface bridge vlan add bridge=bridge1 comment="VLAN 101" tagged=ether8 untagged=ether4 vlan-ids=101
/interface bridge vlan add bridge=bridge1 comment="VLAN 102" tagged=ether8 untagged=ether5 vlan-ids=102
/interface bridge vlan add bridge=bridge1 comment="VLAN 103" tagged=ether8 untagged=ether6 vlan-ids=103
```

### SW2

```bash
/system identity set name=SW2

/interface bridge add name=bridge1 protocol-mode=none vlan-filtering=yes

/interface bridge port add bridge=bridge1 comment="VLAN 101 – Accounting" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether4 pvid=101
/interface bridge port add bridge=bridge1 comment="VLAN 102 – Development" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether5 pvid=102
/interface bridge port add bridge=bridge1 comment="VLAN 103 – Sales" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether6 pvid=103

/interface bridge port add bridge=bridge1 frame-types=admit-only-vlan-tagged hw=no interface=ether8

/interface bridge vlan add bridge=bridge1 comment="VLAN 101" tagged=ether8 untagged=ether4 vlan-ids=101
/interface bridge vlan add bridge=bridge1 comment="VLAN 102" tagged=ether8 untagged=ether5 vlan-ids=102
/interface bridge vlan add bridge=bridge1 comment="VLAN 103" tagged=ether8 untagged=ether6 vlan-ids=103
```

### PC1

```bash
ip 192.168.1.10 255.255.255.0
```

### PC2

```bash
ip 192.168.2.10 255.255.255.0
```

### PC3

```bash
ip 192.168.3.10 255.255.255.0
```

### PC4

```bash
ip 192.168.1.11 255.255.255.0
```

### PC5

```bash
ip 192.168.2.11 255.255.255.0
```

### PC6

```bash
ip 192.168.3.11 255.255.255.0
```

---

## Task 2

**First, set all clients to DHCP.**

### RT1 (Router)

```bash
# Create VLAN interfaces on ether2
/interface vlan add interface=ether2 vlan-id=101 name=ether2_vlan101
/interface vlan add interface=ether2 vlan-id=102 name=ether2_vlan102
/interface vlan add interface=ether2 vlan-id=103 name=ether2_vlan103

# Assign IP addresses to VLAN interfaces
/ip address add address=192.168.55.1/24 interface=ether2_vlan101
/ip address add address=192.168.65.1/24 interface=ether2_vlan102
/ip address add address=192.168.75.1/24 interface=ether2_vlan103

# VLAN mapping for tagged and untagged interfaces
/interface bridge vlan set numbers=0 tagged=ether8,ether2 untagged=ether4
/interface bridge vlan set numbers=1 tagged=ether8,ether2 untagged=ether5
/interface bridge vlan set numbers=2 tagged=ether8,ether2 untagged=ether6

# Add router port to the bridge
/interface bridge port add bridge=bridge1 interface=ether2

# Add VLANs to the bridge with tagging
/interface bridge vlan add bridge=bridge1 tagged=ether2 vlan-ids=101,102,103

# DHCP Server setup for VLAN 101
/ip dhcp-server setup
Interface: ether2_vlan101
DHCP address space: 192.168.55.0/24
Gateway: 192.168.55.1
IP pool: 192.168.55.2-192.168.55.254
DNS server: 8.8.8.8
Lease time: 3 days

# DHCP Server setup for VLAN 102
/ip dhcp-server setup
Interface: ether2_vlan102
DHCP address space: 192.168.65.0/24
Gateway: 192.168.65.1
IP pool: 192.168.65.2-192.168.65.254
DNS server: 8.8.8.8
Lease time: 3 days

# DHCP Server setup for VLAN 103
/ip dhcp-server setup
Interface: ether2_vlan103
DHCP address space: 192.168.75.0/24
Gateway: 192.168.75.1
IP pool: 192.168.75.2-192.168.75.254
DNS server: 8.8.8.8
Lease time: 3 days

# Set internal DNS for VLAN 102 (optional tweak)
/ip dhcp-server network set [find address=192.168.65.0/24] dns-server=192.168.65.1
```
