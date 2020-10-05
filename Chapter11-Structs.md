# Structs

Sometimes we need a variable to hold several related chunks of data, we need structures

```c
#include <stdio.h>

struct Person {
	float heightInMeters;
	int weightInKilos;
};


int main(int argc, const char * argv[])
{
	struct Person mikey;
	mikey.heightInMeters = 1.7;
	mikey.weightInKilos = 96;
	
	struct Person aaron;
	aaron.heightInMeters = 1.97;
	aaron.weightInKilos = 84;
	
	printf("mikey is %.2f meters tall\n", mikey.heightInMeters);
	printf("mikey weighs %d kilograms\n", mikey.weightInKilos);
	printf("aaron is %.2f meters tall\n", aaron.heightInMeters);
	printf("aaron weighs %d kilograms\n", aaron.weightInKilos);
	return 0;
}


```

-   you can access the members of a struct using a period (stylish programmers like to say “dot”).

```c
typedef struct {
    float heightInMeters;
    int weightInKilos;
} Person;

int main(int argc, const char * argv[])
{
	Person mikey;
	mikey.heightInMeters = 1.7;
	mikey.weightInKilos = 96;
	
	Person aaron;
	aaron.heightInMeters = 1.97;
	aaron.weightInKilos = 84;
	
	printf("mikey is %.2f meters tall\n", mikey.heightInMeters);
	printf("mikey weighs %d kilograms\n", mikey.weightInKilos);
	printf("aaron is %.2f meters tall\n", aaron.heightInMeters);
	printf("aaron weighs %d kilograms\n", aaron.weightInKilos);
	return 0;
}
```

-   A typedef defines an alias for a type declaration and allows you to use it more like the usual data types



```c
#include <stdio.h>
// Here is the declaration of the type Person
typedef struct {
    float heightInMeters;
    int weightInKilos;
} Person;

float bodyMassIndex(Person p)
{
return p.weightInKilos / (p.heightInMeters * p.heightInMeters); 
}

int main(int argc, const char * argv[])
{
    Person mikey;
    mikey.heightInMeters = 1.7; 
    mikey.weightInKilos = 96;
    
    Person aaron; 
    aaron.heightInMeters = 1.97; 
    aaron.weightInKilos = 84;
    
    float bmi;
    bmi = bodyMassIndex(mikey);
    printf("mikey has a BMI of %.2f\n", bmi);
    bmi = bodyMassIndex(aaron);
    printf("aaron has a BMI of %.2f\n", bmi);
    return 0; 
}

```

