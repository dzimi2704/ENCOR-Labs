# Mrežni Podsetnik (Cheatsheet) - ENCOR Lab

Ovaj dokument sadrži ključne komande korišćene za konfiguraciju redundanse i rutiranja u labu.

## 1. L3 EtherChannel (Između DSW-1 i DSW-2)
Koristili smo EtherChannel da spojimo dva linka u jedan logički radi veće propusne moći i redundanse.

```bash
interface range Gi0/0 - 1
 channel-group 1 mode active
 no switchport
 ip address 10.1.1.1 255.255.255.252  # (Primer za DSW-1)

#2. OSPF Konfiguracija OSPF omogućava ruterima i switchevima da automatski razmene rute.

 router ospf 1
 router-id 1.1.1.1
 network 10.0.0.0 0.255.255.255 area 0
 network 192.168.10.0 0.0.0.255 area 0
 passive-interface Gi0/2  # (Interfejs ka klijentima)


##3. HSRP (Gateway Redundansa) Podešeno na DSW switchevima kako bi klijenti uvek imali izlaz sa mreže čak i ako jedan switch padne.

 interface Vlan 10
 standby 10 ip 192.168.10.254
 standby 10 priority 110
 standby 10 preempt


#Automatizacija4. SSH za Automatizaciju (Python/Netmiko) Da bi Python skripta radila, ovi parametri su bili neophodni:

 hostname R1
ip domain-name lab.local
crypto key generate rsa (1024 bita)
user admin privilege 15 password cisco
line vty 0 4
 login local
 transport input ssh

