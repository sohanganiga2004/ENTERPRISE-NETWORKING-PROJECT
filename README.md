# ENTERPRISE-NETWORKING-PROJECT
# Network Configuration Overview  ##


## Technologies Implemented

1. **Creating a Network Topology using Cisco Packet Tracer**
2. **Hierarchical Network Design**
3. **Connecting Networking Devices with Correct Cabling**
4. **Configuring Basic Device Settings**
5. **Creating VLANs and Assigning Ports VLAN Numbers**
6. **Subnetting and IP Addressing**
7. **Configuring Inter-VLAN Routing on the Multilayer Switches (Switch Virtual Interface)**
8. **Configuring a Dedicated DHCP Server Device to Provide Dynamic IP Allocation**
9. **Configuring SSH for Secure Remote Access**
10. **Configuring OSPF as the Routing Protocol**
11. **Configuring NAT Overload (Port Address Translation - PAT)**
12. **Configuring Standard and Extended Access Control Lists (ACL)**
13. **Configuring Switchport Security (Port-Security) on the Switches**
14. **Configuring WLAN or Wireless Network (Cisco Access Point)**
15. **Host Device Configurations**
16. **Configuring ISP Routers**
17. **Configuring BGP (Border Gateway Protocol)**
18. **Testing and Verifying Network Communication**




```markdown
# CORE SW1 Configuration

## General Configuration

```plaintext
hostname core-sw1
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

ip domain name sohan

username admin password cisco
crypto key generate rsa
line vty 0 15
  1024
  login local
  transport input ssh
ip ssh version 2
```

## Interface Configuration

```plaintext
show cdp neighbor

interface range gig1/0/3-8
 switchport encapsulation dot1Q
 switchport mode trunk

vtp domain sohan
```

## VLAN Configuration

```plaintext
vlan 10
 name sales
vlan 20
 name hr
vlan 30
 name finance
vlan 40
 name admin
vlan 50
 name ict
vlan 60
 name server
```

## IP and Interface Addressing

```plaintext
interface range gig1/0/1-2
 no switchport

interface gig1/0/1
 ip address 172.16.3.145 255.255.255.252
 no shutdown

interface gig1/0/2
 ip address 172.16.3.149 255.255.255.252
 no shutdown

ip routing
```

## OSPF Configuration

```plaintext
router ospf 10
 router-id 2.2.2.2
 network 172.16.1.0 0.0.0.127 area 0
 network 172.16.1.128 0.0.0.127 area 0
 network 172.16.2.0 0.0.0.127 area 0
 network 172.16.2.128 0.0.0.127 area 0
 network 172.16.3.0 0.0.0.127 area 0
 network 172.16.3.128 0.0.0.15 area 0
 network 172.16.3.144 0.0.0.3 area 0
 network 172.16.3.148 0.0.0.3 area 0
```

## VLAN Interface Configuration

```plaintext
interface vlan 10
 no shutdown
 ip address 172.16.1.1 255.255.255.128
 ip helper-address 172.16.3.130

interface vlan 20
 no shutdown
 ip address 172.16.1.129 255.255.255.128
 ip helper-address 172.16.3.130

interface vlan 30
 no shutdown
 ip address 172.16.2.1 255.255.255.128
 ip helper-address 172.16.3.130

interface vlan 40
 no shutdown
 ip address 172.16.2.129 255.255.255.128
 ip helper-address 172.16.3.130

interface vlan 50
 no shutdown
 ip address 172.16.3.1 255.255.255.128
 ip helper-address 172.16.3.130

interface vlan 60
 no shutdown
 ip address 172.16.3.129 255.255.255.240
 ip helper-address 172.16.3.130
```

## Static Routing

```plaintext
ip route 0.0.0.0 0.0.0.0 gig1/0/1
ip route 0.0.0.0 0.0.0.0 gig1/0/2
```
```

---




```markdown
# CORE SW2 Configuration

## General Configuration

```plaintext
hostname core-sw2
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

ip domain name sohan
username admin password cisco
crypto key generate rsa
  1024
line vty 0 15
  login local
  transport input ssh
ip ssh version 2
```

## Interface Configuration

```plaintext
show cdp neighbor

interface range gig1/0/3-8
 switchport encapsulation dot1Q
 switchport mode trunk

interface range gig1/0/1-2
 no switchport

interface gig1/0/1
 ip address 172.16.3.157 255.255.255.252
 no shutdown

interface gig1/0/2
 ip address 172.16.3.153 255.255.255.252
 no shutdown
```

## IP Routing and OSPF Configuration

```plaintext
ip routing

router ospf 10
 router-id 1.1.1.1
 network 172.16.1.0 0.0.0.127 area 0
 network 172.16.1.128 0.0.0.127 area 0
 network 172.16.2.0 0.0.0.127 area 0
 network 172.16.2.128 0.0.0.127 area 0
 network 172.16.3.0 0.0.0.127 area 0
 network 172.16.3.128 0.0.0.15 area 0
 network 172.16.3.152 0.0.0.3 area 0
 network 172.16.3.156 0.0.0.3 area 0
```

## Static Routing

```plaintext
ip route 0.0.0.0 0.0.0.0 gig1/0/1
ip route 0.0.0.0 0.0.0.0 gig1/0/2
```
```

```markdown
# Access Switch Configurations

## ASW1 Configuration

```plaintext
hostname asw1
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 10

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99
```

## ASW2 Configuration

```plaintext
hostname asw2
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 20

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99
```

## ASW3 Configuration

```plaintext
hostname asw3
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 30

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99

interface range fa0/3-24
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
 do show port-security

interface fa0/4
 no switchport port-security
 no switchport port-security maximum 1
 no switchport port-security mac-address sticky
 no switchport port-security violation shutdown
```

## ASW4 Configuration

```plaintext
hostname asw4
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 40

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99
```

## ASW5 Configuration

```plaintext
hostname asw5
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 50

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99
```

## ASW6 Configuration

```plaintext
hostname asw6
banner motd #NO Unauthorized Access!!!#
no ip domain lookup

line console 0
 password cisco
 login
exit

enable password cisco

service password-encryption

interface range fa0/3-5
 switchport access vlan 60

vlan 99
 name blackhole

interface range gig0/1-2
 switchport access vlan 99
```
```
