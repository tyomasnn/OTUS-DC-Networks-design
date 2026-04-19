### Построение Underlay сети с использованием протокола динамической маршрутизации OSPF

### Задание:
- 1: Спроектировать и настроить сегмент Underlay сети на базе протокола динамической маршрутизации OSPF

### В среде виртуализации EVE-NG cобрана и настроена топология Underlay сети Spine-Leaf с использованием протокола динамической маршрутизации OSPF на базе L3-коммутаторов Arista с подключенными к ней устройствами "PC" имитирующими потребителей сервиса:
![img_1.png](Topology-Lab02.png)

### IP план:
Device|Interface|IP Address|Subnet Mask
---|---|---|---
Spine1|Loopback0|10.52.0.1|/32
-|Ethernet1|10.52.1.0|/31
-|Ethernet2|10.52.1.2|/31
-|Ethernet3|10.52.1.4|/31
Spine2|Loopback0|10.52.0.2|/32
-|Ethernet1|10.52.2.0|/31
-|Ethernet2|10.52.2.2|/31
-|Ethernet3|10.52.2.4|/31
Leaf1|Loopback0|10.52.0.11|/32
-|Ethernet1|10.52.1.1|/31
-|Ethernet2|10.52.2.1|/31
-|Ethernet8|10.52.11.1|/30
Leaf2|Loopback0|10.52.0.12|/32
-|Ethernet1|10.52.1.3|/31
-|Ethernet2|10.52.2.3|/31
-|Ethernet8|10.52.12.1|/30
Leaf3|Loopback0|10.52.0.13|/32
-|Ethernet1|10.52.1.5|/31
-|Ethernet2|10.52.2.5|/31
-|Ethernet8|10.52.12.5|/30
PC1|eth0|10.52.11.2|/30
PC2|eth0|10.52.12.2|/30
PC3|eth0|10.52.13.2|/30
PC4|eth0|10.52.13.6|/30

### Конфигурация оборудования
<details>
<summary> Spine1 </summary>
Spine1#sh run<br>
! Command: show running-config<br>
! device: Spine1 (vEOS-lab, EOS-4.29.2F)<br>
!<br>
! boot system flash:/vEOS-lab.swi<br>
! no aaa root<br>
! transceiver qsfp default-mode 4x10G<br>
! service routing protocols model multi-agent<br>
! hostname Spine1<br>
! spanning-tree mode mstp<br>
! interface Ethernet1<br>
   description to Eth1 Leaf1<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.0/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet2<br>
   description to Eth1 Leaf2<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.2/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet3<br>
   description to Eth1 Leaf3<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.4/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet4<br>
! interface Ethernet5<br>
! interface Ethernet6<br>
! interface Ethernet7<br>
! interface Ethernet8<br>
! interface Loopback0<br>
   ip address 10.52.0.1/32<br>
   ip ospf area 0.0.0.0<br>
! interface Management1<br>
! ip routing<br>
! router ospf 1<br>
   router-id 10.52.0.1<br>
   max-lsa 12000<br>
! end<br>
</details>
<details>
<summary> Spine2 </summary>
Spine2#sh run<br>
! Command: show running-config<br>
! device: Spine2 (vEOS-lab, EOS-4.29.2F)<br>
!<br>
! boot system flash:/vEOS-lab.swi<br>
! no aaa root<br>
! transceiver qsfp default-mode 4x10G<br>
! service routing protocols model multi-agent<br>
! hostname Spine2<br>
! spanning-tree mode mstp<br>
! interface Ethernet1<br>
   description to Eth2 Leaf1<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.0/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet2<br>
   description to Eth2 Leaf2<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.2/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet3<br>
   description to Eth2 Leaf3<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.4/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet4<br>
! interface Ethernet5<br>
! interface Ethernet6<br>
! interface Ethernet7<br>
! interface Ethernet8<br>
! interface Loopback0<br>
   ip address 10.52.0.2/32<br>
   ip ospf area 0.0.0.0<br>
