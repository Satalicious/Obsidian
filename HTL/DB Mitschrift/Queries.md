
Welche Soccerteams haben zumindest einmal gewonnen?

```sql
```SELECT DISTINCT t.name FROM teams t, matches m 
WHERE (t.id = m.home_team_id AND goalsH > goalsG) OR (t.id = m.guest_team_id AND goalsG > goalsH);
```

# SKIRESORTS Queries

```sql

Welche Skigebiete betreiben zumindest eine Gondel?


SELECT DISTINCT r.name
	FROM skiresorts r, skilifts s, lifttypes l
    WHERE r.id = s.skiresort_id AND s.lifttype_id = l.id
    AND l.name = "Gondel";	
	
======================================================================
Welche Skigebiete betreiben keine Gondel?

SELECT DISTINCT r.name
	FROM skiresorts r, skilifts s, lifttypes l
    WHERE r.id = s.skiresort_id AND s.lifttype_id = l.id
    AND l.name <> "Gondel";	
	
SELECT DISTINCT r.name
	FROM skiresorts r
    WHERE r.id NOT IN ()
======================================================================
Klausel: JOIN
======================================================================

SELECT r.name, s.name, t.name
	FROM skiresorts r, skilifts s, lifttypes t
		WHERE r.id = s.skiresort_id
		AND s.lifttype_id = t.id
		AND t.name ='Schleplift';
		
SELECT r.name, s.name
	FROM skiresorts r JOIN skilifts s
		ON r.id = s.skiresort_id
		JOIN lifttypes t
		ON s.lifttype_id = t.id
			WHERE t.name = 'Schleplift';
			
======================================================================		
Wieviele Skilifte gibt es pro Skigebiet?

SELECT r.name, count(*) AS Liftanzahl
	FROM skiresorts r, skilifts l
		WHERE r.id = l.skiresort_id
			GROUP BY r.id, r.name;


+------------+------------+
| name       | Liftanzahl |
+------------+------------+
| Schladming |          2 |
| Naßfeld    |          1 |
+------------+------------+

Keine Frauenalpe dabei, da sie keinen Skilift hat. - PROBLEM!!
==========
	LÖSUNG:
==========

SELECT r.name, count(l.id) AS Liftanzahl
	FROM skiresorts r LEFT OUTER JOIN skilifts l
		ON r.id = l.skiresort_id
			GROUP BY r.id, r.name;
			
======================================================================		
Welche Skigebiete haben mindestens 3 Liftanzahl?
			
SELECT r.name, count(l.id) AS Liftanzahl
	FROM skiresorts r LEFT OUTER JOIN skilifts l
		ON r.id = l.skiresort_id
			GROUP BY r.id, r.name
				HAVING count(*) > 2;
======================================================================
In welchen Skigebiet gibt es KEINE Schleplifte?

SELECT r.name, count(r.id)
	FROM skiresorts r, skilifts l
		WHERE r.id = l.skiresort_id AND l.id = 2
			GROUP BY r.name;

SELECT s.name
	FROM skiresorts s
		WHERE s.id NOT IN (SELECT DISTINCT l.skiresort_id
			FROM skilifts l, lifttypes t
			WHERE l.lifttype_id = t.id AND t.name = 'Schleplift');

(SELECT DISTINCT l.skiresort_id, l.name, t.name
			FROM skilifts l, lifttypes t
			WHERE l.lifttype_id = t.id AND t.name = 'Schleplift');


SELECT s.name, count(t.id) AS Schleplifte
	FROM skiresorts s, lifttypes t, skilifts l
		WHERE s.id = l.skiresort_id AND t.id = l.lifttype_id
		AND t.id = 2
		GROUP BY s.name;
	
SELECT s.name, l.name
	FROM skiresorts s, skilifts l
	WHERE s.id = l.skiresort_id;
	

	
======================================================================	
Wieviele Skilifte hat jedes Skigebiet?

======
LÖSUNG
======
// PASST NOCH NICHT GANZ


SELECT r.name, count(l.id) AS "Anzahl Schleplifte"
	FROM skilifts l JOIN lifttypes t ON (t.id = l.lifttype_id)
	RIGHT OUTER JOIN skiresorts r ON r.id = l.skiresort_id
	GROUP BY r.id, r.name;


	
	
count (*) 		...		zählt alle Datensätze der Gruppe
count(<spalte>) ...		zählt alle Datensätze der Gruppe, bei denen die Spalte mit dem Wert <spalte> != NULL ist


======================================================================
			
Liste aller Skigebiete mit Anzahl der Schleplifte
Idee: alle Skilifte des selben Gebiets zu einer Gruppe zusammenfassen.
pro Gruppe -> ausgeben von Namen und die Anzahl der Schleplifte

======
LÖSUNG
======

SELECT r.name, count(l.id) AS "Anzahl Schleplifte"
	FROM skilifts l JOIN lifttypes t ON (t.id = l.lifttype_id AND t.name = 'Schleplift')
	RIGHT OUTER JOIN skiresorts r ON r.id = l.skiresort_id
	GROUP BY r.id, r.name;
	
	
======================================================================
Welche Skigebiete haben mehr Liftanlagen als das Skigebiet 'Kreischberg'?

