# C programming basic 1

## Table of Contents

-   [Variables](#variables)
-   [Interacting with user](#interacting-with-user)
-   Casting
    -   Implicit
    -   Explicit
-   Operators
    -   Types of Operators in C
        -   Arithmetic
        -   Logical
        -   Bitwise
        -   Relational
        -   Additional Operators in C [ `,` , `.` , `=` , `&` , `*` , `sizeof` , `[]` , `?:` ]
    -   Logical vs Bitwise operators
    -   Applications of operators
        -   Get Bit
        -   Set Bit
        -   Clear Bit
        -   Toggle Bit
-   Comments%d	Signed integer
%u	Unsigned integer
%f	Floating-point number
%lf	Double-precision floating-point number
%c	Character
%s	String
%p	Pointer
-   Expressions
-   Branching
    -   Conditional Branching
        -   if
        -   switch
        -   Ternary Operator
    -   Unconditional Branching
        -   Goto
-   Loops
    -   Forward vs Backward Branching
    -   Types of Loops
    -   Keywords
        -   Continue
        -   Break
-   Arrays
    -   Structure
    -   Storage in memory
    -   Declaration vs Initialization
    -   Accessing Elements
    -   Iterating over array
    -   Special types of arrays
        -   Character array
    -   Multidimensional Array
    -   sizeof operator with array
-

### Variables

-   Declaration vs Initialization

          Declaration Statement :
              [data type] [variable name];

    For Example:

    ```C
        int x;
        float y;
        char z;
    ```

          Initialization Statement :
              [data type] [variable name] = [expression];

    For Example:

    ```C
        int x = 11;
        float y = 12.3;
        char z = 'z';
    ```

-   Data types

          bool : Boolean
          [signed / unsigned] char : character
          [signed / unsigned] [short / long / long long] int : integer
          float : floating decimal point
          double : double precision floating decimal point

-   Naming Rules
-   Naming Convention

    For a variable represents the `"online students number"`

    ```C
        // Snake Case :
            int online_students_number;
        // Camel Case :
            int onlineStudentsNumber;
        // Pascal Case :
            int OnlineStudentsNumber;
        // Kebab Case :
            int online-students-number; // not valid in variable naming rules in C
    ```

-   Storage in memory

-   Behavior

    -   Overflow

        > Overflow occurs when you attempt to store inside any variable a value that is larger than the maximum value that it can hold.

        for example :

        ```C
        	unsigned char x = 250; // Maximum Value this data type can store is 255
        	x += 5;
        	printf("%d\n", x); // Now x = 255 (Maximum)
        	x++;               // After this increment x will roll back to Minimum Value
        	printf("%d\n", x); // Now x = 0

        ```

    -   Garbage value

        > A garbage value refers to an unpredictable and undefined value stored in a variable or memory location that has not been explicitly initialized.

        for example:

        ```C
        	int x; // declaring variable x without initializing it
        	printf("The value of x is: %d\n", x); // Here prints Random Number
        ```

        ```C
        	int x = 0; // initializing variable x to a specific value
        	printf("The value of x is: %d\n", x); // Here prints 0
        ```

### Interacting with user

-   Input

	> To read from input stream you can use `scanf()` function.

	Function Prototype:

	```C
		// scanf([format string],number of variable addresses)
		int scanf(const char *format, ...);
	```

	for example :

	```C
		// To Read One Variable
		int x;
		scanf("%d", &x);

		// To Read More than one Variable
		int x, y;
		scanf("%d%d",&x, &y);
	```

-   Output

	> To print to output stream you can use `printf()` function.

	Function Prototype:

	```C
		// printf([format string],number of expression)
		int printf(const char *format, ...);
	```

	for example :

	```C
		// To print One Variable
		int x = 1;
		printf("%d", x);

		// To print More than one Variable
		int x = 1, y = 2;
		printf("%d%d", x, y);
	```
- Format String

	> It specifies the format of the input or output that the function will read or write containing conversion specifiers.

	Conversion specifiers:
	
		%d	Signed integer
		%u	Unsigned integer
		%f	Floating-point number
		%lf	Double-precision floating-point number
		%c	Character
		%s	String
		%p	Pointer