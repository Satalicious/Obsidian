##### SHUTDOWN / STARTUP
=> **shutdown** \<mode>
 \<mode>:
- normal: //default, alle Sitzungen müssen beendet sein
- transactional
- immediate
- abort
---
=> **startup** //startet DBMS
		1. Instanz erzeugen [create] [[Logfiles-Details.excalidraw]]
		2. Controlfile auslesen [mount] 
		3. Dateien öffnen [open]
---
