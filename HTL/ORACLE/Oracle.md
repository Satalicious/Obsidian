
### How to Setup/Start Oracle: [[Oracle Setup]]
Quick Help: https://docs.oracle.com/cd/F49540_01/DOC/server.815/a66735.pdf
SQL Quieres: [[SQL Basics]]

---

[[Data Dictionary]]

[[Tablespaces]]

[[User Management]]

[[ControlFile]]

[[Docki's Unterlagen.pdf]]

---
---

> wieviel DB-Objekte besitzt jeder User?
```SQL
SELECT owner, count(*) as "DB Objekte"
	FROM DBA_OBJECTS
		GROUP BY owner
		ORDER BY 2 DESC;
```
===============================================
> Wieviele Typen von DB Objekten (object_types) gibt es?
```SQL
SELECT object_type, count(*)
		FROM DBA_OBJECTS
			GROUP BY object_type
				ORDER BY 2 DESC;
```
===============================================
> wieviele DB Objekte gibt es, deren Namen mit DBA_ beginnt?
```SQL
SELECT count(*)
	FROM DBA_OBJECTS
		WHERE object_name LIKE 'DBA_%';
```
===============================================
> Welche Tabellen benötigen mehr als eine Datei?
```sql
SELECT segment_name, count(*)
	FROM DBA_EXTENTS
		WHERE segment_type = 'TABLE'
			GROUP BY segment_name
				HAVING count(DISTINCT file_id) > 1
```
===============================================
> Welchem Benutz gehören die meisten Tabellen?
```SQL 
SELECT owner, count(*) as "Tableanzahl"
	FROM DBA_TABLES
		GROUP BY owner
			HAVING count(*) >= ALL(SELECT count(*) 
			FROM DBA_TABLES GROUP BY owner);
```
### ODER 
```SQL
SELECT owner, count(*) as "Tableanzahl"
	FROM DBA_TABLES
		GROUP BY owner
			HAVING count(*) = (SELECT max(count(*)) 
			FROM DBA_TABLES GROUP BY owner);
```
===============================================
> Wieviele Tabellen gehören dem User 'HR'?
```SQL
SELECT count(*) 
	FROM DBA_TABLES 
		WHERE OWNER = 'HR';
```
===============================================
> Alle Tables selecten auf die ich als jetziger User zugriff habe
```SQL
SELECT TABLE_NAME FROM USER_TABLES ORDER BY 1;
```
==============================================


>Welche Datenobjekttypen benötigen keine Einträge in DATA_FILES?
```sql
SELECT DISTINCT segment_name
FROM DBA_SEGMENTS
WHERE segment_name NOT IN (SELECT segment_name FROM DBA_EXTENTS);
```
---
> Welche DB Objekte kommen, sind keine Segmente?
```sql
SELECT DISTINCT object_type
FROM DBA_OBJECTS
WHERE object_name NOT INT (SELECT segment_name FROM DBA_SEGMENTS);
```

**=> Ergebnis: alle _gewöhnlichen_ DB-Objekte benötigen schon Dateispeicher (EXTENTS -> FILE_ID)
es gibt aber besondere DB-Objekte von Oracle ohne EXTENTS!**


===============================================
> In wievielen Tablespaces werden meine Tabellen verwaltet?
```SQL
SELECT tablespace_name
	FROM USER_TABLES
	GROUP BY tablespace_name;

```
---
---
> Alle Abteilungen nach Durschnittsgehalt, absteigen
```sql
SELECT department_name, avg(salaray)
	WHERE d.department_id = e.department_id
		GROUP BY department_name
			ORDER BY 2 DESC;
```

=> Über Control Files ...
```sql
DESC V$CONTROLFILE;
```
```sql
SELECT name FROM V$CONTROLFILE;
```

...
```sql
SELECT * FROM V$CONTROLFILE_RECORD_SECTION WHERE type='DATA_FILE';
```