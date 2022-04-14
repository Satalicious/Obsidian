## SQL DML

```sql
INSERT INTO skiresorts (name) VALUES ('Schladming');

INSERT INTO lifttypes (name) VALUES ('Sessellift');

INSERT INTO skilifts (name, height, lifttype_id, skiresort_id)
	VALUES("Rosenkranzlift", 550, 1,1);
```