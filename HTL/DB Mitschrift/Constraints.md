
# CONSTRAINTS
- UNIQUE ...     muss eindeutig sein
- NOT NULL ... darf nicht den Wert NULL enthalten
- FOREIGN KEY CONSTRAINT
	- ALTER TABLE skilifts ADD FOREIGN KEY (skiresort_id)
	REFERENCES skiresorts(id)
- PRIMARY KEY ... generiert Index


```sql
UPDATE skilifts SET lifttype_id = 2 WHERE id = 5;
```


### Spalten nachträglich hinzufügen / entfernen / Attrib. ändern

```sql 
ALTER TABLE skiresorts
ADD region VARCHAR(32);

ALTER TABLE skiresorts
DROP region 

ALTER TABLE skiresorts
CHANGE region region VARCHAR(32);
```