##### Header Guards
```c
#ifndef FILENAME_H
#define FILENAME_H
// ... your header file's code or/and #include

#endif // FILENAME_H
```

##### DMM 
Allocate memory and making sure that the operation worked:
```c
const size_t size = 1234; 
int *array = (*int) malloc(size * sizeof(int)); 
if (array == NULL) { 
	fprintf(stderr, "malloc %u bytes failed\n", size); 
	exit(EXIT_FAILURE); } free(array);
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

for (int i = 0; i < n; i++) {
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
- Creating a new datatype, based on the above struct would look like this:
```c
typedef struct intarray Intarray;
```
- Now we can allocate memory for the new struct in main and work with the elements of intarray (e.g. add 10 ele):
```c
int main() {
IntArray* dummy = malloc(sizeof(IntArray));
dummy->array = malloc(10*sizeof(int)) // 10 el
dummy->reserved = 10;
for (int i = 0; i < 10; i++) {
	dummy->array[i] = i;
}
dummy->elements = 10;
}
```

