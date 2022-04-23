1. **LAN**: Ethernet, **Switching** (Flooding, learning, forwarding), **VLAN** (tagging(4byte) mode: access/trunk, Aufbau, Inter-VLAN Routing), **ARP**

2. **Routing**: Ein Beispiel loesen koennen (sind online). Routing Table: Network, SNM, Next Hop, den Routing best match Algorithm(z.B. 10 Ports -> es kommt eine IP-Adresse -> welcher Port wird gewaehlt), Frame to Router.

3. **IPv6** kommt nicht.



learning und forwarding muss ich noch in Flashkarten packen
VLAN Priority für jeden Frame extra oder für das gesamte VLAN konfiguriert??



# Lernen

### Ethernet IEEE 802.3:
Is an IEEE Protocol not actually the physical Connection between Pcs.


Am Data Link und Physical Layer des OSI Modells


**Different Ethernet Standards:**
| **Norm** | **Speed** | **Short** | **Medium**|
|--- | --- | --- | --- |
| 802.3 | 10 Mbps | | |
| 802.3u | 100 Mbps | FE | |
| 802.3z | 1000 Mbps | GE | Fiber |
| 802.3ab | 1000 Mbps | GE | Twisted Pair |
| 802.3ae | 10000 Mbps | 10GE | Fiber | 
| 802.3an | 10000 Mbps | 10GE | Twiste Pair |


### ARP

Die MAC Adresse lernen wir  durchs Adress Resolution Protocol

ARP agiert nur innerhalb eines Netzwerkes
ARP Table speichert welche IP-Adresse zu welcher MAC-Adresse gehört

### VLAN Tag
4 Byte
32 Bit


### Frame
Ein Frame ist ein weiter verpacktes Paket
Paket liegt  am Network Layer
Ein Frame liegt am Data Link Layer

Ein **Ethernet Frame** ist eine Data Layer Protocol Einheit und vererndet den Ethernet physical Layer Transport Mechanismus
Enthält die Source und Destination MAC-Adresse in den ersten zwei Feldern


### Layer 2
- MAC -> Medium Access Control
- Ethernet
- LAN Switching
	- Hub, Switch
	- VLAN

**Collision Domain** -> Eine Collision Domain ist der Teil eines Netzwerkes an dem ein collisino auftreten kann. Ein Collision passiert dann wenn 2 Devices gleichzeitig ein Paket an eine Collision Domain senden. Die 2 Pakete koolidieren und beide Devices müssen ihre Pakete erneut senden.
Collision treten oft in Hub Umgebungen auf da auf einem Hub jeder Port eine Collision Domain ist.
Um eine Collision Domain aufzulösen verwendet man einen Switch/Router da dort jeder Port eine eigene Domain.

### Inter VLAN Routing
VLANs sind Subnetze in einem Netzwerk
Um Kommunikation zwischen den einzelnen VLANs zu ermöglichen muss man den Router so konfigurieren, dass er Komunikationzwischen den VLANs zulässt.
Das einzelne Interface des Routers an dem die VLANS haengen wird das Interface in virtuelle Sub-Interfaces unterteilt.
Diese Sub-Interfaces sind die default gateways der einzelnen VLANs.
Jedes VLAN bekommt ein eigenes Sub-Interface.
Dies ermoeglicht die Kommunikation der VLANs ueber ein einziges Interface, sowie Kommunikation aus dem eingenem Netzwerk hinaus.
[[https://www.section.io/engineering-education/inter-vlan-routing/#what-is-inter-vlan-routing]]

### Switching
##### Forwarding