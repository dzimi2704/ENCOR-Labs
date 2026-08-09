# Cisco CCNP: Site-to-Site GRE Tunneling over eBGP Underlay

![Network Topology](topology.PNG)

Enterprise WAN mreža za spajanje HQ i Branch lokacija preko ISP-a koristeći eBGP za underlay, GRE tunel za overlay i OSPF za unutrašnji ruting.

---

### IP Adresiranje i AS Brojevi

| Uređaj | Interfejs | IP Adresa / Maska | Namena | AS Broj |
| :--- | :--- | :--- | :--- | :--- |
| **HQ-R1** | Gi0/0 | `198.51.100.1/30` | WAN ka ISP-u | **AS 65100** |
| | Gi0/1 | `10.1.0.1/24` | HQ LAN Gateway | |
| | Loopback0 | `1.1.1.1/32` | Router ID | |
| | **Tunnel1** | `172.16.0.1/30` | GRE Overlay Interfejs | |
| **ISP-R2** | Gi0/0 | `198.51.100.2/30` | Link ka HQ-R1 | **AS 65000** |
| | Gi0/1 | `203.0.113.2/30` | Link ka BR-R3 | |
| | Loopback0 | `2.2.2.2/32` | Router ID | |
| **BR-R3** | Gi0/0 | `203.0.113.1/30` | WAN ka ISP-u | **AS 65200** |
| | Gi0/1 | `10.2.0.1/24` | Branch LAN Gateway | |
| | Loopback0 | `3.3.3.3/32` | Router ID | |
| | **Tunnel1** | `172.16.0.2/30` | GRE Overlay Interfejs | |

---

### Configurations

Kompletne running-config fajlove za sve rutere možete pronaći u [Configs](./Configs) folderu.