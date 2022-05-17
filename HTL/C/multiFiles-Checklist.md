- [?] double calc_circuit_resistance(Circuit c) (circuit.c) innerhalb von main.c nicht aufgerufen werden zu muessen.
- [?] resistor Array im struct Circuit sollte 3 Elementen haben (Jetzt hat es nur 2)
```cpp
typedef struct {
	double resistor[2]; // this means the Array is initiated with only 2 Elements
	bool isSerial;
} Circuit;
```

Es sollte so aussehen:
```cpp
typedef struct {
	double resistor[3];
	bool isSerial;
} Circuit;
```

Das Problem beim `double resistor[2]` ist, dass es eine Element kuerzer als was du eigentlich brauchst (also mit 3 Elementen). Das heisst, es hat nur Index \[0\] und \[1\] (bei Array-Initialisierung \[n\] bedeutet, die Grosse vom Array ist n-Elementen -  auch Array-length ist gleich n. Hier hat n nichts mit Index zu tun.) Wenn du ein nicht-existierend Index aendern moechtest (z.B. mit scanf in read_circuit), and when the compiler is especially difficult, it will throw Stack Smashing Detected Error.

- [?] beim Drucken der Taste 'h' sollte das ganze Menu mit alle Auswahl zeigen zu lassen, nicht den Text 'show help text' :P. Probier mal und tipp z.B. 'cd --help' auf deinem Linux-Terminal und kannst du sehen, was ich meine.
- [?] Wenn man beim `i n` tippen, sollten wir eine vorrausichtlich Fehlerbehandlung dafur vorbereiten. Z.B. sollte n > count sein, dann sollte das Programm nichts druecken, ausser von einer Fehlermeldung. Jetzt wenn man z.B. `i 100` tippt und es nur 1, 2 Artikel im Array gibt, dann drueck das Programm so:
>[!Output]
>=> Type:  Quantity: 0  Value: 0.000000 Unit:

- [?] for Schleife in print_items:
Wenn das Array so gross ist (mit 1000 Elementen),  sollte man die for-Schleife vermeiden zu nutzen. Stattdessen sollte man pointers verwenden, um alle Elementen zu druecken.
Der Vorteil von pointers in C im vergleich zum Array in Python ist, dass das Druecken von einer grossen Menge von Daten die Computer-Memory nicht ueberlastet.
In Python, the whole Array of 1000 elements would be processed in RAM. This is distrasous, when there are several loops used, or loops nested inside loops.
With pointers in C, the pointer will point to a place in computer memory (an element of the array), and when it is increased, it will go through the whole array, but no matter how big the array is, only that pointer will be processed in RAM, and its size is minimal (generally 8 bytes).
Dereferencing (Entpacken vom Wert eines Pointer) a pointer would be more effective and less resource-hogging than accessing all elements' values at once.

Fuer dieser Uebung, eine for-Schleife reicht, weil niemand dem ganzen Array mit 1000 Elementen hinzufuegen koennte. Diese ist deshalb nur Gut-zu-wissen Sache.