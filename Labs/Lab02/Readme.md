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
PC1> sh ip<br>
<br>
NAME        : PC1[1]<br>
IP/MASK     : 10.52.11.2/30<br>
GATEWAY     : 10.52.11.1<br>
DNS         :<br>
MAC         : 00:50:79:66:68:06<br>
LPORT       : 20000<br>
RHOST:PORT  : 127.0.0.1:30000<br>
MTU         : 1500<br>
</details>
<details>
<summary> PC2 </summary>
PC2> sh ip<br>
<br>
NAME        : PC2[1]<br>
IP/MASK     : 10.52.12.2/30<br>
GATEWAY     : 10.52.12.1<br>
DNS         :<br>
MAC         : 00:50:79:66:68:07<br>
LPORT       : 20000<br>
RHOST:PORT  : 127.0.0.1:30000<br>
MTU         : 1500<br>
</details>
<details>
<summary> PC3 </summary>
PC3> sh ip<br>
<br>
NAME        : PC3[1]<br>
IP/MASK     : 10.52.13.2/30<br>
GATEWAY     : 10.52.13.1<br>
DNS         :<br>
MAC         : 00:50:79:66:68:08<br>
LPORT       : 20000<br>
RHOST:PORT  : 127.0.0.1:30000<br>
MTU         : 1500<br>
</details>
<details>
<summary> PC4 </summary>
PC4> sh ip<br>
<br>
NAME        : PC4[1]<br>
IP/MASK     : 10.52.13.6/30<br>
GATEWAY     : 10.52.13.5<br>
DNS         :<br>
MAC         : 00:50:79:66:68:09<br>
LPORT       : 20000<br>
RHOST:PORT  : 127.0.0.1:30000<br>
MTU         : 1500<br>
