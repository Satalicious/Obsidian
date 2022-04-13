### DATA_DICTIONARY

==Menge von Inforamtionen über den Inhalt des Datenbestands==
- Datenbankobjekte
	-- Tabelle
	-- Indizes
	-- Views
	-- Procedures, Functions
	-- Sequences
	-- Trigger
	-- User, Privilegien
	-- ...
	
=> DBA_OBJECTS			... "Sammelstelle" aller DB Einträge
	- DESC DBA_OBJECTS

=> DBA_TABLES
	- DESC DBA_TABLES

##### Hierarchie der DD Inforamtionen
		
DBA_xxx				... gehört dem DBA
							Zugriff nur dem DBA möglich
					
ALL_xxx				... Menge auf die ich (als aktueller User) Zugriff habe
							gehört mir nicht notwendigerweise, Zugriff wurde aber erlaubt
					
USER_xxx			... Menge die mir gehört (als aktueller user)


**Infos über Tabellen?**
	gibt es im DD: DBA_TABLES
	
**EXTENT SEGMENT TABLESPACE DATAFILE**

Logische Verwaltung der DB - Objekte (welche der Speicher benötigt)
	- TABLESPACE 			... Menge der log. zusammengehörenden DB Objekte
		- SEGMENT			... einzelnes DB Objekt (Tabelle)
			- EXTENT		... Teil einer Tabelle, in einem Datenfile
