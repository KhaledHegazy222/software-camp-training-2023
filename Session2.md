# C programming basic 2

## Table of Contents

- [Preprocessor Directives](#preprocessor-directives)
- [Functions](#functions)
- [Recursion](#recursion)

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



