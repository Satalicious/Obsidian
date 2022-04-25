ARRAYS
----------------------------------------

Arrays can be initialised using the following methods:
- Initiator with a size
```c
int arr[5] = { 0, 1, 2, 3, 4 };
```
** If fewer values than the size of the arrays are provided, the other elements for which values are not specified will be set to 0.

Example: 

```c
int arr[4] = {10, 2};

for (int i = 0; i < 4; i++) {
	printf("%d ", arr[i]);
}
```

will output: **10 2 0 0**

- Initiator without a size:
int arr[] = { 0, 1, 2, 3, 4, 5, 6 };

The compiler will be forced to assume that the size of the array is the same as the length of the initiator.

>> How many types of arrays are there in C?
3: Arrays in C can be of types int, float and char (also known as string).

>> Can there be elements of different data types in an array in C?
No, different from Python and some other C-descendants such as Javascript, elements in the same array in C cannot be of different types.

To store different data type in the same structure in C, struct is often used.

>> About the sizeof operator:
sizeof is an unary operator (not a function!) with highest possible priority.
*unary means there is only one argument to go with sizeof
*operator means the use of parentheses () in most cases are optional.

Parentheses are absolutely necessary to be used with sizeof only if the argument is an expression or a type (of data, e.g. int, char, float, double)

Example: 
int i; // i is a variable of type int
int int_size = sizeof i; // this is a fully valid assignment, as i is a variable and can be used with sizeof operator without parentheses.
// The programme outputs no error.

int int_size = sizeof (4/ 3); // this is a fully valid assignment, as 4/3 is an expression (here it is a mathematic operation).
Parentheses are needed here because the division operator ( / ) has lower priority than the operator sizeof.
// the programme outputs no error.

int int_size = sizeof 4 / 3;
// Notice the lack of parentheses in this case.
// Due to the lower priority of the division ( / ) operator, the programme will calculate the expression (sizeof 4) first (which equates to 4 bytes or 8 bytes, depending on computers), before divide the result by 3.
// That's why depending on environment (or computer), the programme will output 1 ( 4 / 3) or 2 (8 / 3).
// The programme outputs no error.
// The expression is equal to the following:
int int_size = (sizeof 4) / 3;

Look at the following line of code:
printf("\n%d", sizeof int);

/*Need modification here. (int) is a datatype, int is not */
This time the programme will output error, since both sizeof and int, when standing separately, are operators of the same level of priority. They both expect one argument after them, so the lack of argument after the first operator sizeof would cause the programme to stop execution.

Therefore parentheses are needed for sizeof when its argument is a *type*:
sizeof (int)
sizeof (float)
sizeof (struct)


--------------------------------
SIZEOF AND CHAR ARRAYS (STRINGS)

Strings can be declared and initialised in the following ways:

char string[10]; // string declaration

char string[10] = "hello"; // string declaration + initialisation

char string[10] = { 'h', 'e', 'l', 'l', 'o' };

Or assigned separately:
string[0] = 'H';

>> Is the following declation and initialisation valid in C?
char schule[10];
schule = "Bulme";

No, this is not valid in C
(A bit related to pointers here - can skip if wanted)
This is because C compiler treats the name of the array (without index - e.g. schule) and the whole string ("Bulme") as pointers to reserved place in memory.

When declared and initialised at the same time, like this:
char string[10] = "hello";
Both sides (or pointers) of the assignment operator ( = ) point to the same place in memory.
The expression is equal to the following:
char* string = "hello"  -----> 0x12345 (both pointers named 'string' of type char and named "hello" point to the same address in memory)

But when declared and initialised separately, like this:
char schule[10];
schule = "Bulme"; 

the first pointer, 'schule' already points to a reserved place in memory ( enough for an array of 10 elements, though they are all empty at the moment) and the second pointer "Bulme" when created would point to a different place in memory (an array of 6 filled elements).

These are not regular pointer variables (remember that variables' values can be changed, or reassigned), so changing their addresses (or reassigning their values) is simply not possible, and strictly forbidden.
The programme will output error.

SIZEOF AND STRINGS

> The operator sizeof can be used to determine the length of an array of type int or float. But can it be used to determine the length of an array of type char (or string)?

No. Sizeof cannot be used to determine the length of a string.
This is because it cannot detect where the '\0' character, which signifies the end of the string, is.
It will only returns the length of the whole character array, even if they are not completely filled.
Example:

char schule[20] = "HTL BULME";

Only the first 10 indexes of the array are filled (counting the character '\0')
So string's length should be 10.
But sizeof operator will return 20, which is the total length of the character array when declared.

