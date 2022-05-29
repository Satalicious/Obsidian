[[VLAN]]
[[SNM Table]]
```c
Router# en
Router# conf t
Router#(config)ipv6 unicast-routing
Router#(config)int gig0/0
Router#(config-int)ipv6 enable
strg+c
strg+c
Router# show ipv6 int gig0/0
```
![[Pasted image 20220502101632.png]]

---
#### global unicast zuweisen mit prefix 
#### => 2a10:aac:4100:ff
**(führenden Nullen werden weggelassen, eigentlich
=> 2a10:0aac:4100:00ff)**


---

#### Interface ID
#### 2a10:aac:4100:ff + ::2a <mark style="background: #FF5582A6;">/64</mark> 
(**128 ist Länge von IPV6, Hälfte ist 64 - Grenze zwischen Netz & Host**)

![[Pasted image 20220502105633.png]]

---

### ipv6 Routing:
![[Pasted image 20220516111027.png]]
1. **Bei beiden Routern!**
- unicast-routing enablen
-  interface auswählen - ipv6 enable - ipv6 addr zuweisen
```c
Router1# en
Router1# conf t
Router1#(config)ipv6 unicast-routing
Router1#(config)int fa0/1
Router1#(config-int)ipv6 enable
Router1#(config-if)ipv6 addr 2001:DB:A:F::2B/64 
```
Danach beim rechten Netzwerk folgender Befehl:
![[Pasted image 20220516110323.png]]
**ipv6 route Netzwerkaddr/64 + GlobalUnicast von nexthop**

---

#### IPv6 Konfigurationscheckliste
- [ ] Alle End-Geräte sollten vollständig konfiguriert werden 

![[Pasted image 20220527210702.png]]
![[Pasted image 20220527210805.png]]

*Nun dürfen Link Local und DNS Server leer sein. Link Local wird später automatisch konfiguriert.*
*Default Gateway: Nimme immer die oberste Adresse (z.B. 2000::1)*

- [ ]  Alle Routers sollten auch vollständig konfiguriert werden:
	- [ ] Zuerste sollten ipv6 an ==aller Routers== aktiviert (`ipv6 unicast-routing`) ==!! sehr wichtig !!== 
	- [ ] Alle betätigte (occupied/ active) Interfaces sollten mit `no shut` oder auf dem GUI mit Port on konfiguriert:
	
	![[Pasted image 20220527211531.png]]
	
	*Auf dem CLI:*
```
Router>en
Router#config t
Router(config)#int fa0/1
Router(config-if)#no shut
...
```

- [ ] Weise die Default Gateway Adressen dieser betätigten zu
- [ ] Für Point-to-Point Netzteil, weise die ipv6 Adressen dieser Interfaces zu

*Auf dem CLI:*
```
Router(config)#int fa0/1
Router(config)#ipv6 addr [Adresse/64]
```

- [ ] Wenn alle Netzwerke konfiguriert wurden, sollten die Routing-Tabellen auch vollständig ausgefüllt werden (für alle Routers).
```
Router(config)#ipv6 route [Ziel-Netzwerk Adresse/64] [Next Hop (ohne subnetmask)]
```

*Dieser Befehl funktioniert nur auf (config), nicht auf (config-int)*

- [ ] Wenn ein Gerät mit einem Port an einem Router direkt verbunden wird, aber das Interface akzeptiert keine ipv6 Adresse
Beispiel:

![[Pasted image 20220527213753.png]]

Eine ipv6 Adresse kann nicht dem Interface Fa0/0/0 zugewiesen werden:

![[Pasted image 20220527214049.png]]

- [ ] oder wenn es 2+ Geräte in einem LAN gibt die mit mehrerer Ports an einem Router direkt verbunden werden
Beispiel:

![[Pasted image 20220527214209.png]]

- [ ] dann braucht man ==unbedingt== ein VLAN
```
Router(config)#interface vlan 1
Router(config-if)#no shut
Router(config-if)#ipv6 addr [Default Gateway Adresse kommt hier]
```

- [ ] Wenn eine IP-Adresse einem Port/ Interface falsch zugewiesen wird, kann man so korrigieren:
```
Router(config)#int [interface mit falscher ip-adresse]
Router(config-if)#no ip address
```

für ipv6 Adressen, braucht man nur `no ipv6 address` statt `no ip address` zu tippen.


![[Pasted image 20220529141809.png]]
Router links: 
ipv6 route ::0/0 2001:A:A:B::2
![[Pasted image 20220529142951.png]]
Router rechts:
![[Pasted image 20220529143413.png]]