# C programming basic 2

## Table of Contents

- [Preprocessor Directives](#preprocessor-directives)
- [Functions](#functions)
- [Recursion](#recursion)
- [Important Keywords](#important-keywords)
- [User-defined Data types](#user-defined-data-types)

### Preprocessor Directives

> Preprocessor directives are commands that are processed by the C preprocessor before the actual compilation of the code begins. They start with a pound sign `#` and are used to perform various tasks such as including header files, defining macros, and conditional compilation.

common preprocessor directives:

```C
    #include    // used to include header files
    #define     // used to define macros

    // the others will be discussed later
    #ifdef
    #ifndef
    #if
    #else
    #error
    #pragma
```

### Functions

> A function in C is a block of code that performs a specific task and is used to break down a program into smaller, reusable pieces. It is defined with a name, a return type, and a set of parameters that specify the input values.

- Syntax:

  ```C
      return_type function_name(parameter1, parameter2, ...) {

          // Code that performs a specific task

          // Return statement
          return result;
      }
  ```

  for example:

  ```C
      int add(int a, int b) {
          int result = a + b;
          return result;
      }

      int main(){
          int x = 11;
          int y = 12;

          printf("%d\n", add(x,y));
      }
  ```

  Common Standard functions in C:

        printf()
        scanf()
        abs()
        sqrt()
        pow()
        ceil()
        sin()
        cos()

- Applications:

  - Range Prime Checker Function:

    prototype :

          bool isPrime(int);

    body :

    ```C
        bool isPrime(int x){
            if(x < 2)
                return false;
            for(int i = 2;i < x;i++){
                if(x % i == 0)
                    return false;
            }
            return true;
        }
    ```

    usage:

    ```C

        // Calculate The number of primes in Range from Left to Right

        int left,right;
        scanf("%d%d",&left,&right);
        int primeNumbers = 0;
        for(int i = left;i <= right;i++){
            if(isPrime(i))
                primeNumbers++;
        }
        printf("The number of Primes in Range [%d : %d] = %d",left,right,primeNumbers);


    ```

  - Power Function:

    prototype :

          int power(int,int);

    body :

    ```C
        int power(int b,int p){
            int result = 1;
            while(p--){
                result *= b;
            }
            return result;
        }
    ```

    usage:

    ```C

        // Evaluate This Function (F) for any value of (x)
        // F(x) = 11 * (x ^ 4) - 3 * (x ^ 3) + 12 * x  - 25

        int x;
        scanf("%d",&x);

        int result = 11 * power(x,4) - 3 * power(x,3) + 12 * x - 25;

        printf("F(%d) = %d",x,result);


    ```

### Recursion:

> Defining a problem in terms of itself.

for example:

```C
    int factorial(int n) {
        if (n == 0) {
            return 1;
        }
        else {
            return n * factorial(n-1);
        }
    }
```

Let's see how this function works for the input `n = 5` :

    factorial(5)    = 5 * factorial(4)
                    = 5 * 4 * factorial(3)
                    = 5 * 4 * 3 * factorial(2)
                    = 5 * 4 * 3 * 2 * factorial(1)
                    = 5 * 4 * 3 * 2 * 1 * factorial(0)
                    = 5 * 4 * 3 * 2 * 1 * 1
                    = 120

Another example of a recursive function in C is the Fibonacci sequence :

```C
    int fibonacci(int n) {
        if (n == 0 || n == 1) {
            return n;
        }
        else {
            return fibonacci(n-1) + fibonacci(n-2);
        }
    }

```

Let's see how this function works for the input `n = 4` :

    fibonacci(4)    = fibonacci(3) + fibonacci(2)
                    = (fibonacci(2) + fibonacci(1)) + (fibonacci(1) + fibonacci(0))
                    = ((fibonacci(1) + fibonacci(0)) + 1) + (1 + 0)
                    = ((1 + 0) + 1) + (1 + 0)
                    = 3

### Important Keywords

- local vs global

  > Local variables are declared inside a function or block of code and can only be accessed within that function or block. They have a limited lifetime and are destroyed when the function or block of code exits.

  > Global variables, are declared outside of any function or block of code and can be accessed from any part of the program. They have a longer lifetime and exist throughout the entire execution of the program.

  for example :

  ```C
      #include <stdio.h>

      int global_var = 10;

      void my_function() {
          int local_var = 20;
          printf("local_var = %d\n", local_var);
          printf("global_var = %d\n", global_var);
      }

      int main() {
          my_function();
          printf("global_var = %d\n", global_var);
          return 0;
      }
  ```

- Static

  > In C, the `static` keyword is used to limit the scope or lifetime of a variable or function to the current file or block, respectively.

  for example:

  ```C
      int howManyCalls() {
          static int x = 0;
          x++;
          return x;
      }

      int main() {
          printf("This function get called %d Time(s).\n",howManyCalls()); // 1
          printf("This function get called %d Time(s).\n",howManyCalls()); // 2
          printf("This function get called %d Time(s).\n",howManyCalls()); // 3
          printf("This function get called %d Time(s).\n",howManyCalls()); // 4
          printf("This function get called %d Time(s).\n",howManyCalls()); // 5
          return 0;
      }

  ```

  Important Note:

  `static` keyword is used also in another cases (with global variables and function) and will be discussed later.

- Constant

  > In C, the `const` keyword is used to define a variable that cannot be modified after its initialization.

  syntax:

        const <data_type> <variable_name> = <initial_value>;

  for example:

  ```C
      const int MAX_VALUE = 100;
      int main() {
          // Attempting to modify a const variable will result in a compiler error
          MAX_VALUE = 200;
          return 0;
      }
  ```

- Register:

  > Register is a keyword in C which suggests the system to use register as a memory for a variable instead of RAM.

  Syntax:

      register <datatype> <variable_name>;

  for example:

  ```C
      #include <stdio.h>

      int main()
      {
          for(register int i = 1; i <= 5; i++)
              printf("%d", i);
          return 0;
      }
  ```

  Some key points regarding register in C:

  - register only suggests using register memory
  - We cannot get the memory location of such a variable

    Normal way of getting memory location of a variable is using the & operator like:

    ```C
        int i = 0;
        printf("%p", &i);
    ```

    output:

          0x7fff3d4f4934

    If i, the variable is declared as a register, it will give compile time error. For example:

    ```C
        register int i = 0;
        printf("%p", &i);
    ```

    Compile time error:

          opengenus.c: In function 'main':
          opengenus.c:6:5: error: address of register variable 'i' requested
              printf("%p", &i);
              ^

  - We can get the size using sizeof()

### User-defined Data types

- Structure

  > a structure (struct) is a composite data type that allows you to group together variables of different data types into a single unit.

  Syntax:

        The syntax for defining a struct in C is as follows:
            struct struct_name {
                data_type member1;
                data_type member2;
                .
                .
                .
                data_type memberN;
            };

        Declaration:
            struct struct_name variable_name;

        Initialization:
            struct struct_name variable_name = {value1, value2, ..., valueN};

        To access the members of a struct variable, you can use the dot (.) operator.
        Accessing:
            variable_name.member1 = value;

  for example:

  ```C
      #include <stdio.h>

      struct employee {
          char name[50];
          int age;
          float salary;
      };


      int main(){

          struct employee emp1 = {"John Doe", 30, 5000.0};
              printf("Employee name: %s\n", emp1.name);
              printf("Employee age: %d\n", emp1.age);
              printf("Employee salary: %f\n", emp1.salary);

          }
  ```

  the output:

        Employee name: John Doe
        Employee age: 30
        Employee salary: 5000.000000

- Union

  > ser-defined data type that allows you to store different types of data in the same memory location. A union is similar to a structure in C, but with one major difference: a structure stores each of its members in a `separate memory location`, while a union stores all of its members in the `same memory location`.

  Syntax:

        The syntax for defining a struct in C is as follows:
            union union_name {
                data_type member1;
                data_type member2;
                .
                .
                .
                data_type memberN;
            };


        Declaration:
            union union_name variable_name;

        Initialization:
            union union_name variable_name = {value1, value2, ..., valueN};

        To access the members of a union variable, you can use the dot (.) operator.
        Accessing:
            variable_name.member1 = value;

  for example:

  ```C
      union my_union {
          int x;
          float y;
      };

      int main() {
          union my_union u;
          u.x = 10;
          printf("Value of u.x: %d\n", u.x);
          u.y = 3.14;
          printf("Value of u.y: %f\n", u.y);
          printf("Value of u.x: %d\n", u.x);
          return 0;
      }
  ```

  the output:

        Value of u.x: 10
        Value of u.y: 3.140000
        Value of u.x: 1078523331

- enum

  > enum is a user-defined data type that allows you to define a set of named constants.

  Syntax:

        enum enum_name {
            identifier1,
            identifier2,
            .
            .
            .
            identifierN
        };

  for example:

  ```C
      #include <stdio.h>

      enum months {
          JAN = 1,
          FEB,
          MAR,
          APR,
          MAY,
          JUN,
          JUL,
          AUG,
          SEP,
          OCT,
          NOV,
          DEC
      };

      int main() {
          enum months m = MAY;
          printf("Month number: %d\n", m); // 5
          return 0;
      }
  ```

  another example:

  ```C
      #include <stdio.h>

      enum fruits {
          APPLE = 10,
          ORANGE = 20,
          BANANA = 30
      };

      int main() {
          enum fruits f = ORANGE;
          printf("Fruit value: %d\n", f); // 20
          return 0;
      }
  ```
