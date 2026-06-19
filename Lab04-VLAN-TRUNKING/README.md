### CISCO PACKET TRACER LAB - VLAN TRUNKING CONFIGURATION
## Lab Objective

The objective of this lab is to configure VLANs on two Cisco 2960 switches and establish communication between devices in the same VLAN across different switches using a trunk link.

---
## Network Topology
## Switch to Switch Trunk Proof

**Topology:** S0-Gi0/1  =====  S1-Gi0/2

### Switch0 Output
![S0 Proof](s0-trunk.png)
*Gi0/1 is up/up and in trunking mode*

### Switch1 Output  
![S1 Proof](s1-trunk.png)
*Gi0/2 is up/up and in trunking mode*

**Verification Commands Used:**
- `show ip interface brief`  -> Link Status = up/up
- `show interface trunk`     -> Status = trunking
### Switch0
- PC1 → Fa0/1 → VLAN 10 (smurfs)
- PC3 → Fa0/2 → VLAN 20 (tom&jerry)

### Switch0(1)
- PC2 → Fa0/3 → VLAN 10 (smurfs)
- PC4 → Fa0/4 → VLAN 20 (tom&jerry)

## NOTE ## In this lab,VLAN 10(smurfs) represents the sales department and VLAN20(tom and jerry) represents the marketing department.

### Trunk Link

Switch0 Gi0/2 :left_right_arrow: Switch0(1) Gi0/2

---

## Step 1: Create VLANs on Both Switches

Open the Cisco 2960 Switch CLI and enter the following commands:

```cisco
enable
configure terminal

vlan 10
 name smurfs

vlan 20
 name tom&jerry

exit
write memory

show vlan brief
```

### Note

VLAN IDs 1–1001 can be created and used on a Cisco switch.

---

## Step 2: Assign Access Ports

### On Switch0

Configure Fa0/1 for VLAN 10:

```cisco
configure terminal

interface fa0/1
 switchport mode access
 switchport access vlan 10
exit
```

Configure Fa0/2 for VLAN 20:

```cisco
configure terminal

interface fa0/2
 switchport mode access
 switchport access vlan 20
exit
```

---

### On Switch0(1)

Configure Fa0/3 for VLAN 10:

```cisco
configure terminal

interface fa0/3
 switchport mode access
 switchport access vlan 10
exit
```

Configure Fa0/4 for VLAN 20:

```cisco
configure terminal

interface fa0/4
 switchport mode access
 switchport access vlan 20
exit
```

---

## Step 3: Verify VLAN Configuration

Run:

```cisco
show vlan brief
```

Expected Output:

```text
VLAN 10 (smurfs)      Fa0/1, Fa0/3
VLAN 20 (tom&jerry)   Fa0/2, Fa0/4
```

---

## Step 4: Configure Trunk Link

A trunk link allows multiple VLANs to travel between switches over a single cable.

### On Switch0

```cisco
configure terminal

interface gigabitEthernet0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown

exit
```

### On Switch0(1)

```cisco
configure terminal

interface gigabitEthernet0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown

exit
```

---

## Step 5: Verify Trunk Configuration

Run:

```cisco
show interfaces trunk
```

Expected Output:

```text
Port      Mode      Encapsulation   Status      Native VLAN
Gi0/2     on        802.1Q          trunking    1
```

Allowed VLANs:

```text
10,20
```

From the lab output:

```text
Vlans allowed on trunk: 1-1005
Vlans allowed and active in management domain: 1,10,20
Vlans in spanning tree forwarding state and not pruned: 1,10,20
```

---

## Step 6: Verify Interface Status

Run:

```cisco
show ip interface brief
```

From the lab output:

```text
FastEthernet0/1      up      up
FastEthernet0/2      up      up
FastEthernet0/3      up      up
FastEthernet0/4      up      up
GigabitEthernet0/2   up      up
Vlan1                administratively down
```

---

## Step 7: Testing

### Test 1 – Same VLAN Communication

Ping from:

```text
PC1 (VLAN 10) → PC2 (VLAN 10)
```

Result:

```text
Reply Success
```

This confirms that VLAN 10 traffic is successfully passing through the trunk link.

---

### Test 2 – Different VLAN Communication

Ping from:

```text
PC1 (VLAN 10) → PC4 (VLAN 20)
```

Result:

```text
Request Timed Out
```

Reason:

VLAN 10 and VLAN 20 are different broadcast domains. A Layer 2 switch cannot route traffic between VLANs. Inter-VLAN Routing is required.

---

## Commands Used

```cisco
show vlan brief
show interfaces trunk
show ip interface brief
```

---

## Conclusion



Successfully created VLAN 10 (smurfs) and VLAN 20 (tom&jerry), assigned switch ports to the required VLANs, configured trunking between Switch0 and Switch0(1), and verified communication between devices in the same VLAN across different switches.
Make a note of something