! interface Management1<br>
! ip routing<br>
! router ospf 1<br>
   router-id 10.52.0.2<br>
   max-lsa 12000<br>
! end<br>
</details>
<details>
<summary> Leaf1 </summary>
Leaf1#sh run<br>
! Command: show running-config<br>
! device: Leaf1 (vEOS-lab, EOS-4.29.2F)<br>
!<br>
! boot system flash:/vEOS-lab.swi<br>
! no aaa root<br>
! transceiver qsfp default-mode 4x10G<br>
! service routing protocols model multi-agent<br>
! hostname Leaf1<br>
! spanning-tree mode mstp<br>
! interface Ethernet1<br>
   description to Eth1 Spine1<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.1/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet2<br>
   description to Eth1 Spine2<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.1/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet3<br>
! interface Ethernet4<br>
! interface Ethernet5<br>
! interface Ethernet6<br>
! interface Ethernet7<br>
! interface Ethernet8<br>
   description to PC1<br>
   no switchport<br>
   ip address 10.52.11.1/30<br>
! interface Loopback0<br>
   ip address 10.52.0.11/32<br>
   ip ospf area 0.0.0.0<br>
! interface Management1<br>
! ip routing<br>
! router ospf 1<br>
   router-id 10.52.0.11<br>
   redistribute connected<br>
   max-lsa 12000<br>
! end<br>
</details>
<details>
<summary> Leaf2 </summary>
Leaf2#sh run<br>
! Command: show running-config<br>
! device: Leaf2 (vEOS-lab, EOS-4.29.2F)<br>
!<br>
! boot system flash:/vEOS-lab.swi<br>
! no aaa root<br>
! transceiver qsfp default-mode 4x10G<br>
! service routing protocols model multi-agent<br>
! hostname Leaf2<br>
! spanning-tree mode mstp<br>
! interface Ethernet1<br>
   description to Eth2 Spine1<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.3/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet2<br>
   description to Eth2 Spine2<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.3/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet3<br>
! interface Ethernet4<br>
! interface Ethernet5<br>
! interface Ethernet6<br>
! interface Ethernet7<br>
! interface Ethernet8<br>
   description to PC2<br>
   no switchport<br>
   ip address 10.52.12.1/30<br>
! interface Loopback0<br>
   ip address 10.52.0.12/32<br>
   ip ospf area 0.0.0.0<br>
! interface Management1<br>
! ip routing<br>
! router ospf 1<br>
   router-id 10.52.0.12<br>
   redistribute connected<br>
   max-lsa 12000<br>
! end<br>
</details>
<details>
<summary> Leaf3 </summary>
Leaf3#sh run<br>
! Command: show running-config<br>
! device: Leaf3 (vEOS-lab, EOS-4.29.2F)<br>
!<br>
! boot system flash:/vEOS-lab.swi<br>
! no aaa root<br>
! transceiver qsfp default-mode 4x10G<br>
! service routing protocols model multi-agent<br>
! hostname Leaf3<br>
! spanning-tree mode mstp<br>
! interface Ethernet1<br>
   description to Eth3 Spine1<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.1.5/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet2<br>
   description to Eth3 Spine2<br>
   mtu 9214<br>
   no switchport<br>
   ip address 10.52.2.5/31<br>
   ip ospf network point-to-point<br>
   ip ospf area 0.0.0.0<br>
! interface Ethernet3<br>
! interface Ethernet4<br>
! interface Ethernet5<br>
! interface Ethernet6<br>
! interface Ethernet7<br>
   description to PC3<br>
   no switchport<br>
   ip address 10.52.13.1/30<br>
! interface Ethernet8<br>
   description to PC4<br>
   no switchport<br>
   ip address 10.52.13.5/30<br>
! interface Loopback0<br>
   ip address 10.52.0.13/32<br>
   ip ospf area 0.0.0.0<br>
