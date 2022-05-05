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

```c
Router# en
Router# conf t
Router#(config)ipv6 unicast-routing
Router#(config)int gig0/0
Router#(config-if)ipv6 addr 2a10:aac:4100:ff::2a 
```
![[Pasted image 20220502105633.png]]