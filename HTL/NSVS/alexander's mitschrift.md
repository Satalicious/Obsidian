### IPV4
Cross-over Kabel zwischen Router und Router und Switch und Switch

1.      Alle Ports einschalten die benutzt werden

2.      IP Adressen laut Angabe für Geräte zuweisen und Default-Gateway eintragen

3.      Default Gateway bei Router eintragen

4.      Routingtable einrichten

5.      VLAN einrichten

a.       Die Verbindungen auf Access und Trunk einstellen

b.      Mit CLI VLAN auf gewünschten Port einstellen

##### Bsp. fastEthernet 0/1

In Config gehen

è Interface fastEthernet0/1.1

è Subnetz wird erstellt

è encapsulation dot1q 2(gewünschte ID vergeben)

è Mit -> ip address  (ip address) (submask)  eintragen (Default gateway)

è Mit no shutdown abschließen

VLAN einrichten (bei Ports an denen man keine Adressen vergeben kann)

In Router config gehen

Interface vlan 1(ID)

Mit -> ip address  (ip address) (submask)  eintragen

Und mit -> no shutdown abschließen

#### IPV6
**Router:**

router> enable

router# conf t

router(config) ipv6 unicast-routing                  allg. IPV6 freischalten

router(config) interface fas0/0                                  port auswählen

router(config if) ipv6 enable                               beim port ipv6 freischalten            

router(config if) ipv6 address FE80::1 link-local (link-local beim Gerät(Laptop, etc.) eingeben)

router(config if) ipv6 address 2001:DB:A:E::1/64 (dem port die Adresse zuweisen. Bzw.default gateway einstellen)

router(config) no ip domain-lookup (WTF...??)

router(config if) no ipv6 address 2001:DB:A:E::1/64 (Wenn ip falsch)

router(config): ipv6 route 2001:DB:A:E::/64 2001:DB:A:B::1

 (Routingtable erstellen!! (::/0 => 0.0.0.0))

===============================================================================

Falls fa 0/0/0 port ausgewählt:

router(config) interface vlan 1

router(config if) ipv6 address 2001:DB:A:F::1/64 (dem port die Adresse zuweisen. Bzw.default gateway einstellen)

router(config if) no shutdown

===============================================================================

sprung zurück = exit              

router# sh run                                                        nur zum kontrollieren der Einstellungen