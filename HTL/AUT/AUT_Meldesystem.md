## Das Meldesystem

#### Fehlermeldungen sind 
- Systemfehler
- Ereignisse aus Anwenderprogrammen


#### FEHLER, Zeitstempel
	- K ... kommt
	- G ... geht
	- R ... quittiert

#### => Speicher in eigenen Datenbaustein
 - Vielzahl Einzeldaten im DB => !! CHAOS !!
 - daher organisieren in Datentypen!

---
---

## HOW TO

> => eigenes System erstellen bei "PLC-Datentypen"
=> neuen Datenbaustein einfügen. Neue Variable erstellen mit dem Datentyp den wir vorher erstellt haben

<br>

Static  |  Datentyp
----          |          ----
Fehler | Array[1...10] of "Fehlermeldung"


**Wenn ein DB mit Datentyp verknüpft ist (anstatt GlobalDB den PLC-Datentypen auswählen), ändert sich der DB mit wenn die Datentypen sich verändern.**
<br>

