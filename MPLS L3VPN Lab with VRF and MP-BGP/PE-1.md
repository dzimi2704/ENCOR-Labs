version 15.6
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname PE-1
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
ethernet lmi ce
!
!
!
mmi polling-interval 60
no mmi auto-configure
no mmi pvc
mmi snmp-timeout 180
!
!
!
!
!
no ip icmp rate-limit unreachable
!
!
!
ip vrf CLIENT_A
 rd 100:1
 route-target export 100:1
 route-target import 100:1
!
!
!
!
no ip domain lookup
ip cef
no ipv6 cef
!
multilink bundle-name authenticated
!
!
!
!
!
redundancy
!
no cdp log mismatch duplex
!
ip tcp synwait-time 5
!
!
!
!
!
!
!
!
!
!
!
!
!
interface Loopback0
 ip address 1.1.1.1 255.255.255.255
!
interface GigabitEthernet0/0
 ip vrf forwarding CLIENT_A
 ip address 192.168.10.1 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/1
 ip address 172.16.11.1 255.255.255.252
 duplex auto
 speed auto
 media-type rj45
 mpls label protocol ldp
 mpls ip
!
interface GigabitEthernet0/2
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
interface GigabitEthernet0/3
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
!
router ospf 1
 network 1.1.1.1 0.0.0.0 area 0
 network 172.16.11.0 0.0.0.3 area 0
!
router bgp 100
 bgp log-neighbor-changes
 neighbor 3.3.3.3 remote-as 100
 neighbor 3.3.3.3 update-source Loopback0
 !
 address-family vpnv4
  neighbor 3.3.3.3 activate
  neighbor 3.3.3.3 send-community both
 exit-address-family
 !
 address-family ipv4 vrf CLIENT_A
  redistribute connected
  redistribute static
 exit-address-family
!
ip forward-protocol nd
!
!
no ip http server
no ip http secure-server
ip route vrf CLIENT_A 10.1.1.0 255.255.255.0 192.168.10.2
!
!
!
!
control-plane
!
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 4
 login
 transport input none
!
no scheduler allocate
!
end
