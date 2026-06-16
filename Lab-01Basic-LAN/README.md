#Lab-01: Basic lan connection with switch, router, pc, server, laptop.                           
Cisco Packet Tracer | CCNA Practical | Cyber Security |Soc Analyst

File: 1st time pc and switch and router configuration.pkt
By: Nasrathshaik
Date: October 2026
TOPOLOGY
Devices: Router4, Switch0, PC0, Laptop0, PC1, Server0
Status: All links green = Physical connectivity successful
OBJECTIVE
1. Build a basic LAN with 1 Router + 1 Switch + 4 End devices
2. Configure Router4 as default gateway 
3. Apply security: Console, Enable secret, Telnet
4. Test with ping and telnet
IP ADDRESSING
Router4 Fa0/0  = 192.168.1.1
PC0            = 192.168.1.10
Laptop0        = 192.168.1.11  
PC1            = 192.168.1.12
Server0        = 192.168.1.13
Subnet: 255.255.255.0
ROUTER4 CONFIG COMMANDS
enable
conf t
hostname Router4
interface fa0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit
enable secret cisco123
line console 0
 password console123
 login
exit
line vty 0 4
 password telnet123
 login
 transport input telnet
end
write memory
VERIFICATION
1. PC0>ping 192.168.1.1 = Success
2. PC0>telnet 192.168.1.1 = Working
3. show ip interface brief = Fa0/0 up/up
KEY LEARNINGS
1. no shutdown is mandatory
2. login is needed after password
3. Always write memory to save.
