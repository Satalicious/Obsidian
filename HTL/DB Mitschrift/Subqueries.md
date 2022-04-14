

<mark style="background: #FFB8EBA6;">einfache SQ:</mark> ein Wert

<mark style="background: #FFB8EBA6;">komplexe SQ:</mark> eine Menge an Werten. Zum Vergleichen: IN, ANY, ALL

<mark style="background: #FFB8EBA6;">abhängige SQ:</mark> innere Query verwendet Tablle der äußeren Query


### UNABHÄNGIG / ABHÄNGIGE SUBQUERIES

Abhängige Subqueries nur wo man sie unbedingt braucht, da Datensätze sich multiplizieren und Laufzeit größer wird.	
```sql
SELECT FROM WHERE GROUP BY HAVING
```

Bei unabhängigen SQ werden diese nur 1 Mal ausgeführt und verglichen, sie liefern genau einen Wert.	

```sql
SELECT FROM WHERE
```

Einfache SQ liefert genau EINEN Wert.
Komplexe liefert eine MENGE. 
```sql 
IN, NOT IN, <=ANY,>ALL
```


# MAXIMUS

---
