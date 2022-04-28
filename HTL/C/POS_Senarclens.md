__Senarclens Test 09.06.2022__



###### 08.03.2022 ######
# C Programming   

## Functions: ##
__Function Signature:__ --> Defines Datatypes of  parameters and return Value. 
Example sum function: (int)(int, int)
                        

```c
#include <stdio.h>

// Prototypen
void helper(in a);  
int sum(int a, int b); 

// können in der main genutzt werden, obwohl erst nachher geschrieben!
int main(){
	sum(3, 5);	
	return 0;
}

int sum(int a, int b){ //Functions Definition of sum
	helper(a, b);
	return a + b;
}

void helper(int a){ //Functions Definition of helper
	printf("got help for %d", a);
}
```

###### 15.03.2022
## String

**STDIN** input über Tastatur
**STDOUT** output über Konsole
**STD Error** eigenes File quasi wie STDOUT

**C-String** 
 - char array terminated with '\0'  ('\0' == false)  
 - kann Werte von 0-256 annehmen limited to ASCII
 - 8 Bit
 - are "dumb"
 ```c 
 char text[] = "Freedom" // sind 8 character Freedom + \0
 ```
**sscanf()** und **fgets()** um String einzulesen

bei fgets werden überschüssige Character verworfen
bei sscanf liest nur von einem bestehendem C-String kann dadurch nicht 'zuviel' lesen
**printf()** printet bis es auf ein \0 trifft
 
---

###### 22.03.2022
# Structs
Werden benötigt um mehrere Werte in einer Funktion zurückzugeben
Mit Structs werden Datensäzte gespeichert.
Ein struct wäre somit eine Zeile in einer Datenbank.

Eine Datensatz wie dieser wäre als Array von Structs in C Dargestellt

| Item     | Amount | Unit |
| -------- |:------:| ---- |
| Apple    |   2    | kg   |
| Lemonade |   3    | l    |
| Grapes   |   1    | kg   |

In Structs könne verschieden Datentypen kombiniert werden.

**Syntax**
```c
struct strct_name{
	type member1;
	type member2;
}
```

**Bsp**
Zuerst wird der Bauplan erstellt --> die Klasse
Danach wird das Struct befüllt --> Instanz
```c
struct strct_name{
	int year;
	int month;
	int day;
};

struct date d = {2021, 12, 10};
```

Oder man addressiert die member direkt
```c
struct date d = {.year=2021, .month=12, .day=10};
```

---

### Typedef
Type definition identifier.
Ist ein Alias für einen Datentyp

Neuer type names car_number der einen INT repräsentiert.
```c
typedef int car_number;

car_number my_peugot_id = 13743;

printf("My car number: %d \n", my_peugot_id);
```

---

