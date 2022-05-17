Was ich gelernt habe (in dieser Reihenfolge): 

> blinky (1.) --> Stoppuhr --> blinky (2.) --> Interrupts --> Zeichenumkehrt
> *beim zweiten Mal beim blinky:*
> - *zw. InterruptIn & DigitalIn unterscheiden*
> - *wie man mbed Bibliotheken lesen und verstehen soll*
>
> *beim Zeichenumkehrt:*
> - *Schwerpunkt: pointers, putchar() & getchar()*

### blinky (1.)
mit [simulartor](https://simulator.mbed.com/)

```cpp
#include "mbed.h"

DigitalOut led(LED1);

int main() {
    while (1) {
		led = !led;
		printf("Blink! LED is now %d\n", led.read());
		
		wait_ms(500);
	}
}
```

Schon probiert:
- [?]   wait_ms(500) auszukommentieren (Ctrl + / bei englische Tastatur) --> Achtung: Memory-Überlastung. Led würde nicht blinken.
- [?]   `led = !led` und `led = !led; wait_ms(500)` außerhalb der while-Schleife schreiben --> Led würde nicht blinken.
- **Erklärung:** `while` liest und aktualisiert den Wert von led1 immer (led1 würde immer blinken). Code innerhalb der main-Funktion (statt innerhalb einer Schleife) wird nur einmal ausgeführt.

### Stoppuhr
Aufgabenstellung:
> Programmieren Sie eine Stopp-Uhr mit folgenden Funktionen:
> -   Ein ==Druck nach OBEN auf dem Joystick (p15)== startet die Zeitnehmung, welche bis zum Beginn eines zweiten Drucks nach OBEN (egal wie lange dieser ist, soll das Niederdrücken des Tasters zählen) läuft. Danach wird die gemessene Zeit im Format "sss,xy" (mit sss in Sekunden, x Zehntelsekunden, y Hundertstelsekunden) ausgegeben.
> -   Mit ==einem Druck nach unten (p12)== kann die Messung jederzeit gestoppt und die Zeit resettiert werden
> -   Während die Zeitnehmung läuft, soll die LED1 leuchten (und LED2 und 3 aus sein) - wenn die Uhr stoppt und einen Wert ungleich 0 hat, soll LED1 aus sein und LED2 leuchten.
> -   Wenn die Uhr resettiert ist, soll LED3 leuchten.
> GLEICHZEITIG ==soll die LED4== mit einer Frequenz von ==genau 2Hz blinken==, ==ohne von den Stoppuhr-Funktionen gestört zu werden==.

- **Druck auf dem Joystick** == Hardware interrupt/ input, das vom Hardware erkennt wird --> DigitalIn oder InterruptIn zu verwenden.
- **LED4 mit 2Hz immer blinken, unabhängig von der anderen Funktionalitäten von Stoppuhr** -->  zurück zum Blinky + google : 2Hz to seconds

>[!Probier und schreib dein Ergebnis hier:]

- [ ] 2Hz = ??? Sekunden = ??? Millisekunden
- [ ] Welche Funktion zu verwenden, damit LED4 nicht immer leuchtet, sondern blinken soll? (zurück zum blinky - Simulator)
- [ ] Code, damit LED4 immer blinken soll:
```cpp
int main() {
	/* schreib dein Code hier */
}
```

##### Interrupts
[Interrupts with Simulator](https://simulator.mbed.com/#interrupts)

*Note to self: man kann auf diesem schwarzen Button drucken*
![[Pasted image 20220515011933.png]]

Schon probiert:
- [ ] Welche LED wird vom Button (btn) eingeschaltet? Und durch welche Funktion?
- [ ] Wie sieht der Code für InterruptIn aus, der mit BUTTON1 (btn) verbunden wird?
- [ ] Kommentier diese Zeilen aus:
	- [ ] `printf("Ticker fired\n");` in `void blink_led1()` (damit man von der Texte nicht abgelenkt wird)
	- [ ] `t1.attach(callback(&blink_led1), 1.0f);`
	- [ ] `t2.attach(callback(&turn_led3_on), 2.5f);`
	- [ ] Auf Run klicken, um die Seite mit dem neuen Code zu aktualisieren.
- [ ] Auf dem schwarzen Button sowohl kurz als auch länger klicken. Wann kann man den Text 'BUTTON fall invoked' auf dem Terminal sehen?
- [ ] die Callback-Funktion innerhalb von `btn.fall(callback(--))` ändern:
	- [ ] statt `toggle_led2` tippe `toggle_led2()`. Was wird passieren? Den Fehler kopiere und hier hinzufüge:
	- [ ] statt `toggle_led2` `blink_led1` und `turn_led3_on` hinzufüge. Achte auf:
		- [ ] The state of each led after a new function was swapped in
		- [ ] Compare to `t1.attach(callback(&blink_led1), 1.0f);` and `t2.attach(callback(&turn_led3_on), 2.5f);`. What determines whether the led should blink in each case?
- [ ] Den Code für Interrupts erneut lade (Load Demo klicke) und auf Keil Studio in 3 Verschiedene Projekte hinzufüge:
	- [?] Es gibt keinen BUTTON1 beim mbed LPC1768 (unser Mikrocontroller), aslo braucht man um vllt Joystick(p14) zu wechseln.
	- [ ] eines beim mbed-os2
	- [ ] eines beim mbed-os5
	- [ ] eines beim mbed-os6
- [ ] Versuche, diese Projekte zu kompilieren. Was würde im jeden Fall passieren?

>[!Zusammenfassung:]
>- Wie sieht der Code für einen InterruptIn aus?
>``` /* Code hier schreibe */ ```
>- Wann verwendet man InterruptIn?


**Stoppuhr Aufgabenstellung**
> Programmieren Sie eine Stopp-Uhr mit folgenden Funktionen:
> -   Ein Druck nach OBEN auf dem Joystick (p15) startet die Zeitnehmung, welche bis zum Beginn eines zweiten Drucks nach OBEN (==egal wie lange dieser ist, soll das Niederdrücken des Tasters zählen==) läuft. Danach wird die gemessene Zeit im Format "sss,xy" (mit sss in Sekunden, x Zehntelsekunden, y Hundertstelsekunden) ausgegeben.

- [ ] Welche Klasse (DigitalIn oder InterruptIn) sollte für diesen Zweck geeignet sein?

##### DigitalIn
*Wie man die Bibliotheke von mbed Klassen lesen und verstehen soll*
*!!Diese Skills sind wichtig, da man die für den Open-book Test braucht*

Schon probiert:
- [ ] google *mbed digitalin*
- [ ] Screenshot all the immediate steps that lead to this page: [Descriptions of DigitalIn class methods](https://os.mbed.com/docs/mbed-os/v6.15/mbed-os-api-doxy/classmbed_1_1_digital_in.html#aaab5dab5b969a87f538242e524431637)
- [ ] *Noch nicht fertig*
![[Pasted image 20220515021915.png]]
	