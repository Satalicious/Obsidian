# ORACLE SETUP

### Wie startet man Oracle DBMS?
=> OracleServiceXE starten
=> sqlplus [cmd]			
=> mit dem user SYS anmelden (User der Oracle installiert hat)
		/ as sysdba
=> mit dem user SYSTEM anmelden		// fast so viele Rechte wie der SYS
		connect System
		
```SQL
SHOW user;                  ... Anzeige des aktuellen Users
```

---

## SHUTDOWN / STARTUP
=> **shutdown** \<mode>
 \<mode>:
- normal: //default, alle Sitzungen müssen beendet sein
- transactional
- immediate
- abort
---
=> **startup** //startet DBMS
		1. Instanz erzeugen [create]
		2. Controlfile auslesen [mount]
		3. Dateien öffnen [open]

---

