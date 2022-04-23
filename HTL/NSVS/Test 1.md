###### 29.03.2022

## VLAN (802.1Q)
 - dot1q Norm
 - Trennung von lan und kabel
 - Es können über ein Kabel 2 LANS geführt werden.
 - wird an Switch/Router konfiguriert
 - Ist für den PC wie eine normale Netzwerkschnittstelle



> Der Router benötigt nun ==2 Default Gateways== da 2 Netzwerke an ihm hängen und bekommt deswegen 2 IP-Adressen. => Es werden aus dem einem physikalischem Interface 2 virtuelle Interfaces erstellt. 

![[Pasted_image_20220328071543.png]]
*Skizze zum Aufbau eines Systems mit 2 VLANS*


**Trunk**  -> die Leitung auf der die VLAN Nummer transportiert wird.

**GigabitEthernet 0/0** -> Normales Interface
**GigabitEthernet 0/0.1** -> Virtuell geteiltes Interface wird anders nummeriert

Verschiedene Arten der Interfaces -> [[CLI_interfaceTypes.pdf]]

---
<div style="display:flex; justify-content:center; width:100%;" ><span><b>The need for IPv6</b></span></div>

 - IPv4 Adresse sind begrentzt. Große Firmen können schon Probleme mit benötigter IPv6  Range bekommen
 - IPv4 und IPv6 Koexistieren zurzeit

**IPv4 Tunnel** 
- verbindet IPv6 Netzwerke
- transportiert IPv6
- IPv6 Paket wird enkapsuliert in IPv4 Paket 


**NAT-Router** --> Network Address Translation übersetzt IPv6 Adresse in IPv4 Adresse und umgekehrt


**IPv6 Representation**
1. 128 bits
2. Darstellung in hexadezimal
3. 4 bits -> one Digit
4. besteht aus 32 Digits / 16 bytes

![[Pasted_image_20220328075844.png]]
---

###### 04.04.2022
Hub ist ein dummer Switch
Flooding ist genau das was ein Hub macht. Wenn er an einem Interface etwas bekommt, sendet er es an alle anderen (vorrausgesetzt sie sind nicht down).

Ist etwas im ARP-Table werden die Eintraege verwendet. Wenn sie leer ist, muss angefragt werden(Er hat eine IP-Adresse und will die MAC Adresse herausfinden) 
Kann man anschauen mit **cmd -> arp -a**

#### Routing Ablauf

**Kommend**

|MAC/src|MAC/dest|IP/src|IP/dest|TTL|Data|
|-----|-----|-----|-----|-----|-----|
|prev Hop|seine Eigene|Sender|Empfaenger|TTL|Data|

**1.** **Mac destination check** (ob seine eigene oder nicht)
**2.** **TTL check**
**3.** **TTL --**
**4.** **IP -destination** -> Routing Table -> best match
**5.** **Egress Port** -> ist der ausgehende Port
**6.** wird gesendet MAC/src ist seine eigene
**7.** MAC/src -> holt er aus dem ARP-Table

**Gehend**

|MAC/src|MAC/dest|IP/src|IP/dest|TTL|Data|
|-----|-----|-----|-----|-----|-----|
|seine eigene|next Hop|Sender|Empfaenger|TTL - 1|Data|

Pseudocode for finding the best match:
```pseudocode
findMatch(destIp) {
  foreach zeile in routingTable {
    addr=mask(destIp,zeile.netmask)
	if(addr == zeile.netaddr)
	  return zeile.nextHop
  }
}
```

#### Übungsbeispiel