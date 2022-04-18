# Statements zu den Cocktails

```sql
> Welche Cocktails sind alkoholfrei?

SELECT Cocktail
	FROM tblCocktail
		WHERE Alkoholgehalt = 0
=========================================================	
> Aus wievielen Zutaten wird jeder Cocktail erzeugt?

	SELECT c.Cocktail, count(*) as Zutatenanzahl
		FROM tblCocktail c, tblCocktailZutaten cz
			WHERE c.CocktailNr = cz.CocktailNr
				GROUP BY c.CocktailNr, c.Cocktail
=========================================================
> Aus wievielen alkoholfrei Zutaten wird jeder Cocktail erzeugt?

	SELECT c.Cocktail, count(*) as "Zutatenanzahl alkoholfrei"
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND cz.ZutatenNr = z.ZutatenNr AND z.Alkoholgehalt = 0
				GROUP BY c.CocktailNr, c.Cocktail;				
=========================================================		
> Alle Cocktails ohne Gruppe?

SELECT c.Cocktail
	FROM tblCocktail c, tblGruppe g
		WHERE c.GruppeNr = (g.GruppeNr AND g.Gruppe = 'Ohne') OR c.GruppeNr is NULL;
=========================================================	
> Cocktails mit mehreren alk. Zutaten?

	SELECT c.CocktailNr, c.Cocktail, count(*) as AlkhoholZutaten
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND cz.ZutatenNr = z.ZutatenNr AND z.alkoholgehalt > 0
				GROUP BY c.CocktailNr, c.Cocktail
				HAVING count(*) > 1;			
=========================================================
!!!!!!
> Welche Zutaten befinden sich nicht in der Hausbar?

	v1) ohne SQ
	
	SELECT z.Zutat
		FROM tblZutat z LEFT OUTER JOIN tblHausbar h
			ON z.ZutatenNr = h.ZutatenNr
				WHERE h.ZutatenNr is NULL
					GROUP BY z.Zutat;

	v2) mit SQ
	
	SELECT z.Zutat	
		FROM tblZutat z
			WHERE z.ZutatenNr NOT IN (SELECT ZutatenNr FROM tblHausbar)			
=========================================================		
> Welche Cocktails beinhalten die alkoholhältigste Zutat?

	SELECT 	c.Cocktail
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND cz.ZutatenNr = z.ZutatenNr
			AND z.Alkoholgehalt = (	SELECT max(Alkoholgehalt)
				FROM tblZutat);
=========================================================			
> Welche Cocktails haben mehr Zutaten als 'Gin Fizz'?

Subquery als Vorbereitung, Anzahl Zutaten von Gin Fizz:

	SELECT count(*) FROM tblCocktail c, tblCocktailZutaten cz
		WHERE c.CocktailNr = cz.CocktailNr AND c.Cocktail = 'Gin Fizz';
			

	SELECT DISTINCT c.Cocktail, count(*) as Anzahl
		FROM tblCocktail c, tblCocktailZutaten cz
			WHERE c.CocktailNr = cz.CocktailNr
				GROUP BY c.Cocktail HAVING count(*) > (SELECT count(*) FROM tblCocktail c2, tblCocktailZutaten cz2
												WHERE c2.CocktailNr = cz2.CocktailNr AND c2.Cocktail = 'Gin Fizz');
=========================================================			
> Welche Cocktails werden aus gleich vielen alkoholfreien Zutaten erzeugt wie 'Bloody Mary'?

Subquery als Vorbereitung, Anzahl alkoholfreier Zutaten von Bloody Mary:

	SELECT count(*)
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND c.Cocktail = 'Bloody Mary' AND cz.ZutatenNr = z.ZutatenNr AND z.Alkoholgehalt = 0;



	SELECT c.Cocktail, count(*) as Anzahl
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND cz.ZutatenNr = z.ZutatenNr AND z.Alkoholgehalt = 0 AND c.cocktail <> 'Bloody Mary'
				GROUP BY c.Cocktail HAVING count(*) = (	SELECT count(*)
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND c.Cocktail = 'Bloody Mary' AND cz.ZutatenNr = z.ZutatenNr AND z.Alkoholgehalt = 0);
=========================================================		
> Welche Cocktails können nicht produziert werden? = TESTBEISPIEL EVENTUELL!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
	V1) weil eine Zutat fehlt.
	V2) Weil eine Zutat komplett fehlt oder nur in zu geringer Menge vorhanden ist(Hausbar).
		Vorrauss.: Einheit ist überall dieselbe


	V1) -> Idee: Cocktails suchen wo zumindest 1 Zutat nicht in der Hausbar ist.
	
	SELECT c.Cocktail, count (*) as "Zutaten nicht vorhanden"
		FROM tblCocktail c, tblCocktailZutaten cz
			WHERE c.CocktailNr = cz.CocktailNr 
				AND cz.ZutatenNr NOT IN (SELECT ZutatenNr FROM tblHausbar)
					GROUP BY c.Cocktail
				
	V2) 
	
	SELECT c.Cocktail, count (*) AS "Zutat nicht vorh"
		FROM tblCocktail AS c, tblCocktailZutaten AS cz, tblHausbar AS h
			WHERE c.CocktailNr = cz.CocktailNr AND
				(
					(cz.ZutatenNr NOT IN (SELECT ZutatenNr FROM tblHausbar)) 
				OR 
					(cz.Menge > h.Menge AND h.ZutatenNr = cz.ZutatenNr)
				)
					GROUP BY c.Cocktail;
=========================================================
> Welche Cocktails werden aus mehr Brandy hergestellt als ' B and P'? 
// vllt Testbeispiel
Voraussetzung: max. 1 Brandy pro Cocktail

	SELECT c.Cocktail, sum(cz.menge) as Brandymenge
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = cz.CocktailNr AND cz.ZutatenNr = z.ZutatenNr
			AND z.Zutat = 'Brandy' 
			GROUP BY c.Cocktail
			HAVING (sum(cz.Menge)) > (SELECT sum(cz1.menge)
			FROM tblCocktail c1, tblCocktailZutaten cz1, tblZutat z1
			WHERE c1.CocktailNr = cz1.CocktailNr AND cz1.ZutatenNr = z1.ZutatenNr
			AND z1.Zutat = 'Brandy' AND c1.Cocktail = 'B and P');
=========================================================
> Welche Cocktails werden aus den meisten Zutaten erzeugt und Menge nicht gleich 0?
> 
	V1)

	SELECT c.Cocktail, count(*) as Anzahl
	FROM tblCocktail c, tblCocktailzutaten cz
	WHERE c.CocktailNr = cz.CocktailNr
	GROUP BY c.Cocktail
	HAVING count(*) >= ALL (SELECT count(*)
		FROM tblCocktailzutaten cz1
		WHERE cz1.menge > 0
		GROUP BY cz1.CocktailNr);
		
	V2)
	
	SELECT c.Cocktail, count(*) as Anzahl
	FROM tblCocktail c, tblCocktailzutaten cz
	WHERE c.CocktailNr = cz.CocktailNr
	GROUP BY c.Cocktail
	HAVING count(*) = (SELECT max(count(*))
		FROM tblCocktailzutaten cz1
		WHERE cz1.menge > 0
		GROUP BY cz1.CocktailNr);
=========================================================
> Welche Cocktails werden nicht aus den wenigsten Zutaten erzeugt?
	
	SELECT c.Cocktail, count(*) as Anzahl
	FROM tblCocktail c, tblCocktailzutaten cz
	WHERE c.CocktailNr = cz.CocktailNr
	GROUP BY c.Cocktail
	HAVING count(*) > ANY (SELECT max(count(*))
		FROM tblCocktailzutaten cz1
		WHERE cz1.menge > 0
		GROUP BY cz1.CocktailNr);
	
            ABHÄNGIGE SUBQUERIES
>>>>>>>>>>>>> Operator EXISTS <<<<<<<<<<<<<<<<<<<<<<<<<

	....WHERE/HAVING ... EXISTS (SELECT ...) => true wenn SELECT Statement ein Ergebnis bringt
	
>> in der Subquery hat man Zugriff auf die Spalten der Hauptquery.

	-> Subquery muss immer wieder neu ausgeführt werden !!!

=========================================================
> Welche Cocktails lassen sich nicht erzeugen, da zumindest eine Zutat in nicht
ausreichender Menge in der Hausbar vorhanden ist?
		
	SELECT c.Cocktail
		FROM tblCocktail c, tblCocktailZutaten cz, tblHausbar h
			WHERE c.CocktailNr = cz.CocktailNr AND
				AND cz.menge > (SELECT h.menge FROM tblHausbar h 
				WHERE h.ZutatenNr = cz.ZutatenNr);
=========================================================			
> Welche Cocktails werden aus mehr alkoholischen Zutaten erzeugt als aus antialkoholischen?

	SELECT c.Cocktail, count(*) AS Zutaten
		FROM tblCocktail c, tblCocktailZutaten cz, tblZutat z
			WHERE c.CocktailNr = c.CocktailNr AND z.ZutatenNr = cz.ZutatenNr
			HAVING count(*) > (SELECT 
			
			
