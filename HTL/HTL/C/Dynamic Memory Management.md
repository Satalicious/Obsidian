
## Dynamic Memory Management

https://bulme.find-santa.eu/presentations/c/dynamic_memory_management/

we got ~ 8000 - 32000 MB, 8-32 GB RAM
			- in C ~ 8MB nutzbar
---

**DOWNSIDES**
- requires working with pointers
- relatively slower compared to the stack bcs stack is already reserved
- programmer in charge of managing memory
- potential memory leaks (tools like valgrind help with debugging)

*some of these problems are solved by C++*

---

```cpp
#include <stdlib.h>

void *malloc(size_t size)

	// Allocates `size` bytes and returns a pointer to the allocated memory. The memory is not initialized.

void free(void *ptr)
	// Frees the memory space pointed to by `ptr`.

void *calloc(size_t nmemb, size_t size)

	// Allocates memory for an array of `nmemb` elements of `size` bytes each and returns a pointer to the allocated memory. The memory is set to zero.
	// speichern von array mit 4 int => 4 * sizeof(int)

void *realloc(void *ptr, size_t size)

	// Changes the size of the memory block pointed to by ptr to size bytes.
```

**void * weil C nicht weiß welchen Datentypen wir wollen von der Funktion**

---
## Make Sure the Calls Were Successful

```c
const size_t size = 1234;  // any value determined at runtimeint 
*array = (int*) malloc(size * sizeof(int));
if (array == NULL) {  // NULL pointer means no memory was allocated  
	fprintf(stderr, "malloc %lu bytes failed\n", size);  
	exit(EXIT_FAILURE);} // use the array ...free(array);
```

### Limited Size of the Stack

Determine the size of the stack via

```bash
$ ulimit -s  # or `ulimit -a` for all limits
```

Impossible to exceed the given stack size

```c
#include <stdio.h>
int main(void) {  
int array[8192 * 1024 / 4];// use 8192 kB if sizeof(int) = 4  
printf("Survived?\n");  
return 0;}
```

Try to compile and run [exceed_stack_size.c](https://bulme.find-santa.eu/data/c/free_store/exceed_stack_size.c)

---

## Examples
### Allocate memory for an array

```c
#include <stdio.h>#include <stdlib.h>int main(void) {  const size_t size = 12;  // any value determined at runtime  
int *array = (int*) malloc(size * sizeof(int));  
if (array == NULL) { exit(EXIT_FAILURE); }  
for (size_t i = 0; i < size; ++i) {    
array[i] = i * i;  // initialize the array ...  }  
for (size_t i = 0; i < 3; ++i) {  // use the array ...    
printf("array[%lu]: %d\n", i, array[i]);  
}  
free(array);  // otherwise memory will grow when the program keeps running  return 0;}
```

[source/c/free_store/allocate_array.c](http://pythontutor.com/iframe-embed.html#code=%23include%20%3Cstdio.h%3E%0A%23include%20%3Cstdlib.h%3E%0Aint%20main(void)%20%7B%0A%20%20const%20size_t%20size%20%3D%2012%3B%20%20%2F%2F%20any%20value%20determined%20at%20runtime%0A%20%20int%20*array%20%3D%20(int*)%20malloc(size%20*%20sizeof(int))%3B%0A%20%20if%20(array%20%3D%3D%20NULL)%20%7B%20exit(EXIT_FAILURE)%3B%20%7D%0A%20%20for%20(size_t%20i%20%3D%200%3B%20i%20%3C%20size%3B%20%2B%2Bi)%20%7B%0A%20%20%20%20array%5Bi%5D%20%3D%20i%20*%20i%3B%20%20%2F%2F%20initialize%20the%20array%20...%0A%20%20%7D%0A%20%20for%20(size_t%20i%20%3D%200%3B%20i%20%3C%203%3B%20%2B%2Bi)%20%7B%20%20%2F%2F%20use%20the%20array%20...%0A%20%20%20%20printf(%22array%5B%25lu%5D%3A%20%25d%5Cn%22%2C%20i%2C%20array%5Bi%5D)%3B%0A%20%20%7D%0A%20%20free(array)%3B%20%20%2F%2F%20otherwise%20memory%20will%20grow%20when%20the%20program%20keeps%20running%0A%20%20return%200%3B%0A%7D%0A&curInstr=0&mode=display&py=c_gcc9.3.0)

### Allocate larger amounts of memory

```c
#include <stdio.h>#include <stdlib.h>int main(void) {  size_t size = 8192 * 1024;  // 8 MB  int *array = (int*) malloc(size);  if (array == NULL) {    fprintf(stderr, "malloc %lu bytes failed\n", size);    exit(EXIT_FAILURE);  }  for (size_t i = 0; i < size / sizeof(int); ++i) {    array[i] = i * i;  // initialize the array ...  }  printf("Survived?\n");  free(array);  // avoid memory leak  return 0;}
```

Download [allocate_large_array.c](https://bulme.find-santa.eu/data/c/free_store/allocate_large_array.c)

---


# EXERCISES

https://bulme.find-santa.eu/exercises/c/exercise_free_store/