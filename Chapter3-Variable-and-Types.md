# Chapter 3 - Variable and Types

## Types

-   You create a new variable by declaring its type and name
-   `float weight`
    -   type of the variable is `float`, its name is `weight`
    -   at this point, it does not have a value

-   must declare the type of each variable for two reasons
    -   lets compiler check your work and alert you possible mistakes
    -   tells how much space in memory reserve for that variable
-   short, int, long
-   float, double
-   char
-   pointer
-   struct



## A program with variables

```c
#include <stdio.h>

int main(int argc, const char * argv[]) {
	float weight;
	weight = 14.2;
	printf("The turkey weighs %f. \n", weight);
	
	float cookingTime;
	cookingTime = 15.0 + 15.0 * weight;
	
	printf("Cook it for %f minutes.\n", cookingTime);
	
	return 0;
}

```

-   the computer first multiplies weight by 15.0 and then adds that result to 15.0
-   multiplication has *precedence* over addition.