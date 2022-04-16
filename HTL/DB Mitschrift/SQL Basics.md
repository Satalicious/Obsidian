
## Erzeugen von Tabellen

CREATE TABLE lifttypes 
(id INT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(32),
description VARCHAR(512));

CREATE TABLE skilifts (id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(32),height INT,lifttype_id INT,skiresort_id INT);

[[Constraints]]

[[Datensätze einfügen]]

---

# SQL DRL
- logische Operatoren: AND, OR, NOT
- rel. Operatoren: >, <=, <, =, <>
- besondere: <mark style="background: #FFF3A3A6;">BETWEEN, LIKE, IS NULL</mark> 
	
- WHERE id BETWEEN 1 AND 3			//WHERE id >= 1 AND id <= 3
- WHERE last_name LIKE "A%"			//Namen beginnend mit Großbuchstaben
- WHERE last_name LIKE "___"		//Name mit genau 3 Buchstaben

---
### Eines der wichtigsten Dinge: [[Queries]]
[[Subqueries]]
[[Cocktails]]
---


## JOIN zwischen mehreren Tabellen

```sql 

select * FROM skiresorts, skilifts;
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+
| id | name       | slope_length | plz  | city | region | id | name           | height | lifttype_id | skiresort_id |
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+
|  1 | Schladming |         NULL | NULL | NULL | NULL   |  1 | Rosenkranzlift |    550 |           1 |            1 |
|  2 | Naßfeld    |         NULL | NULL | NULL | NULL   |  1 | Rosenkranzlift |    550 |           1 |            1 |
|  1 | Schladming |         NULL | NULL | NULL | NULL   |  2 | Rosenkranzlift |    550 |           2 |            1 |
|  2 | Naßfeld    |         NULL | NULL | NULL | NULL   |  2 | Rosenkranzlift |    550 |           2 |            1 |
|  1 | Schladming |         NULL | NULL | NULL | NULL   |  3 | Naßfeldbahn    |    800 |           3 |            2 |
|  2 | Naßfeld    |         NULL | NULL | NULL | NULL   |  3 | Naßfeldbahn    |    800 |           3 |            2 |
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+


select * FROM skiresorts, skilifts
    WHERE skiresorts.id = skilifts.skiresort_id;
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+
| id | name       | slope_length | plz  | city | region | id | name           | height | lifttype_id | skiresort_id |
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+
|  1 | Schladming |         NULL | NULL | NULL | NULL   |  1 | Rosenkranzlift |    550 |           1 |            1 |
|  1 | Schladming |         NULL | NULL | NULL | NULL   |  2 | Rosenkranzlift |    550 |           2 |            1 |
|  2 | Naßfeld    |         NULL | NULL | NULL | NULL   |  3 | Naßfeldbahn    |    800 |           3 |            2 |
+----+------------+--------------+------+------+--------+----+----------------+--------+-------------+--------------+


select skiresorts.name, skilifts.name, skilifts.height FROM skiresorts, skilifts
    WHERE skiresorts.id = skilifts.skiresort_id;
+------------+----------------+--------+
| name       | name           | height |
+------------+----------------+--------+
| Schladming | Rosenkranzlift |    550 |
| Schladming | Rosenkranzlift |    550 |
| Naßfeld    | Naßfeldbahn    |    800 |
+------------+----------------+--------+


> ALIAS SETZEN

SELECT r.name, s.name, s.height FROM skiresorts r, skilifts s
    -> WHERE r.id = s.skiresort_id;
	

```


