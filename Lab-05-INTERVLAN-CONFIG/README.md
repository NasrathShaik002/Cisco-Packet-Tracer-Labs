# Cisco Packet Tracer Lab: Inter-VlanRouter on a Stick (ROAS)

## Inter-VLAN Routing Between VLAN 10 (soc) and VLAN 20 (soc12)

---

# Objective

In this lab, Router on a Stick (ROAS) was configured to enable communication between devices connected to VLAN 10 and VLAN 20. A Cisco Router and Cisco Switch were used to perform Inter-VLAN Routing.

---

# Theory

VLANs (Virtual Local Area Networks) are used to divide a network into separate logical groups. Devices within the same VLAN can communicate directly, but devices in different VLANs cannot communicate without a Layer 3 device such as a router.

Router on a Stick (ROAS) is a method of Inter-VLAN Routing where a single router interface is divided into multiple subinterfaces. Each subinterface is assigned to a VLAN and acts as the default gateway for that VLAN.

A trunk link is configured between the switch and router using IEEE 802.1Q encapsulation. This trunk carries traffic from multiple VLANs, allowing the router to route packets between them.

In this lab:

- VLAN 10 is named **soc**
- VLAN 20 is named **soc12**
- VLAN 10 uses network **192.168.10.0/24**
- VLAN 20 uses network **192.168.20.0/24**
- Inter-VLAN communication is achieved using Router on a Stick

---

# Network Topology

![Topology](topology.png)

The network consists of one router, one switch, two PCs, one laptop, and two servers. VLAN 10 (soc) and VLAN 20 (soc12) are configured on the switch, and communication between the two VLANs is provided through Router on a Stick.

---

# Devices Used

- 1 Cisco Router
- 1 Cisco Switch
- 2 PCs
- 1 Laptop
- 2 Servers
- Cisco Packet Tracer

---

# VLAN Information

| VLAN ID | VLAN Name | Network Address | Default Gateway |
|----------|----------|----------------|----------------|
| 10 | soc | 192.168.10.0/24 | 192.168.10.1 |
| 20 | soc12 | 192.168.20.0/24 | 192.168.20.1 |

---

# Port Assignment

| Switch Port | VLAN |
|------------|-------|
| Fa0/1 - Fa0/3 | VLAN 10 (soc) |
| Fa0/4 - Fa0/6 | VLAN 20 (soc12) |
| Fa0/24 | Trunk Port (Connected to Router) |

---

# Configuration

## Step 1: Create VLAN 10 and VLAN 20 on Cisco Switch

```bash( open switch cli)
enable
configure terminal

vlan 10
 name soc

vlan 20
 name soc12

exit
```

---

## Step 2: Assign Ports Fa0/1 to Fa0/3 to VLAN 10 on Cisco Switch

```bash
interface range fa0/1 - 3
 switchport mode access
 switchport access vlan 10
 no shutdown
exit
```

---

## Step 3: Assign Ports Fa0/4 to Fa0/6 to VLAN 20 on Cisco Switch

```bash
interface range fa0/4 - 6
 switchport mode access
 switchport access vlan 20
 no shutdown
exit
```

---

## Step 4: Configure Trunk Port Fa0/24 on Cisco Switch

```bash
interface fa0/24
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown
exit

end
write
```

---

## Step 5: Enable Interface Fa0/0 on Cisco Router

```bash
enable
configure terminal

interface fa0/0
 no shutdown
exit
```

---

## Step 6: Configure VLAN 10 Subinterface on Cisco Router

```bash(router cli)
interface fa0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit
```

---

## Step 7: Configure VLAN 20 Subinterface on Cisco Router

```bash
interface fa0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit

end
write
```

---

# Verification

## Verify VLAN Configuration on Cisco Switch

```bash
show vlan brief
```

Expected Result:

- VLAN 10 (soc) should be present
- VLAN 20 (soc12) should be present
- Ports Fa0/1 to Fa0/3 should be assigned to VLAN 10
- Ports Fa0/4 to Fa0/6 should be assigned to VLAN 20

---

## Verify Trunk Configuration on Cisco Switch

```bash
show interfaces trunk
```

Expected Result:

- Fa0/24 should be operating in trunk mode
- VLANs 10 and 20 should be allowed on the trunk

---

## Verify Switchport Details on Cisco Switch

```bash
show interfaces fa0/24 switchport
```

Expected Result:

- Administrative Mode: trunk
- Operational Mode: trunk
- Trunking Encapsulation: 802.1Q

---

## Verify Interface Status on Cisco Router

```bash
show ip interface brief
```

Expected Result:

- Fa0/0.10 should be up/up
- Fa0/0.20 should be up/up

---

## Verify Routing Table on Cisco Router

```bash
show ip route
```

Expected Result:

- Route for 192.168.10.0/24 should be present
- Route for 192.168.20.0/24 should be present

---

## Test Gateway Connectivity from PC or Laptop

```bash
ping 192.168.10.1
```

Expected Result:

Successful replies from the default gateway.

---

## Test Inter-VLAN Communication from PC or Laptop

```bash
ping 192.168.20.20
```

Expected Result:

Successful replies confirming communication between VLAN 10 and VLAN 20.

---

## Verify Packet Path from PC or Laptop

```bash
tracert 192.168.20.20
```

Expected Result:

The packet should pass through the router before reaching the destination device.

---

# Troubleshooting

## Troubleshooting Commands on Cisco Switch

```bash
show vlan brief
show interfaces trunk
show interfaces fa0/24 switchport
```

## Troubleshooting Commands on Cisco Router

```bash
show ip interface brief
show ip route
```

## Troubleshooting Commands on PC or Laptop

```bash
ping 192.168.10.1
ping 192.168.20.20
```

---

# Key Points

- VLANs help separate devices into different logical networks.
- Devices in different VLANs require a router to communicate.
- Router on a Stick uses one physical router interface with multiple subinterfaces.
- A trunk link carries traffic from multiple VLANs.
- Each VLAN must have its own subnet and default gateway.
- The `encapsulation dot1Q` command is required on router subinterfaces.

---

# Conclusion

In this lab, Router on a Stick (ROAS) was configured successfully to enable communication between VLAN 10 (soc) and VLAN 20 (soc12). VLANs were created on the switch, a trunk link was configured between the switch and router, and router subinterfaces were configured as default gateways. Verification and connectivity tests confirmed successful communication between devices in different VLANs.
Make a note of something
