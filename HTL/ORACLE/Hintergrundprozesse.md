**Logfile Writer** schreibt ins Redo Logfile.

**DB_WRITER** schreibt vom Logfile in die Disk Blöcke, verbessert Performance, vorallem beim Zugriff von mehreren Usern. Performance ist immer gleich, egal ob 1 oder 100 auf DB zugreifen.

**Redo Logfile** beeinhaltet lokale Änderungen, die ohne Probleme rückgängig gemacht werden können.