! interface Management1<br>
! ip routing<br>
! router ospf 1<br>
   router-id 10.52.0.13<br>
   redistribute connected<br>
   max-lsa 12000<br>
! end<br>
</details>
<details>
<summary> PC1 </summary>

 ```
PC1> sh ip

NAME        : PC1[1]
IP/MASK     : 10.52.11.2/30
GATEWAY     : 10.52.11.1
DNS         :
MAC         : 00:50:79:66:68:06
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```
</details>
<details>
<summary> PC2 </summary>
   
 ```
PC2> sh ip

NAME        : PC2[1]
IP/MASK     : 10.52.12.2/30
GATEWAY     : 10.52.12.1
DNS         :
MAC         : 00:50:79:66:68:07
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```
</details>
<details>
<summary> PC3 </summary>

 ```
PC3> sh ip<br>

NAME        : PC3[1]
IP/MASK     : 10.52.13.2/30
GATEWAY     : 10.52.13.1
DNS         :
MAC         : 00:50:79:66:68:08
LPORT       : 20000
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```
</details>
<details>
<summary> PC4 </summary>

 ```
PC4> sh ip

NAME        : PC4[1]
IP/MASK     : 10.52.13.6/30
GATEWAY     : 10.52.13.5
DNS         :
MAC         : 00:50:79:66:68:09
LPORT       : 20000<br>
RHOST:PORT  : 127.0.0.1:30000
MTU         : 1500
```
</details>

#### Диагностика Spine/Leaf