SELECT r.name, count(s.name) as "Anzahl Liftanlagen"
	FROM skilifts s, skiresorts r
		WHERE s.skiresort_id = r.id
			GROUP BY r.id, r.name
				HAVING count(*) > (SELECT count(*)
	FROM skiresorts r1, skilifts l1
		WHERE r1.id = l1.skiresort_id AND r1.name = 'Kreischberg');


// Anzahl Skilifte bei Kreischberg in INT
(SELECT count(*)
	FROM skiresorts r1, skilifts l1
		WHERE r1.id = l1.skiresort_id AND r1.name = 'Kreischberg')
		
======================================================================
BEI GROUP BY DAS VON SELECT REINSCHREIBEN,
AM BESTEN NOCH id MIT name DAZU SCHREIBEN		

```

# Subqueries 01.03.22

```sql

> Es gibt Stellen in denen man statt einem Wert oder einer Menge von Werten 
	das Ergebnis einer Abfrage einsetzen kann.
	
	z.B. WHERE Klausel
	
	SELECT ...
		FROM ...
			WHERE ... = (SELECT ...)
			
======================================================================: Welche Skiresorts gibt es aus der selben Region wie "Frauenalpe"?
	
	a) ohne Subquery
	SELECT s1.name 
		FROM skiresorts s1, skiresorts s2
			WHERE s2.name = 'Frauenalpe'
			AND s1.region = s2.region
	
	b) mit Subquery
	SELECT sr.name
		FROM skiresorts sr
			WHERE sr.region = (SELECT sr1.region FROM skiresorts sr1 WHERE sr1.name = 'Frauenalpe')
			
======================================================================	
	Bsp: Welches Skigebiet hat die meisten Pistenkilometer?

	a) ohne Subquery
	SELECT s1.name
		FROM skiresorts s1, skiresorts s2
			WHERE 
	
	b) mit Subquery
	SELECT s1.name 
		FROM skiresorts s1
			WHERE slope_length = (SELECT max(slope_length) FROM skiresorts);
			
======================================================================
	Bsp: Welches Skigebiet hat die meisten Pistenanlagen?
	
	SELECT r.name
		FROM skiresorts r, skilifts l
			WHERE r.id = l.skiresort_id
			GROUP BY r.id, r.name 
				HAVING count(*) >= ALL 
				(SELECT count(*) FROM skilifts
				GROUP BY skiresort_id);
				
	/* nur falls DBMS geschachtelte Spaltenfunktionen beherrscht!!
	SELECT r.name
		FROM skiresorts r, skilifts l
			WHERE r.id = l.skiresort_id
			GROUP BY r.id, r.name 
				HAVING count(*) >= ALL 
				(SELECT max(count(*)) FROM skilifts GROUP BY skiresort_id);
	*/		
======================================================================
	Bsp: Welcher Lifttyp wird am häufigsten verwendet?
	
	SELECT lt.name
		FROM skilifts l, lifttypes lt
		WHERE lt.id = l.lifttype_id
		GROUP BY lt.id, lt.name
		HAVING count(*) >= ALL
		(SELECT count(*) FROM skilifts l2 GROUP BY l2.lifttype_id);
		
======================================================================
	Bsp: Welche Skiresorts haben mehr Sessellifte als Schlepplifte?
	
	-> abhängige SQ: in der SQ Zugriff auf Datensatz der äußeren Query.
	-> Prinzip:
	SELECT ...
		FROM ... t, ...
			WHERE ... (SELECT ... FROM ... WHERE ... t.
			
	
	SELECT r.name
		FROM skiresorts r, skilifts l, lifttypes t
		WHERE r.id = l.skiresort_id AND l.lifttype_id = t.id AND t.name = 'Sessellift'
		GROUP BY r.id, r.name
		HAVING count(*) > 
		(SELECT
			FROM skilifts l1, lifttypes t1
				WHERE l1.lifttype_id = t1.id AND l1.skiresort_id = r.id
				AND t1.name = 'Schlepplift');											
```
###  DAS OBEN IST DER SPRINGENDE PUNKT EINER ABHÄNGIGEN SQ!!
```sql
Welche Skiresorts haben größere Liftanzahl als Schladming?

Bsp: Welcher Skilift absolviert die meisten Höhenmeter?

a) ohne SQ
SELECT s1.id, s1.name
	FROM skilifts s1, skilifts s2
		WHERE s1.height >= s2.height
		GROUPY BY s1.id, s1.name
		HAVING count(*) = 9;
				
b) mit SQ
SELECT s.name
	FROM skilifts s
		WHERE height = (SELECT max(height) FROM skilifts);
		
======================================================================
Views: Sichten auf Tabellen

	> jede View besitzt ein zugrundeliegendes SELECT Statement
	> jede View kann wie eine Tabelle verwendet werden
		allerding wird bei jeder Verwendung zuerst immer
		dieses Statement ausgeführt (Performance leidet)
		
	CREATE VIEW biglifts AS 
	(SELECT id, name, height FROM skilifts WHERE height > 600)
	
	CREATE VIEW resorts_ov AS
	(SELECT r.id, r.name, r.slope_length, count(*) AS "nr_lifts"
		FROM skiresorts r, skilifts l
		WHERE r.id = l.skiresort_id
		GROUP BY r.id, r.name, r.slope_length)
```