### Struct Syntax
[Practice](https://bulme.find-santa.eu/exercises/c/exercise_structs/)
Entweder werden Structs so erzeugt
```c
struct point {
float x;
float y;
};
struct point p = {2.5, 4.8};
```

oder mit typedef um den syntax zu verkürzen.
```c
typedef struct{
	float x;
	float y;
} Point;

Point p1 = {.x=3.2, .y=4.1};
```

copy assignment
```c
Point p2 = p1; // der zweite Punkt wird kopiert und hat eigene Punkte die keine referenz sind "copy assignment"
p2.x = -5;
```

---

#### Structs in Funktionen übergeben
Structs werden kopiert, wenn sie in Funktionen übergeben werden.
```c
void print_point(Point p){
	printf("P(%f/p%f)", p.x, p.y);
	p.x = 3.1;
	p.y = 2.9;
	return p;
}
```

Hier wird beim Aufruf in der Funktion eine Kopie des Structs erstellt
```c
#include <stdio.h>
typedef struct{ //struct definition
    int year;
    int month;
    int day;
  } Date;

void print_date(Date *datum);// prototype

int main(void) {
  Date datum = {1999, 1, 13};
  print_date(&datum); // function call
}
void print_date(Date *datum){
  printf("My Day of Birth %d.%d.%d\n", (*datum).day, (*datum).month, (*datum).year);
}
```

**Merke:** Auf diese Weise wird beim Functionscall keine Kopie des Structs erzeugt
```c
#include <stdio.h>
typedef struct{ //struct definition
    int year;
    int month;
    int day;
  } Date;
void print_date(Date *datum);//function protoype

int main(void) {
  Date datum = {1999, 1, 13};
  Date *dptr = &datum; // a pointer to pass to the function
  print_date(dptr);  
}

void print_date(Date *datum){
  printf("My Day of Birth %d.%d.%d\n", datum->day, datum->month, datum->year); // syntactic sugar to access the struct members
}
```


---

###### 05.04.2022
## Pointer
[**Practice**](https://bulme.find-santa.eu/exercises/c/exercise_pointers/) 

**Why use pointers?**
	- To pass arrays to functions
	- to increase Performance (not copying values)
	- Function pointers in structs (like methods in c++)
	- Change Parameter values from a function
	- Dynamic memory managment
	- for hight level data structures (linked lists...)

**Problems:**
- Prone to bugs
- Memory leaks
- Do not modify parameters (bad Practice)

**Conventions:**
- initialisieren mit "NULL"
- der Stern * kann am Datentyp oder am Namen haengen
- Entweder ein Suffix verwenden y.B. var_ptr, varPtr
- oder ein Prefix z.B. ptr_varname, ptrVarname

**Syntax:**
- Nullpointer darf man nicht dereferenzieren
- \* um Pointer zu dereferenzieren (dorthingehen wo der Pointer hinzeigt)
- & um die Speicheradresse einer Variable zu bekommen (um sie in einem Pointer zu speichern)


>Der Wert eines Pointer ist der Zahlenwert einer Speicheradresse
Wenn man auf den Wert auf eben diese Speicheradresse zugreifen moechte verwendet man den Stern * Syntax.
Um auf die Speicheradresse einer Variable zugreiffen zu koennen verwendet man den & Syntax.
```c
	int test = 42;
	int* intPtr = &test;
	printf("Wert auf test %d", *intPtr);
```


> Changing Values
```c
	int* ptr = NULL;
	int a = 5;
	ptr = &a; // bei spaeterer zuweisung wird kein * verwendet
	*ptr += 5;	// der Wert auf a ist nun 10;
```


> Pointer koenne auf andere Pointer zeigen
```c
	int test = 13;
	int* ptr = &test;
	int** ptrptr = &ptr;
```

**array\[1]** ist dasselbe wie \***array + 1**

> 

**Pointer to Struct**
```c
	void print_date(Date *datum){
  printf("My Day of Birth %d.%d.%d\n", (*datum).day, datum->month, datum->year); 
}
```

--- 

###### 19.04.2022

## Dynamic Mmory Management
>Just another way to declare and use Arrays

[**Practice**](https://bulme.find-santa.eu/exercises/c/exercise_free_store/) *(cmake + git repo + criterion needed => siehe git README)*

Only way to set array size at Rutnime
To grow and shrink arrays and Structures

Needed to bypass the **ulimit** /the max Stack Size of the Operating System 
(Is only about 8MB (8192 KB))
you can check the ulimit with `ulimit -s` in the terminal
it can be configured by the SysAdmin

Interpretet Languages (at least python) do that on their own.

**cons**
 - Requires working with pointers
 - Relativlely slower compared to stack
 - The Programmer is in charge of managing the memory 
 - Potential Memory Leak
---
##### **Syntax**
```c
#include <stdlib.h>
void *malloc(size_t size) // Allocates size bytes and returns a pointer to the allocated memory

void free(void *ptr) // Frees the memory space pointed to by ptr


void *calloc(size_t nmemb, size_t size) Allocates memory for an array of nmemb elements of size bytes each and returns a pointer to the allocated memory. The memory is set to zero

void *realloc(coid *ptr, size_t size) //Changes the size of the memory block pointed to by ptr to size bytes.
```

---
##### **Beispiel for dynamically allocating memory**
```c
dynamically allocate the Memory
const int size = 1234;
int *array = malloc(size * sizeof(int));

// always free the memory
free(array);
```

---
##### **Safety**
Wenn das Betriebssystem uns den speicher aus irgendeinem Grund nicht freigibt bekommen wir Null zurueck. 
Deswegen checken wir `if (array == NULL)` ob wir den Speicher bekommen haben.
```c
const size_t size = 1234;
int *array = (*int) malloc(size * sizeof(int));
if (array == NULL){
	fprintf(stderr, "malloc %u bytes failed\n", size);
	exit(EXIT_FAILURE);
}

free(array);
```

---

###### 26.04.2022
### Working with multiple Source Files
[[POS_Zingerle]] Auslagern von Funktionen

> mit `extern` und `static` kann man Funktionen deklariere die nicht aus dem Modul exportiert werden sollen.
Bei default sind funktionen in einem Modul extern.
Möchte man einen Funktionsnamen in zwei verschiedenen Modulen verwenden, muss man static verwenden um Konflikte zu verhindern.

```c
static void function();
```


##### Include Guards
Um Doppelinkludierungen zu verhinden wird ein sogennanter **Guard** verwendet.

[Slideshow](https://bulme.find-santa.eu/presentations/c/multiple_files/#/5/1/0)

```c
#ifndef FILENAME H
#define FILENAME H
// your header file`s code
#endif // FILENAME H
```
