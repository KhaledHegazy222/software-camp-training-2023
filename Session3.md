# Pointers

## Table of Contents

-   [Definition of pointers](#definition-of-pointers)
-   [Pointers Classifications](#pointers-classifications)
-   [Pointers Arithmetic](#pointers-arithmetic)
-   [Pointers casting](#pointers-casting)
-   [Dynamic Memory Allocation](#dynamic-memory-allocation)
-   [Pointer vs Array](#pointer-vs-array)
-   Pointers and functions
-   Pointer to pointer

### Definition of pointers

> In the C programming language, a pointer is a variable that stores the memory address of another variable.

-   declaration

    ```C
        // To declare a pointer variable in C, you use an asterisk (*) symbol
        int* integerPointer;    // pointer to integer   (can read or write 4 bytes)
        char* charPointer;      // pointer to character (can read or write 1 byte)
        double* doublePointer;  // pointer to double    (can read or write 8 bytes)
    ```

-   initialization
    ```C
        int myVar = 5;          // declares an integer variable
        int *myPtr = &myVar;    // assigns the address of myVar to myPtr
    ```

Important notes :

-   `*` Operator is used in multiple scenarios :

    1. when defining the pointer `Declaration`
    2. when accessing the pointer's value `Dereferencing`
    3. multiplication `binary arithmetic operator`

-   `&` Operator is used in multiple scenarios :
    1. Bitwise And `binary bitwise operator`
    2. address of operator `unary operator`

### pointers classifications

-   Type-specific pointers:

          int*
          char*
          ...

-   void pointer `void*`
-   Wild pointers
-   Dangling pointers
-   null pointers

### Pointers Arithmetic

> The only rule to take care about is that the type of the pointer is an indicator for what is the number of bytes that it points to.

-   Addition

    -   Increment operator (++):

              When you use the ++ operator on a pointer, the pointer is incremented to point to the next memory location of the same data type.

        For example:

        ```C
            int arr[] = {1, 2, 3, 4, 5};
            int *ptr = &(arr[0]);
            printf("%d ", *ptr);  // Output: 1
            ptr++;
            printf("%d ", *ptr);  // Output: 2
        ```

    -   Addition operator (+):

              When you use the + operator on a pointer, the pointer is incremented by a certain number of bytes, based on the data type of the pointer.

        for example:

        ```C
            int arr[] = {1, 2, 3, 4, 5};
            int *ptr = &(arr[0]);
            printf("%d ", *ptr);  // Output: 1
            ptr = ptr + 2;
            printf("%d ", *ptr);  // Output: 3
        ```

-   Subtraction

    -   Decrement operator (--):

              When you use the -- operator on a pointer, the pointer is decremented to point to the previous memory location of the same data type.

        for example:

        ```C
            int arr[] = {1, 2, 3, 4, 5};
            int *ptr = &(arr[2]);
            printf("%d ", *ptr);  // Output: 3
            ptr--;
            printf("%d ", *ptr);  // Output: 2
        ```

    -   Subtraction operator (-):

              When you use the - operator on a pointer, the pointer is decremented by a certain number of bytes, based on the data type of the pointer.

        for example:

        ```C
            int arr[] = {1, 2, 3, 4, 5};
            int *ptr = &(arr[2]);
            printf("%d ", *ptr);  // Output: 3
            ptr = ptr - 2;
            printf("%d ", *ptr);  // Output: 1
        ```

    -   Subtraction of two pointers:

              When you subtract two pointers, the result is the number of elements between them.

        for example:

        ```C
            int arr[] = {1, 2, 3, 4, 5};
            int *ptr1 = &arr[0];
            int *ptr2 = &arr[3];
            printf("%d ", ptr2 - ptr1);  // Output: 3
        ```

### Dynamic memory allocation

> Dynamic memory allocation in C is a technique that allows you to allocate and deallocate memory during runtime using `HEAP`.

This is done using the following functions:

-   malloc

    prototype:

    ```C
        void* malloc(size_t size);
    ```

          The malloc() function returns a pointer to the first byte of the allocated memory block, or NULL if the memory allocation fails.

    for example:

    ```C
        int *ptr;
        ptr = (int*) malloc(4);
    ```

-   free

    prototype:

    ```C
        void free(void *ptr);
    ```

          The free() function is used to release dynamically allocated memory back to the system, allowing it to be used by other parts of the program.

for example:

```C
    int* ptr;
    int n = 5; // number of integers to allocate

    // allocate memory for n integers
    ptr = (int*) malloc(n * 4);

    // initialize the memory with some values
    for(int i=0; i<n; i++) {
        *(ptr + i) = i + 1;
    }

    // print the values of the memory
    for(int i=0; i<n; i++) {
        printf("%d ", *(ptr + i));
    }

    // free the allocated memory
    free(ptr);
```

### Pointers Casting

> pointer casting refers to the process of converting one type of pointer to another.

usage:

    This is often necessary when working with void pointers, which are generic pointers that can point to any data type.

for example:

```C
   int x = 10;
   void* p = &x;

   // cast the void pointer to an int pointer
   int* q = (int*) p;

   // dereference the int pointer and print the value
   printf("%d\n", *q);
```

### Pointer vs Array

> Arrays and Pointers are similar in that they both deal with memory locations in C, but they have some key differences. Arrays are `fixed` in size and can be accessed using the subscript operator, while pointers are variables that store memory addresses and can be reassigned to point to `different` memory locations.

for example:
```C
    int arr[3] = {1, 2, 3};
    for (int i = 0; i < 3; i++) {
        printf("%d ", arr[i]);
    }

    ////////////////////////////////

    int ptr = (int*) malloc(3 * 4);
    *(ptr + 0) = 1;
    *(ptr + 1) = 2;
    *(ptr + 2) = 3;
    for (int i = 0; i < 3; i++) {
        printf("%d ", *(ptr + i));
    }

    ////////////////////////////////
    
    int arr[3] = {1, 2, 3};
    int *ptr = arr; // arr == &arr[0];
    for (int i = 0; i < 3; i++) {
        printf("%d ", *(ptr + i));
    }
    int arr2[3] = {4,5,6};
    ptr = arr2;
    for (int i = 0; i < 3; i++) {
        printf("%d ", ptr[i]);
    }

    ////////////////////////////////

    int arr[3] = {1, 2, 3};
    int *ptr = arr; // arr == &arr[0];
    for (int i = 0; i < 3; i++) {
        printf("%d ", *(ptr + i));
    }
    int arr2[3] = {4,5,6};
    arr = arr2;
    for (int i = 0; i < 3; i++) {
        printf("%d ", arr[i]);
    }
```



### Pointers with functions

- Parameter
    
    examples:
    ```C
        void addStore(int a,int b,int *c){
            *c = a + b;
        }

        int main(){
            int a,b,c;
            a = 10;
            b = 11;
            addStore(a,b,&c);
            printf("%d\n",c);
        }
    ```



    ```C
        void swap(int a,int b){
            int c = a;
            a = b;
            b = c;
        }
        int main(){
            int a,b;
            a = 10;
            b = 11;
            printf("%d %d\n",a,b); // 10 11
            swap(a,b);
            printf("%d %d\n",a,b); // 10 11
        }


        // The correct version for swap
        
        void swap(int* a,int* b){
            int c = *a;
            *a = *b;
            *b = c;
        }
        int main(){
            int a,b;
            a = 10;
            b = 11;
            printf("%d %d\n",a,b); // 10 11
            swap(&a,&b);
            printf("%d %d\n",a,b); // 11 10
        }

    ```



- Return Value

example:

```C
    // What is wrong with this code ? 
    int* fun(){
        int x = 11;
        return &x;
    }

    int main(){
        int* ptr = fun();
        printf("%d\n",*ptr);
    }


    // Correct Version
    int* fun(){
        int *x = malloc(4);
        *x = 11;
        return x;
    }

    int main(){
        int* ptr = fun();
        printf("%d\n",*ptr);
    }
```
