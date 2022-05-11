## Das Meldesystem

#### Fehlermeldungen sind 
- Systemfehler
- Ereignisse aus Anwenderprogrammen


#### FEHLER, Zeitstempel
-  K ... kommt
-  G ... geht
-  R ... quittiert

#### => Speicher in eigenen Datenbaustein
 - Vielzahl Einzeldaten im DB => !! CHAOS !!
 - daher organisieren in Datentypen!

---
---

## HOW TO

=> eigenes System erstellen bei "PLC-Datentypen"
=> neuen Datenbaustein einfügen. Neue Variable erstellen mit dem Datentyp den wir vorher erstellt haben

Static  |  Datentyp
----          |          ----
Fehler | Array[1...10] of "Fehlermeldung"

**Wenn ein DB mit Datentyp verknüpft ist (anstatt GlobalDB den PLC-Datentypen auswählen), ändert sich der DB mit wenn die Datentypen sich verändern.**

---

![[Verschachtelung.jpg.png]]

=> weiters der Ablauf im Main:

1. Aufruf des übergeordneten FB's
	- INPUTS in den Instanz-DB eintragen (KOPIEREN)

1. Code ausführen
		1. statische verändern (werden <mark style="background: #FFF3A3A6;">in der Instanz</mark> verändert)
		2. externe (POINTER) verändern
		3. OUPUT verändern (werden <mark style="background: #FFF3A3A6;">in der Instanz</mark> verändert)
2. OUTPUTS
		-  von Instanz Zustände in die Variablen kopiert