<details>
<summary> Spine1 diag </summary>
 
 ```
Spine1#sh ip route

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

Gateway of last resort is not set

 C        10.52.0.1/32 is directly connected, Loopback0
 O        10.52.0.2/32 [110/30] via 10.52.1.1, Ethernet1
                                via 10.52.1.3, Ethernet2
                                via 10.52.1.5, Ethernet3
 O        10.52.0.11/32 [110/20] via 10.52.1.1, Ethernet1
 O        10.52.0.12/32 [110/20] via 10.52.1.3, Ethernet2
 O        10.52.0.13/32 [110/20] via 10.52.1.5, Ethernet3
 C        10.52.1.0/31 is directly connected, Ethernet1
 C        10.52.1.2/31 is directly connected, Ethernet2
 C        10.52.1.4/31 is directly connected, Ethernet3
 O        10.52.2.0/31 [110/20] via 10.52.1.1, Ethernet1
 O        10.52.2.2/31 [110/20] via 10.52.1.3, Ethernet2
 O        10.52.2.4/31 [110/20] via 10.52.1.5, Ethernet3
 O E2     10.52.11.0/30 [110/1] via 10.52.1.1, Ethernet1
 O E2     10.52.12.0/30 [110/1] via 10.52.1.3, Ethernet2
 O E2     10.52.13.0/30 [110/1] via 10.52.1.5, Ethernet3
 O E2     10.52.13.4/30 [110/1] via 10.52.1.5, Ethernet3

Spine1#sh ip ospf interface
Loopback0 is up
  Interface Address 10.52.0.1/32, instance 1, VRF default, Area 0.0.0.0
  Network Type Broadcast, Cost: 10
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router is 10.52.0.1
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 0
  No authentication
  Traffic engineering is disabled
Ethernet2 is up
  Interface Address 10.52.1.2/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet1 is up
  Interface Address 10.52.1.0/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet3 is up
  Interface Address 10.52.1.4/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled

Spine1#sh ip ospf neighbor
Neighbor ID     Instance VRF      Pri State                  Dead Time   Address         Interface
10.52.0.12      1        default  0   FULL                   00:00:34    10.52.1.3       Ethernet2
10.52.0.11      1        default  0   FULL                   00:00:32    10.52.1.1       Ethernet1
10.52.0.13      1        default  0   FULL                   00:00:36    10.52.1.5       Ethernet3
```
</details>
<details>
<summary> Spine2 diag </summary>
 
 ```
Spine2#sh ip route

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

Gateway of last resort is not set

 O        10.52.0.1/32 [110/30] via 10.52.2.1, Ethernet1
                                via 10.52.2.3, Ethernet2
                                via 10.52.2.5, Ethernet3
 C        10.52.0.2/32 is directly connected, Loopback0
 O        10.52.0.11/32 [110/20] via 10.52.2.1, Ethernet1
 O        10.52.0.12/32 [110/20] via 10.52.2.3, Ethernet2
 O        10.52.0.13/32 [110/20] via 10.52.2.5, Ethernet3
 O        10.52.1.0/31 [110/20] via 10.52.2.1, Ethernet1
 O        10.52.1.2/31 [110/20] via 10.52.2.3, Ethernet2
 O        10.52.1.4/31 [110/20] via 10.52.2.5, Ethernet3
 C        10.52.2.0/31 is directly connected, Ethernet1
 C        10.52.2.2/31 is directly connected, Ethernet2
 C        10.52.2.4/31 is directly connected, Ethernet3
 O E2     10.52.11.0/30 [110/1] via 10.52.2.1, Ethernet1
 O E2     10.52.12.0/30 [110/1] via 10.52.2.3, Ethernet2
 O E2     10.52.13.0/30 [110/1] via 10.52.2.5, Ethernet3
 O E2     10.52.13.4/30 [110/1] via 10.52.2.5, Ethernet3

Spine2#sh ip osp interface
Loopback0 is up
  Interface Address 10.52.0.2/32, instance 1, VRF default, Area 0.0.0.0
  Network Type Broadcast, Cost: 10
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router is 10.52.0.2
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 0
  No authentication
  Traffic engineering is disabled
Ethernet1 is up
  Interface Address 10.52.2.0/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet2 is up
  Interface Address 10.52.2.2/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet3 is up
  Interface Address 10.52.2.4/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled

Spine2#sh ip osp nei
Neighbor ID     Instance VRF      Pri State                  Dead Time   Address         Interface
10.52.0.11      1        default  0   FULL                   00:00:38    10.52.2.1       Ethernet1
10.52.0.12      1        default  0   FULL                   00:00:29    10.52.2.3       Ethernet2
10.52.0.13      1        default  0   FULL                   00:00:30    10.52.2.5       Ethernet3
```
</details>
<details>
<summary> Leaf1 diag </summary>
 
 ```
Leaf1#sh ip route

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

Gateway of last resort is not set

 O        10.52.0.1/32 [110/20] via 10.52.1.0, Ethernet1
 O        10.52.0.2/32 [110/20] via 10.52.2.0, Ethernet2
 C        10.52.0.11/32 is directly connected, Loopback0
 O        10.52.0.12/32 [110/30] via 10.52.1.0, Ethernet1
                                 via 10.52.2.0, Ethernet2
 O        10.52.0.13/32 [110/30] via 10.52.1.0, Ethernet1
                                 via 10.52.2.0, Ethernet2
 C        10.52.1.0/31 is directly connected, Ethernet1
 O        10.52.1.2/31 [110/20] via 10.52.1.0, Ethernet1
 O        10.52.1.4/31 [110/20] via 10.52.1.0, Ethernet1
 C        10.52.2.0/31 is directly connected, Ethernet2
 O        10.52.2.2/31 [110/20] via 10.52.2.0, Ethernet2
 O        10.52.2.4/31 [110/20] via 10.52.2.0, Ethernet2
 C        10.52.11.0/30 is directly connected, Ethernet8
 O E2     10.52.12.0/30 [110/1] via 10.52.1.0, Ethernet1
                                via 10.52.2.0, Ethernet2
 O E2     10.52.13.0/30 [110/1] via 10.52.1.0, Ethernet1
                                via 10.52.2.0, Ethernet2
 O E2     10.52.13.4/30 [110/1] via 10.52.1.0, Ethernet1
                                via 10.52.2.0, Ethernet2

Leaf1#sh ip osp inter
Loopback0 is up
  Interface Address 10.52.0.11/32, instance 1, VRF default, Area 0.0.0.0
  Network Type Broadcast, Cost: 10
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router is 10.52.0.11
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 0
  No authentication
  Traffic engineering is disabled
Ethernet2 is up
  Interface Address 10.52.2.1/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet1 is up
  Interface Address 10.52.1.1/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled

Leaf1#sh ip osp nei
Neighbor ID     Instance VRF      Pri State                  Dead Time   Address         Interface
10.52.0.2       1        default  0   FULL                   00:00:36    10.52.2.0       Ethernet2
10.52.0.1       1        default  0   FULL                   00:00:35    10.52.1.0       Ethernet1
```
</details>
<details>
<summary> Leaf2 diag </summary>
 
 ```
Leaf2#sh ip route

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

Gateway of last resort is not set

 O        10.52.0.1/32 [110/20] via 10.52.1.2, Ethernet1
 O        10.52.0.2/32 [110/20] via 10.52.2.2, Ethernet2
 O        10.52.0.11/32 [110/30] via 10.52.1.2, Ethernet1
                                 via 10.52.2.2, Ethernet2
 C        10.52.0.12/32 is directly connected, Loopback0
 O        10.52.0.13/32 [110/30] via 10.52.1.2, Ethernet1
                                 via 10.52.2.2, Ethernet2
 O        10.52.1.0/31 [110/20] via 10.52.1.2, Ethernet1
 C        10.52.1.2/31 is directly connected, Ethernet1
 O        10.52.1.4/31 [110/20] via 10.52.1.2, Ethernet1
 O        10.52.2.0/31 [110/20] via 10.52.2.2, Ethernet2
 C        10.52.2.2/31 is directly connected, Ethernet2
 O        10.52.2.4/31 [110/20] via 10.52.2.2, Ethernet2
 O E2     10.52.11.0/30 [110/1] via 10.52.1.2, Ethernet1
                                via 10.52.2.2, Ethernet2
 C        10.52.12.0/30 is directly connected, Ethernet8
 O E2     10.52.13.0/30 [110/1] via 10.52.1.2, Ethernet1
                                via 10.52.2.2, Ethernet2
 O E2     10.52.13.4/30 [110/1] via 10.52.1.2, Ethernet1
                                via 10.52.2.2, Ethernet2

Leaf2#sh ip osp int
Loopback0 is up
  Interface Address 10.52.0.12/32, instance 1, VRF default, Area 0.0.0.0
  Network Type Broadcast, Cost: 10
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router is 10.52.0.12
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 0
  No authentication
  Traffic engineering is disabled
Ethernet2 is up
  Interface Address 10.52.2.3/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet1 is up
  Interface Address 10.52.1.3/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled

Leaf2#sh ip osp nei
Neighbor ID     Instance VRF      Pri State                  Dead Time   Address         Interface
10.52.0.2       1        default  0   FULL                   00:00:30    10.52.2.2       Ethernet2
10.52.0.1       1        default  0   FULL                   00:00:35    10.52.1.2       Ethernet1
```
</details>
<details>
<summary> Leaf3 diag </summary>
 
 ```
Leaf3#sh ip route

VRF: default
Codes: C - connected, S - static, K - kernel,
       O - OSPF, IA - OSPF inter area, E1 - OSPF external type 1,
       E2 - OSPF external type 2, N1 - OSPF NSSA external type 1,
       N2 - OSPF NSSA external type2, B - Other BGP Routes,
       B I - iBGP, B E - eBGP, R - RIP, I L1 - IS-IS level 1,
       I L2 - IS-IS level 2, O3 - OSPFv3, A B - BGP Aggregate,
       A O - OSPF Summary, NG - Nexthop Group Static Route,
       V - VXLAN Control Service, M - Martian,
       DH - DHCP client installed default route,
       DP - Dynamic Policy Route, L - VRF Leaked,
       G  - gRIBI, RC - Route Cache Route

Gateway of last resort is not set

 O        10.52.0.1/32 [110/20] via 10.52.1.4, Ethernet1
 O        10.52.0.2/32 [110/20] via 10.52.2.4, Ethernet2
 O        10.52.0.11/32 [110/30] via 10.52.1.4, Ethernet1
                                 via 10.52.2.4, Ethernet2
 O        10.52.0.12/32 [110/30] via 10.52.1.4, Ethernet1
                                 via 10.52.2.4, Ethernet2
 C        10.52.0.13/32 is directly connected, Loopback0
 O        10.52.1.0/31 [110/20] via 10.52.1.4, Ethernet1
 O        10.52.1.2/31 [110/20] via 10.52.1.4, Ethernet1
 C        10.52.1.4/31 is directly connected, Ethernet1
 O        10.52.2.0/31 [110/20] via 10.52.2.4, Ethernet2
 O        10.52.2.2/31 [110/20] via 10.52.2.4, Ethernet2
 C        10.52.2.4/31 is directly connected, Ethernet2
 O E2     10.52.11.0/30 [110/1] via 10.52.1.4, Ethernet1
                                via 10.52.2.4, Ethernet2
 O E2     10.52.12.0/30 [110/1] via 10.52.1.4, Ethernet1
                                via 10.52.2.4, Ethernet2
 C        10.52.13.0/30 is directly connected, Ethernet7
 C        10.52.13.4/30 is directly connected, Ethernet8

Leaf3#sh ip osp int
Loopback0 is up
  Interface Address 10.52.0.13/32, instance 1, VRF default, Area 0.0.0.0
  Network Type Broadcast, Cost: 10
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router is 10.52.0.13
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 0
  No authentication
  Traffic engineering is disabled
Ethernet2 is up
  Interface Address 10.52.2.5/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled
Ethernet1 is up
  Interface Address 10.52.1.5/31, instance 1, VRF default, Area 0.0.0.0
  Network Type Point-To-Point, Cost: 10
  Transmit Delay is 1 sec, State P2P
  Interface Speed: 1000 mbps
  No Designated Router on this network
  No Backup Designated Router on this network
  Timer intervals configured, Hello 10, Dead 40, Retransmit 5
  Neighbor Count is 1
  No authentication
  Traffic engineering is disabled

Leaf3#sh ip osp nei
Neighbor ID     Instance VRF      Pri State                  Dead Time   Address         Interface
10.52.0.2       1        default  0   FULL                   00:00:34    10.52.2.4       Ethernet2
10.52.0.1       1        default  0   FULL                   00:00:32    10.52.1.4       Ethernet1
```
</details>

#### Проверка наличия IP связности между устройствами "PC" имитирующими потребителей сервиса подключенных к портам Leaf-ов OSPF домена:

<details>
 
```
PC1> ping 10.52.12.2

84 bytes from 10.52.12.2 icmp_seq=1 ttl=61 time=101.051 ms

PC1> ping 10.52.13.2

84 bytes from 10.52.13.2 icmp_seq=1 ttl=61 time=74.793 ms

PC1> ping 10.52.13.6

84 bytes from 10.52.13.6 icmp_seq=1 ttl=61 time=59.598 ms

PC2> ping 10.52.13.2

84 bytes from 10.52.13.2 icmp_seq=1 ttl=61 time=37.102 ms

PC2> ping 10.52.13.6

84 bytes from 10.52.13.6 icmp_seq=1 ttl=61 time=32.166 ms

PC3> ping 10.52.13.6

84 bytes from 10.52.13.6 icmp_seq=1 ttl=63 time=18.671 ms

```
</details>
