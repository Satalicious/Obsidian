#  ARRAYS
----------------------------------------

Arrays can be initialised using the following methods:
1. Initiator with a size

```c
int arr[5] = { 0, 1, 2, 3, 4 };
```

*If fewer values than the size of the arrays are provided, the other elements for which values are not specified will be set to 0. *

Example: 
```c
int arr[4] = {10, 2};

for (int i = 0; i < 4; i++) {
	printf("%d ", arr[i]);
}
```

will output: 10 2 0 0

2. Initiator without a size:

```c
int arr[] = { 0, 1, 2, 3, 4, 5, 6 };
```

The compiler will be forced to assume that the size of the array is the same as the length of the initiator.

*How many types of arrays are there in C?*
<details>
3  <br>
Arrays in C can be of types int, float and char (also known as string).
</details>

*Can there be elements of different data types in an array in C?*
<details>
No, different from Python and some other C-descendants such as Javascript, elements in the same array in C cannot be of different types. <br>
To store different data type in the same structure in C, struct is often used.
</details>

==About the sizeof operator: ==
sizeof is an unary operator (not a function!) with highest possible priority.
*unary means there is only one argument to go with sizeof*
*operator means the use of parentheses () in most cases are optional.*

Parentheses are absolutely necessary to be used with sizeof only if the argument is an expression or a type (of data, e.g. int, char, float, double)

Example: 
```c
int i; // i is a variable of type int
int int_size = sizeof i; 
```

- this is a fully valid assignment, as i is a variable and can be used with sizeof operator without parentheses.
- The programme outputs no error.

```c
int int_size = sizeof (4/ 3); 
```

- this is a fully valid assignment, as 4/3 is an expression (here it is a mathematic operation).
- Parentheses are needed here because the division operator ( / ) has lower priority than the operator sizeof.
- the programme outputs no error.

```c
int int_size = sizeof 4 / 3;
```

==Notice the lack of parentheses in this case.==
- Due to the lower priority of the division ( / ) operator, the programme will calculate the expression (sizeof 4) first (which equates to 4 bytes or 8 bytes, depending on computers), before dividing the result by 3.
- That's why depending on environment (or computer), the programme will output 1 ( 4 / 3) or 2 (8 / 3).
- The programme outputs no error.
- The expression is equal to the following:
int int_size = (sizeof 4) / 3;

Look at the following line of code:

```c
printf("\n%d", sizeof int);
```

- This time the programme will output an error, since int as a standalone keyword (no parentheses) is not a type operator.

- Therefore parentheses are needed for sizeof when its argument is a *type*:

```c
sizeof (int)
sizeof (float)
sizeof (struct)
```

--------------------------------
# SIZEOF AND CHAR ARRAYS (STRINGS)

Strings can be declared and initialised in the following ways:

1. String declaration:
```c
char string[10];
```

2. String declaration + initialisation:
```c
char string[10] = "hello"; 
```

```c
char string[10] = { 'h', 'e', 'l', 'l', 'o' };
```

3. Or assigned separately:
```c
string[0] = 'H';
```

*Is the following declation and initialisation valid in C? *
```c
char schule[10];
schule = "Bulme";
```

<details>
No, this is not valid in C<br>
<i>(A bit related to pointers here - can skip if wanted)</i><br>
This is because C compiler treats the name of the array (without index - e.g. schule) and the whole string ("Bulme") as pointers to 2 different reserved places in memory.<br>
When declared and initialised at the same time, like this:
<blockquote>	
char string[10] = "hello";
</blockquote>
Both sides (or pointers) of the assignment operator ( = ) point to the same place in memory.<br>
The expression is equal to the following:<br>
char* string = "hello"  -----> 0x12345 (both pointers named 'string' of type char and named "hello" point to the same address in memory)<br><br>
But when declared and initialised separately, like this:<br>
<blockquote>
char schule[10];<br>
schule = "Bulme"; </blockquote>
the first pointer, 'schule' already points to a reserved place in memory ( enough for an array of 10 elements, though they are all empty at the moment) and the second pointer "Bulme" when created would point to a different place in memory (an array of 6 filled elements).<br><br>
These are not regular pointer variables (remember that variables' values can be changed, or reassigned), so changing their addresses (or reassigning their values) is simply not possible, and strictly forbidden.<br>
The programme will output an error.
</details>

### SIZEOF AND STRINGS

*The operator sizeof can be used to determine the length of an array of type int or float. But can it be used to determine the length of an array of type char (or string)?*

<details>
No. Sizeof cannot be used to determine the length of a string.
This is because it cannot detect where the '\0' character, which signifies the end of the string, is.<br>
It will only returns the length of the whole character array, even if they are not completely filled.<br>
Example:
<blockquote>
char schule[20] = "HTL BULME";
</blockquote>
Only the first 10 indexes of the array are filled (counting the character '\0')<br>
So string's length should be 10.<br>
But sizeof operator will return 20, which is the total length of the character array when declared.
</details>


