# Addresses and Pointers

## Getting Address



```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
	int i = 17;
	printf("i stores its value at %p\n", &i);
	printf("this function starts at %p\n", main);
	return 0;
}


// i stores its value at 0x7ffeefbff4dc
// this function starts at 0x100003f00
```



## Stroing addresses in pointers

```c
float *ptr;

int main(int argc, const char *argv[]) {
    int i = 17;
    int *addressOfI = &i; // store the address in a pointer 
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
    return 0;
}
```



## Getting the data at an address

```c
int main(int argc, const char *argv[]) {
    int i = 17;
    int *addressOfI = &i; // store the address in a pointer 
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
    printf("the int stored at addressOfI is %d\n", *addressOfI); // use * to get the data, called dereference
    
    *addressOfI = 89; // amend the data in variable i 
	printf("Now i is %d\n", i); // Now i is 89
    return 0;
}
```



## How many bytes

```c
int main(int argc, const char * argv[])
{
	int i = 17;
	int *addressOfI = &i;
	printf("i stores its value at %p\n", addressOfI);
	*addressOfI = 89;
	printf("Now i is %d\n", i);
	printf("An int is %zu bytes\n", sizeof(int));
	printf("A pointer is %zu bytes\n", sizeof(int *));
	return 0;
}

```

-   Since the sizeof() returns a value of type `size_t`, the correct placeholder is %zu
-   The pointer is 4 bytes long if 32-bit, 8byets long if 64bits



## NULL

-   sometime we want a pointer to nothing 
-   A variable that can hold address, and store something in it that makes it explicit that the variable is not set to anything
-   We use NULL for this

```c 
float *myPointer;
// Set myPointer to NULL for now, I'll store an address there // later in the program
myPointer = NULL;

if (myPointer) {
    //myPointer is not NULL
} else {
    //myPointer is NULL
}

float *measuredGravityPtr = NULL;

if (measuredGravityPtr) {
    actualGravity = *measuredGravityPtr;
} else {
    actualGravity = estimatedGravity(planetRadius);
}

float actualGravity = measuredGravityPtr ? *measuredGravityPtr : estimatedGravity(planetRadius);
```



## Stylish Pointer Declarations

-   Putting the * directly next to the variable name makes this clearer.

```c
// COrrect way to declare a pointer\
float *powerPtr;
float *b, *c;
```

