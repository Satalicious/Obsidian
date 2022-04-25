[

](https://cdn.discordapp.com/attachments/898116754591588382/965572382557352007/Finished_Handout.pdf#page=1 "Seite 1")[

](https://cdn.discordapp.com/attachments/898116754591588382/965572382557352007/Finished_Handout.pdf#page=2 "Seite 2")

Mutex  
Was ist das?  
Mutex steht für mutually exclusive, und wird verwendet um sicherzustellen, dass ein Thread  
exklusiven Zugriff auf eine Ressource hat.  
Benötigt wird dies im Bereich des Multithreadings, wenn mehrere Threads parallel zueinander  
laufen können.  
Ist dieser wechselseite Ausschluss nicht gegeben kann ein Thread die Ressourcen eines  
anderen Threads manipulieren, was zu unerwartet verfälschten Ergebnissen führen kann.  
Wie löst Mutex dieses Problem?  
Im Prinzip ist ein Mutex ein Vorhängeschloss, welches vor einen Codeblock gehängt wird.  
Im Folgendem Beispiel zeigen wir eine Funktion die einen geschützten Prozess darstellt.  
Durch pthread_mutex_lock() kann der Inhalt dieser Funktion immer nur von einem Thread  
gleichzeitig ausgeführt werden.  
Nachdem der Thread mit seiner Verwendung der Ressourcen fertig ist wird der Abschnitt durch  
pthread_mutex_unlock() wieder freigegeben.  
pthread_t tid[2];  
int counter;  
pthread_mutex_t lock; // Die Deklarierung useres Mutex  
void* doSomeThing(void *arg)  
{  
pthread_mutex_lock(&lock); // Versperrt unser "Vorhängeschloss"  
unsigned long i = 0;  
counter += 1;  
printf("\n Job %d started\n", counter);  
for(i=0; i<(0xFFFFFFFF);i++); // Der "Job" welcher ausgefuehrt wird  
printf("\n Job %d finished\n", counter);  
pthread_mutex_unlock(&lock); // Unser "Schloss" wird entgesperrt  
return NULL;  
}

Was passiert mit einem ausgesperrtem Thread?  
Ist ein Mutex ausgesprochen, kann kein anderer Thread auf diese Ressourcen zugreifen.  
Ein wartender Thread hat nun 3 Möglichkeiten.  
 Nichts weiter ausführen und "aktiv" auf die Zugriffserlaubnis warten.  
 Andere Aufgaben ausführen und später zurückkommen "passiv" warten  
 Den Zugriff verwerfen.  
Was kann dabei Schiefgehen?  
Wenn ein Thread mehrere Ressourcenpools für seine Aufgabe benötigen kann es passieren,  
dass ein Thread nur einen Teil dieser Ressourcen freigegeben bekommt. Nun kann es  
vorkommen, dass sich 2 Threads jeweils einen Teil der benötigten Ressourcen gegenseitig  
wegnimmt.  
Nun warten aber beide Threads auf ihre Ressourcen die sie benötigen bekommen diese jedoch  
nicht und das Programm steht still.  
Diese Situtation nennt man dann einen Deadlock.  
Link zu Problem, welches ohne Mutex entstehen kann:  
Link zur Lösung des Problems: