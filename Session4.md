# Last Session in C

### Searching

-   Read the documentation of the languages

    for examples:

    -   Convert double to string
    -   generate random numbers
    -   File Handling

-   Explore New Libraries
    > We will be discussed briefly in Arduino Session

### Debugging

What is the problem with these code snippets

```C
    #include <stdio.h>

    int main() {
        int x = 5;
        if (x = 10) {
            printf("x is equal to 10\n");
        } else {
            printf("x is not equal to 10\n");
        }
        return 0;
    }
```

```C
    #include <stdio.h>

    int main() {
        int arr[5] = {1,2,3,4,5};
        unsigned int i = 4;
        while(i >= 0){
            printf("%d, ",arr[i]);
            i--;
        }
        return 0;
    }

```

```C
    #include <stdio.h>

    int main() {
        int arr[5] = {1, 2, 3, 4, 5};
        for (int i = 0; i <= 5; i++) {
            printf("%d ", arr[i]);
        }
        return 0;
    }

```

```C
    #include <stdio.h>

    int main() {
        int *p;
        *p = 10;
        printf("%d\n", *p);
        return 0;
    }

```

```C
    #include <stdlib.h>

    int main() {
        int *p = malloc(sizeof(int));
        *p = 10;
        return 0;
    }
```

### Clean Code

-   Meaningfully Names
-   Global Variable isn't best practice in C
-   Variable name consistent
-   Use searchable names

          // In the future we will not remember what 86400000 means.
          clearBacklog(backlog, 86400000);


          // Declare constants with a searchable name
          var MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;
          clearBacklog(backlog, MILLISECONDS_PER_DAY);

-   Don't repeat yourself (DRY)
    for example:

```C
    #include <stdio.h>

    int sum(int arr[], int size) {
        int result = 0;
        for (int i = 0; i < size; i++) {
            result += arr[i];
        }
        return result;
    }

    int main() {
        int arr1[] = {1, 2, 3, 4, 5};
        int arr2[] = {10, 20, 30};
        int sum1 = sum(arr1, 5);
        int sum2 = sum(arr2, 3);
        printf("Sum of arr1: %d\n", sum1);
        printf("Sum of arr2: %d\n", sum2);
        return 0;
    }
```


-   Uses highly descriptive variable names

    ```C
        const address = "One Infinite Loop, Cupertino 95014";
        var cityZipCodeRegex = new Regex(@"/ ^[^,\\] +[,\\\s] + (.+?)\s * (\d{ 5 })?$/").Matches(address);
        saveCityZipCode(
            cityZipCodeRegex[0].Value,
            cityZipCodeRegex[1].Value
        );
    ```

    ```C
        var address = "One Infinite Loop, Cupertino 95014";
        var cityZipCodeRegex = new Regex(@"/ ^[^,\\] +[,\\\s] + (.+?)\s * (\d{ 5 })?$/").Matches(address);
            var city = cityZipCodeRegex[0].Value;
            var zipCode = cityZipCodeRegex[1].Value;
        saveCityZipCode(city, zipCode);
    ```

-   Bad Code Examples

    -   Unconditional Branching

        ```C
        void foo() {
            int i = 0;
        start:
            printf("%d\n", i);
            i++;
            if (i < 10) {
                goto start;
            }
        }

        int main() {
            foo();
            return 0;
        }
        ```

    -   Check Null + Free after using the memory:

        ```C
        int *array = malloc(10 * sizeof(int));
        // do something with array
        ```

        > Fix

        ```C
            int *array = malloc(10 * sizeof(int));
            if (array == NULL) {
                perror("Error allocating memory");
                exit(EXIT_FAILURE);
            }
            // do something with array
            free(array);
        ```

    -   No Magical Numbers

        ```C
            if (status == 1) {
                // do something
            } else if (status == 2) {
                // do something else
            } else if (status == 3) {
                // do something different
            }
        ```

        > Fix

        ```C
            #define STATUS_OK 1
            #define STATUS_ERROR 2
            #define STATUS_WARNING 3

            if (status == STATUS_OK) {
                // do something
            } else if (status == STATUS_ERROR) {
                // do something else
            } else if (status == STATUS_WARNING) {
                // do something different
            }
        ```

    -   use const pointer if needed

        ```C
            void print_name(char *name) {
                name[0] = toupper(name[0]);
                printf("Name: %s\n", name);
            }

            int main() {
                char name[] = "john";
                print_name(name);
                return 0;
            }
        ```

        > Fix

        ```C
            void print_name(const char *name) {
                printf("Name: %s\n", name);
            }

            int main() {
                const char name[] = "john";
                print_name(name);
                return 0;
            }
        ```

    -   Common mistakes that kill your performance

        ```C
            void print_string(const char *str) {
                for (int i = 0; i < strlen(str); i++) {
                    printf("%c\n", str[i]);
                }
            }

            int main() {
                const char str[] = "hello";
                print_string(str);
                return 0;
            }
        ```

        > Fix

        ```C
            void print_string(const char *str) {
                size_t len = strlen(str);
                for (int i = 0; i < len; i++) {
                    printf("%c\n", str[i]);
                }
            }

            int main() {
                const char str[] = "hello";
                print_string(str);
                return 0;
            }
        ```

### Pointers Cont.

-   pointers to structure

    example:

    ```C
        #include <stdio.h>
        #include <stdlib.h>

        // Define a structure
        struct student {
            char name[50];
            int age;
            float gpa;
        };

        int main() {
            // Declare a pointer to a structure
            struct student *ptr;

            // Dynamically allocate memory for the structure
            ptr = (struct student*) malloc(sizeof(struct student));

            // Check if memory allocation was successful
            if (ptr == NULL) {
                printf("Memory allocation failed\n");
                exit(1);
            }

            // Access the members of the structure using the arrow operator (->)
            printf("Enter student name: ");
            scanf("%s", ptr->name);
            printf("Enter student age: ");
            scanf("%d", &ptr->age);
            printf("Enter student GPA: ");
            scanf("%f", &ptr->gpa);

            // Print the structure using the pointer and arrow operator
            printf("\nStudent information:\n");
            printf("Name: %s\n", ptr->name);
            printf("Age: %d\n", ptr->age);
            printf("GPA: %f\n", ptr->gpa);

            // Free the dynamically allocated memory
            free(ptr);

            return 0;
        }
    ```

-   use Cases

    > pointers to structure are used in data structures like:

    1. Linked Lists
    2. Stack
    3. Queue
    4. Tree
    5. Graph

    #### Linked List

    ![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist.png)

    #### Stack

    ![](https://i0.wp.com/learnersbucket.com/wp-content/uploads/2018/12/stack-2-1.png?fit=768%2C400&ssl=1)

    #### Queue

    ![](https://i0.wp.com/learnersbucket.com/wp-content/uploads/2019/01/Queue-2-1.png?resize=768%2C400&ssl=1)

### Recursion Cont.

-   Recursion Structure

    1. Base Case
    2. recursive call

    example:

    ```C
        //function definition
        int factorial(int num) {

        if (num == 1)  /* base case */
            return 1;
        else
            return (num * factorial(num - 1));
        }
    ```

    ```C
        int sum(int n) {
            if (n == 0)
                return 0
            else
                return n + sum(n - 1);
        }
    ```

-   Recursion Overhead

-   Why use recursion

    1. Complex tasks can be broken down into simpler problems.
    2. Code using recursion is usually shorter and more elegant.
    3. Sequence generation is cleaner with recursion than with iteration.

-   Why not to use recursion

    1. The recursive logic is usually harder to follow and debug.
    2. It increases memory usage and its Big O notation is often higher than the corresponding iterative solution.

-   How to write recursive code
    The answer is simple `Think Recursively`

-   Recursion simulation

    Trace this code below:

    ```C
        int func(int a,int b){
            if(b == 0)
                return 1;
            return a * func(a,b - 1);
        }
    ```

    ```C

    int max(int a,int b){
        if (a > b)
            return a;
        return b;
    }
    int fun(int arr[],int n){
        if n == 1:
            return arr[0];
        else:
            return max(arr[n-1], fun(arr, n-1));
    }
    ```

### C is Very powerful programming language

    The only limitation of what you can build is your imagination.

-   C / C++ programs examples

    -   Simple Login System
    -   Image filters
    -   Chess engines

### Additional Resources

-   [Neso Academy](https://www.youtube.com/playlist?list=PLBlnK6fEyqRhX6r2uhhlubuF5QextdCSM)
-   [Pointers in C](https://www.youtube.com/playlist?list=PL2_aWCzGMAwLZp6LMUKI3cc7pgGsasm2_)
-   [A Modern Approach](https://drive.google.com/file/d/129n7tb8gIAVDFftBgymHq98sgIkqw6oo/view?usp=share_link)
-   [Understanding and Using C Pointers](https://drive.google.com/file/d/15c38tNQJIIiem_PQErl_oHzkXc9ly8Fu/view?usp=share_link)
