## Pass by reference

```c
#include <stdio.h>
#include <math.h>
int main(int argc, const char * argv[])
{
	double pi = 3.14;
	double integerPart;
	double fractionPart;
	
	fractionPart = modf(pi, &integerPart);
	
	printf("integerPart = %.0f, fractionPart = %.2f\n", integerPart, fractionPart);
	return 0;
}

```



-   you supply a address (reference), and the function puts the data there



## Writing pass-by-reference functions

```c
void metersToFeetAndInches(double meters, unsigned int *ftPtr, double *inPtr) {
	double rawFeet = meters * 3.281;
	
	unsigned int feet = (unsigned int)floor(rawFeet);
	// Store the number of feet at the supplied address
	
	if (ftPtr) {
		printf("Storing %u to the address %p\n", feet, ftPtr);
		*ftPtr = feet;
	}
	
	double fractionalFoot = rawFeet - feet;
	double inches = fractionalFoot * 12.0;
	
	if (inPtr) {
		printf("Storing %.2f to the address %p\n", inches, inPtr);
		*inPtr = inches;
	}
}

int main(int argc, const char * argv[])
{
	double meters = 3.0;
	unsigned int feet;
	double inches;
	
	metersToFeetAndInches(meters, &feet, &inches);
	printf("%.1f meters is equal to %d feet and %.1f inches. \n", meters, feet, inches);
	
	return 0;
}
```

-   add if (...) for NULL CHECKING