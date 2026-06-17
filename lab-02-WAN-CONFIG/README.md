# WAN Connectivity Configuration using Cisco Packet Tracer
## Objective
To establish WAN connectivity between Hyderabad and Chennai branch offices using Serial DCE/DTE links and configure both Static Routing and Dynamic Routing (RIPv2).
## Network Topology
- Hyderabad Router
- Chennai Router
- 2 Switches
- 2 PCs
- Serial WAN Link
  ## Instructions
Router-Router-Cross Cable
Router-Switch-PC-Straight Cable

## LAN Configuration

### Hyderabad LAN
IP Address: 192.168.10.1/24

### Chennai LAN
IP Address: 192.168.20.1/24

## WAN Configuration

### Hyderabad Router (DTE)
IP: 172.16.0.1/30
Encapsulation: PPP

### Chennai Router (DCE)
IP: 172.16.0.2/30
Encapsulation: PPP
Clock Rate: 64000

## Static Routing

### Hyderabad Router
ip route 192.168.20.0 255.255.255.0 172.16.0.2
## Verification Commands
show ip route or show ip route static
ping 192.168.20.10
telnet 172.16.0.2

### Chennai Router
ip route 192.168.10.0 255.255.255.0 172.16.0.1
## Verification Commands
show ip route or show ip route static
ping 192.168.10.10
telnet 172.16.0.1

## Dynamic Routing (RIPv2)

### Hyderabad Router
router rip
version 2
network 192.168.10.0
network 172.16.0.0
no auto-summary

### Chennai Router
router rip
version 2
network 192.168.20.0
network 172.16.0.0
no auto-summary

## Verification Commands
show ip interface brief
show ip route
ping 172.16.0.2
ping 192.168.20.10

## Result
Successfully established WAN connectivity between Hyderabad and Chennai networks using PPP, Static Routing, and RIPv2 Dynamic Routing in Cisco Packet Tracer.

## Tools Used
- Cisco Packet Tracer
- Router
- Switch
- PCs
- Serial DCE/DTE Cable
