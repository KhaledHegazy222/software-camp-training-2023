# C programming basic 1

## Table of Contents

-   [Variables](#variables)
-   [Interacting with user](#interacting-with-user)
-   Casting
    -   Implicit
    -   Explicit
-   [Operators](#operators)
-   [Comments](#comments)
-   Expressions
-   [Branching](#branching)
-   [Loops](#loops)
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

    For a variable represents the `online students number`

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

-   Format String

    > It specifies the format of the input or output that the function will read or write containing conversion specifiers.

    Conversion specifiers:

        %d	Signed integer
        %u	Unsigned integer
        %f	Floating-point number
        %lf	Double-precision floating-point number
        %c	Character
        %s	String
        %p	Pointer

### Operators

-   Types of Operators in C

    -   Arithmetic

        -   Unary

                  ++ [post increment] / [pre increment]
                  -- [post decrement] / [pre decrement]

                  For Pre operators :
                      The increment comes first then the evaluation
                  For Post operators :
                      The evaluation comes first then the increment

            for example:

            ```C
                // For Post Increment
                int x = 11;
                printf("%d\n",x++); // Here Prints 11
                printf("%d\n");     // Here Prints 12

                // For Pre Increment
                int y = 11;
                printf("%d\n",++y); // Here Prints 12
                printf("%d\n",y);   // Here Prints 12
            ```

            What Should be the printed value here :

            ```C
                int x = 12;
                int y = 11;
                printf("%d\n",++x + y--);
                printf("%d",x++ - ++y);
            ```

        -   Binary

                  +   Addition
                  -   Subtraction
                  *   multiplication
                  /   Division
                  %   Modulus [remainder of the division]

    -   Logical

            &&  Logical And
            ||  Logical Or
            !   Logical Not

    -   Bitwise

            &   Bitwise And
            |   Bitwise Or
            ~   One's complement
            ^   Bitwise Xor
            >>  Right Shift
            <<  Left Shift

    -   Relational

            ==
            !=
            <
            >
            >=
            <=

    -   Assignment

            =
            +=
            -=
            *=
            /=
            %=

    -   Additional Operators in C

            Will be Discussed Later:
            ,       Comma
            .       Dot
            &       Address-of
            *       Asterisk
            sizeof  Size-of
            []      Brackets
            ?:      Ternary Operator

-   Logical vs Bitwise operators

    > Logical operators are used to evaluate the truth value of logical expressions and return `boolean` values (true or false), whereas bitwise operators are used to perform operations on `individual bits` of `integer` values.

    for example :

    ```C
        int x = 3;
        int y = 4;
        printf("%d\n",x & y);   // Here the evaluation result = 0 (all bits = 0)
        printf("%d\n",x && y);  // Here the evaluation result = 1 (True)
    ```

-   Applications of operators
    -   Get Bit
    -   Set Bit
    -   Clear Bit
    -   Toggle Bit

### Comments

-   One line Comment

    > You can use double forward slashes `//` to create a comment in C. Any text following the // on the same line will be ignored by the compiler.

    for example:

    ```C
        int x = 11; //  this will be ignored
        int y = 11;     this will not be ignored
    ```

-   Multi line Comment

    > multi-line comments can be created by enclosing the comments within `/*` and `*/` delimiters. Any text within these delimiters will be ignored by the compiler, regardless of how many lines it spans.

    for example:

    ```C
        /*
        This is an example of a multi-line comment in C.
        Anything between the opening and closing delimiters
        will be ignored by the compiler, including any code or text
        that spans multiple lines.
        */
        int x = 11;
    ```

### Branching

-   Conditional Branching

    -   if condition

        ```C
            if(/* condition */) {
                // Statement
                // Statement
            }

            /***************************************/

            if(/* condition */) {
                // Statement
                // Statement
            }
            else{
                // Statement
                // Statement
            }

            /***************************************/

            if(/* condition */) {
                // Statement
                // Statement
            }
            else if(/* condition */) {
                // Statement
                // Statement
            }
            else{

            }
        ```

    -   switch case

        ```C
            switch (/* expression */) {
                case /* Constant decimal (non floating) numerical Value */ :
                    // Statement
                    // Statement
                    break;
                case /* Constant decimal (non floating) numerical Value */ :
                    // Statement
                    // Statement
                    break;
                case /* Constant decimal (non floating) numerical Value */ :
                    // Statement
                    // Statement
                    break;
                default:
                    // Statement
                    // Statement
            }
        ```

    -   Ternary Operator

        ```C
            // short handed way to write If-else conditions
            int x;
            if(/* condition */) {
                x = 1;
            }
            else{
                x = 2;
            }
            x = (/* condition */) ? 1 : 2;

            /*
                Important Note :
                the returned expressions in a ternary operator (?:) must be of the same type or have compatible types.

                for example :

                int a = 42;
                double b = 3.14;
                int result = (a > b) ? a : b;

                [this will generate compilation error]

            */
        ```

-   Unconditional Branching

    > unconditional branching can be achieved using the `goto` statement. The `goto` statement transfers control to the `labeled statement` specified as its argument.

    Syntax :

        // Backward Jumping

        labelName :

        ...

        goto labelName;

        OR

        // Forward Jumping

        goto labelName;

        ...

        labelName :

    for example :

    ```C
        int x;
        scanf("%d",&x);

        if(x == 11) {
            goto eleven;
        }
        else{
            goto otherwise;
        }


        eleven :
            printf("X equals eleven\n");
            return 0;

        otherwise:
            printf("X doesn't equal eleven\n");
            return 0;
    ```

    Important Note :

        In general, it is not considered good practice to use goto statements in C, because they can make the code more difficult to understand and maintain. Using goto statements can lead to spaghetti code, where the flow of control is difficult to follow and debug.

    See this example :

    ```C
        int i = 0;

        loop: // label
        printf("%d ", i);
        i++;
        if (i < 10) {
            goto loop; // unconditional jump to label
        }

        return 0;
    ```

### Loops

-   Types of Loops

    -   While

        Syntax:

        ```C
            while(/* condition */) {
                // Statement
            }
        ```

        for example:

        ```C
            int i = 0;
            while(i < 11) {
                printf("%d\n",i);
                i++;
            }
        ```

    -   For

        Syntax:

        ```C
            for(/* initialization */; /* condition */; /* increment/decrement */) {
                // Statement
                // Statement
            }
        ```

        for example:

        ```C
            for(int i = 0;i < 11;i++) {
                printf("%d\n",i);
            }
        ```

    -   Do While

        Syntax:

        ```C
            do {
                // Statement
                // Statement
            } while(/* Condition */)
        ```

        for example:

        ```C
            int x = 11;
            do {
                printf("%d\n",x);
                x--;
            } while(x >= 0);
        ```

-   Keywords
    -   Continue
        > `continue` is a keyword used in loops (for, while, and do-while) to skip the current iteration and move on to the next iteration. When continue is encountered in a loop, the remaining statements in the loop body are skipped, and control jumps back to the loop header to re-evaluate the loop condition.

        for example: 
        ```C
            for (int i = 0; i < 10; i++) {
                if (i == 5) {
                    continue;  // skip the rest of the loop body for i = 5
                }
                printf("%d ", i);
            }

            // 0 1 2 3 4 6 7 8 9
        ```
    -   Break
        > `break` is a keyword used in loops (for, while, and do-while) and switch statements to exit the loop or switch statement prematurely. When break is encountered in a loop or switch statement, the control immediately jumps to the statement immediately following the loop or switch.

        for example:
        ```C
        for (int i = 0; i < 10; i++) {
            if (i == 5) {
                break;   // exit the loop when i == 5
            }
            printf("%d ", i);
        }

        // 0 1 2 3 4
        ```