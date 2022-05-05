
! TEST

=> beinhaltet Informationen über
		- alle Datenfiles (Pfade)
		- Systeminformationen (seq#, Checkpoints, ...)

=> wird beim Start benötigt
	=> ohne Controlfile kein Zugriff auf den Datenbestand!!


```sql
alter system set control_files = '/u01/app/oracle/oradata/myorcl/control1.ctl' ,'/u02/app/oracle/oradata/myorcl/control2.ctl' 
scope = spfile;
```

```sql
show parameter control_files;
```