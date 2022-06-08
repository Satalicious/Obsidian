##### Header Guards
```c
#ifndef FILENAME_H
#define FILENAME_H
// ... your header file's code or/and #include

#endif // FILENAME_H
```


##### Pointers
- **stores the memory address of a variable**
=> to pass arrays to functions
=> to change parameter values from a function

Changing a variable with a pointer.
```c
int a = 5;
int* a_ptr = &a;
*a_ptr += 5;
// a is now 10
```
##### DMM 

###### Basics:
```c
#include <stdlib.h>

void *malloc(size_t size)
Allocates `size` bytes and returns a pointer to the allocated memory. The memory is not initialized.

void free(void *ptr)
Frees the memory space pointed to by `ptr`.

void *calloc(size_t nmemb, size_t size)
Allocates memory for an array of `nmemb` elements of `size` bytes each and returns a pointer to the allocated memory. The memory is set to zero.

void *realloc(void *ptr, size_t size)
Changes the size of the memory block pointed to by ptr to size bytes.
```
Allocate memory and making sure that the operation worked:
```c
const size_t size = 1234; 
int *array = (int*) malloc(size * sizeof(int)); 
if (array == NULL) { 
	fprintf(stderr, "malloc %u bytes failed\n", size); 
exit(EXIT_FAILURE); 
} 
// use the array, afterwards dont forget to free it
free(array);
```

When you want to read a STRING from stdin:
```c
printf("Enter the first name: ");  fgets(s.first_name, 30, stdin);  s.first_name[strcspn(s.first_name, "\n")] = '\0';
```

When you want to read an INT from stdin:
```c
char buffer[20];
printf("how much resistors do you have?\n");
fgets(buffer,20,stdin);
sscanf(buffer, "%d",&n);

for (int i = 0; i < n; i++) { // just an example
```

##### Structs
Following struct is already coded:
```c
struct intarray {  
size_t reserved;  // available storage  
size_t elements;  // current number of elements
int* array;
};
```
- Creating a new datatype, based on the above struct would look like this: // this line has to be 
```c
typedef struct intarray IntArray;
```
- Now we can allocate memory for the new struct in main and work with the elements of IntArray (e.g. adding 10 elements):
```c
int main() {
IntArray* dummy = malloc(sizeof(IntArray));
dummy->array = malloc(10*sizeof(int)) // space for 0-9 int's
dummy->reserved = 10;
dummy->elements = 10;
for (int i = 0; i < 10; i++) {
	dummy->array[i] = i;
	}
free(array); // avoid memory leak
return 0;
}
```
---

#### C++
```c
#include <iostream>
#include <string>
#include <vector>

using std::cout;

int main() {
int a_number(3);  // an integral value
double value = 13.7404;  // double precision floating point value
char sep = '\t';  // single character (escaped tab key)
std::string name("Amelie");  // C++ string
std::vector<double> numbers(3);  // a managed array of doubles
cout << a_number << sep << value << std::endl;
cout << name << std::endl;
for (auto& number : numbers) {
    cout << number << sep;  // dereference the iterator
  }
cout << std::endl;
return 0;
}
```
OUTPUT:
![[Pasted image 20220608123919.png]]

##### FOR LOOPS
![[Pasted image 20220608125142.png]]


FIND MAX
```c
#include <stdio.h>
int max(const int *array, int dimension) {
int value = 0;
	while (dimension--) {
		if (*array > value)
			value = *array;
			
		array++;
   }
    return value;
}
int main() {
int arr[100] = {4, 1, 7, 5, 8, 1, 4, 2, 3, 1, 100};

printf("highest number is %d\n", max(arr, 10));
return 0;
}
```