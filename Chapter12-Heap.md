# The Heap

Sometimes we need to claim a configuous chunk of memory or we called a buffer.

The buffer comes from a region of memory known as the heap, which is separate from the stack

On the heap, the buffer is independent of any function’s frame. Thus, it can be used across many functions. 

You request a buffer of memory using the function **malloc()**. 

When you are done using the buffer, you call the function **free()** to release your claim on that memory and return it to the heap.

```c
#include <stdio.h>
#include <stdlib.h> // malloc() and free() are in stdlib.h

int main(int argc, const char * argv[])
{
	// Declare a pointer
	float *startOfBuffer;
	
	// Ask to use some bytes from the heap
	startOfBuffer = malloc(1000 * sizeof(float));
	
	// ...use the buffer here...
	// Relinquish your claim on the memory so it can be reused
	free(startOfBuffer);
	
	// Forget where that memory is
	startOfBuffer = NULL;
	return 0;
}

```



`startOfBuffer` is a pointer to the address of the first floating point number in the buffer.



```c
#include <stdio.h>
#include <stdlib.h>
typedef struct {
	float heightInMeters;
	int weightInKilos;
} Person;

float bodyMassIndex(Person *p)
{
return p->weightInKilos / (p->heightInMeters * p->heightInMeters);
}

int main(int argc, const char * argv[])
{
	// Allocate memory for one Person struct
	Person *mikey = (Person *)malloc(sizeof(Person));
	
	// Fill in two members of the struct
	mikey->weightInKilos = 96;
	mikey->heightInMeters = 1.7;
	
	// Print out the BMI of the original Person
	float mikeyBMI = bodyMassIndex(mikey);
	printf("mikey has a BMI of %f\n", mikeyBMI);
	
	// Let the memory be recycled
	free(mikey);
	
	// Forget where it was
	mikey = NULL;
	
	return 0;
}

```

