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
