### USER MANAGEMENT

###### => User anlegen => Rechte zuweisen

```sql
CREATE USER akift22 IDENTIFIED BY akift22;
```

###### => "Einstiegsrechte" zu einer **Rolle** zusammengefasst
- CONNECT
```sql
GRANT connect TO akift22;
```

- User zu einem **Tablespace** zuweisen
```sql
ALTER USER akift22 DEFAULT TABLESPACE users;
```

- User eine **Datenmenge** zuweisen 
```sql
ALTER USER akift22 QUOTA 10M ON users;
```

- Systemprivileg: **CREATE TABLE** (**inkl.** SELECT, UPDATE, ..)
```sql
GRANT CREATE TABLE TO akift22;
```