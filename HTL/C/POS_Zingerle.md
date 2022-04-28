###### 09.03.2022

# Auslagern von Funktionen

Wenn man Funktionen aus der main.cpp auslagern möchte benötigt man eine Header (.h) Datei und eine gleichnamige .cpp Datei

Module aus dem eigenem Projekt werden mit `#include "Module.h"` inkludiert
Module aus dem Standardpfad des Compilers werden mit `#include <Module.h>` inkludiert. 

__In der Header Datei werden die Prototypen der Dateien angelegt:__

```c
void hallo();
void hallo(int); //overloaded hallo funktion
void summe(int, int);
```

__In der gleichnamigen .cpp Datei werden nun die Funktionen definiert:__

```c
#include <stdio.h>
void hallo() {
	printf("Hello World\n");
}
void hallo(int x) {
	printf("The number is %d\n", x);
}
void summe(int a, int b) {
	printf("Summ is %d\n", a + b);
}
```

Anschließend können die Dateien wie folgend in main eingefügt werden.
__Merke:__ die Header Datei wird mit __\#include "name.h"__ eingefügt.

```c
#include <stdio.h>
#include "test.h"
int main(){
	hallo();
	hallo(3);
	summe(1, 4);
	return 0;
}
```

Die Ordnerstruktur schaut folgend aus:

![[Pasted_image_20220309102443-1.png]]
---

###### 23.03.2022


**Call bei Reference** uebergibt die Adresse der uebergebenen Variable
a passed down Array is automatically called by Reference.

```c
void test1(int *z25){
	*z25 = 20; // this function will alter the passed down variable
}

void main(){
	int z1 = 5;
	test1(&z1);
}
```

**Call bei Value** erstellt eine Kopie des uebergebenen Wertes
for example a passed down Integer is automatically called by Value 

```c
void test1(int z25){
	z25 = 20;  // this function does not alter the passed down variable. 
}

void main(){
	int z1 = 5;
	test1(z1);
}
```


