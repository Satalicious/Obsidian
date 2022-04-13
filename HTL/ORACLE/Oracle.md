
### How to Setup/Start Oracle: [[Oracle Setup]]

### Data Dictionary: [[Data Dictionary]]
---
---

### USER MANAGEMENT

=> User HR entsperren

```SQL
ALTER USER HR ACCOUNT UNLOCK;
```

=> Passwort für HR ändern

```SQL
ALTER USER HR IDENTIFIED BY hr;
```

---
---


> wieviel DB-Objekte besitzt jeder User?

```SQL
SELECT owner, count(*) as "DB Objekte"
	FROM DBA_OBJECTS
		GROUP BY owner
		ORDER BY 2 DESC;
```

> Wieviele Typen von DB Objekten (object_types) gibt es?

```SQL
SELECT object_type, count(*)
		FROM DBA_OBJECTS
			GROUP BY object_type
				ORDER BY 2 DESC;
```
	
> wieviele DB Objekte gibt es, deren Namen mit DBA_ beginnt?

```SQL
SELECT count(*)
	FROM DBA_OBJECTS
		WHERE object_name LIKE 'DBA_%';
```

> Welchem Benutz gehören die meisten Tabellen?

```SQL 
SELECT owner, count(*) as "Tableanzahl"
	FROM DBA_TABLES
		GROUP BY owner
			HAVING count(*) >= ALL(SELECT count(*) 
			FROM DBA_TABLES GROUP BY owner);
```

```SQL
SELECT owner, count(*) as "Tableanzahl"
	FROM DBA_TABLES
		GROUP BY owner
			HAVING count(*) = (SELECT max(count(*)) 
			FROM DBA_TABLES GROUP BY owner);
```

> Wieviele Tabellen gehören dem User 'HR'?

```SQL
SELECT count(*) 
	FROM DBA_TABLES 
		WHERE OWNER = 'HR';
```

> Alle Tables selecten auf die ich als jetziger User zugriff habe

```SQL
SELECT TABLE_NAME FROM USER_TABLES ORDER BY 1;
```


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



