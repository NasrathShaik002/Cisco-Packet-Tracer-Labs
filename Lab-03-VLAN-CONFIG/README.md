# VLAN Configuration Lab - Cisco Packet Tracer

## Objective

To create VLANs, assign switch ports to different VLANs, verify VLAN membership, and check interface status using Cisco Packet Tracer.
-------
## Lab: Implementing VLANs

### 1. Create VLANs

Open the Cisco 2960 Switch CLI and enter the following commands:

```cisco
enable
configure terminal
vlan 10
 name SALES
vlan 20
 name MARKETING
exit
write memory
show vlan
```
**Note:** VLAN IDs 1–1001 can be created and used for normal VLAN configuration. VLANs 1002–1005 are reserved.
................

### 2. Connect Ports to VLAN 10 - SALES Department

Open the Cisco 2960 Switch CLI and enter:

```cisco
configure terminal
interface fa0/1
 switchport mode access
 switchport access vlan 10
exit
show vlan
.........

**Result:** Port FastEthernet0/1 is assigned to VLAN 10 (SALES Department).

---

### 3. Connect Ports to VLAN 20 - MARKETING Department

Open the Cisco 2960 Switch CLI and enter:

```cisco
configure terminal
interface fa0/5
 switchport mode access
 switchport access vlan 20
exit
```

Configure another port for VLAN 20:

```cisco
configure terminal
interface fa0/6
 switchport mode access
 switchport access vlan 20
exit
show vlan
```

**Result:** Ports FastEthernet0/5 and FastEthernet0/6 are assigned to VLAN 20 (MARKETING Department).

---

### 4. Configure Multiple Ports Using Interface Range

If we want to configure multiple ports for the same VLAN, we can use the interface range command.

Open the Cisco 2960 Switch CLI and enter:

```cisco
configure terminal
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 10
exit
```

For viewing all VLANs and connected interfaces:

```cisco
show vlan brief
```

**Purpose:** Displays all configured VLANs and the ports assigned to them.

---

## Verification Commands

```cisco
show vlan
show vlan brief
show ip interface brief
```

### Purpose

- `show vlan` → Displays configured VLANs.
- `show vlan brief` → Displays VLAN membership and assigned ports.
- `show ip interface brief` → Displays interface status and IP information.

---

## Lab Proof - Interface Status

Open the Cisco 2960 Switch CLI and enter:

```cisco
show ip interface brief
```

### Output

```text
Interface              IP-Address      OK? Method Status                Protocol
Vlan1                  unassigned      YES manual administratively down down
FastEthernet0/1        unassigned      YES manual up                    up
FastEthernet0/2        unassigned      YES manual up                    up
FastEthernet0/3        unassigned      YES manual up                    up
FastEthernet0/4        unassigned      YES manual down                  down
FastEthernet0/5        unassigned      YES manual down                  down
FastEthernet0/6        unassigned      YES manual down                  down
FastEthernet0/7        unassigned      YES manual down                  down
FastEthernet0/8        unassigned      YES manual down                  down
FastEthernet0/9        unassigned      YES manual down                  down
FastEthernet0/10       unassigned      YES manual down                  down
FastEthernet0/11       unassigned      YES manual down                  down
FastEthernet0/12       unassigned      YES manual down                  down
FastEthernet0/13       unassigned      YES manual down                  down
FastEthernet0/14       unassigned      YES manual down                  down
FastEthernet0/15       unassigned      YES manual down                  down
FastEthernet0/16       unassigned      YES manual down                  down
FastEthernet0/17       unassigned      YES manual down                  down
FastEthernet0/18       unassigned      YES manual down                  down
FastEthernet0/19       unassigned      YES manual down                  down
FastEthernet0/20       unassigned      YES manual down                  down
FastEthernet0/21       unassigned      YES manual down                  down
FastEthernet0/22       unassigned      YES manual down                  down
FastEthernet0/23       unassigned      YES manual down                  down
FastEthernet0/24       unassigned      YES manual down                  down
GigabitEthernet0/1     unassigned      YES manual down                  down
GigabitEthernet0/2     unassigned      YES manual down                  down
```

---

## Result

Successfully created VLAN 10 (SALES) and VLAN 20 (MARKETING), assigned switch ports to the respective VLANs, and verified the configuration using `show vlan`, `show vlan brief`, and `show ip interface brief` commands in Cisco Packet Tracer.

---

## Tools Used

- Cisco Packet Tracer
- Cisco 2960 Switch
- PCs
- FastEthernet Interfaces
- VLAN Technology
