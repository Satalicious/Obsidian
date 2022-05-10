### Redo Logifle

#####  => Zweck:

1. Performancegewinn
2. Sicherheit falls Rechner abstürzt

```sql
desc V$LOG;

SELECT group, members, status from V$LOG;

ALTER SYSTEM SWITCH LOGFILE; // um gespiegelte Files zu switchen

SELECT member FROM V$LOGFILE;#

ALTER DATABASE ADD LOGFILE;
```

Logfiles anlegen:

```sql
ALTER DATABASE ADD LOGFILE ('c:\oraclexe\app\oracle\fast_recovery_area\xe\onlinelog\GRP4A.LOG') SIZE 10M;

// das ist der 'spiegel' dazu
ALTER DATABASE ADD LOGFILE MEMBER ('c:\oraclexe\app\oracle\fast_recovery_area\xe\onlinelog\GRP4B.LOG') TO GROUP 4;
```