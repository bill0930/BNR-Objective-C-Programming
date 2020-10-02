# Chapter 4 - If else statment

```c
if (conditional) {
   // Execute this code if the conditional evaluates to true
} else {
   // Execute this code if the conditional evaluates to false
}

```

```c
float truckWeight = 34563.8;
// Is it under the limit?
if (truckWeight < 40000.0) {
	printf("It is a light truck\n"); 
} 
else {
	printf("It is a heavy truck\n"); 
}

float truckWeight = 34563.8;
// Is it under the limit?
if (truckWeight < 40000.0) {
	printf("It is a light truck\n"); 
}
```

-   In C, it was decided that 0 would represent **false**,
-   anything that is not zero would be considered **true**.



## Comparison and Logic Operators

-   <, >, <=, >=, ==, !=

-   ```c
    if ((truckWeight > 0.0) && (truckWeight < 40000.0)) {
    printf("Truck weight is within legal range.\n"); }
    ```

-   &&, ||, !

## Boolean variables

-   ```objective-c
    BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight < 40000.0)); 
    if (isNotLegal) {
    	printf("Truck weight is not within legal range.\n"); 
    }
    ```

-   A variable that can be `true` or `false` is a `boolean` variable

-   C programmingers have always used an int to hold a boolean value

-   Objective-C pgraommers typically use the type `BOOL` for boolean variable. (BOOL is an alias of integer type)

-   ```c
    #include <objc/objc.h>
    ```



## Curly Braces are optional

-   when the conditional expression consists of only ONE statement

-   ```c
    BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight < 40000.0)); 
    if (isNotLegal)
    	printf("Truck weight is not within legal range.\n");
    ```

## Else-if

```c
if (truckWeight <= 0) {
	printf("A floating truck\n");
} else if (truckWeight < 40000.0) { 
    printf("A light truck\n");
} else {
	printf("A heavy truck\n"); }
```

## Conditional Operators

```c
int minutesPerPound;
if (isBoneless) {
	minutesPerPound = 15; }
else {
	minutesPerPound = 20; }

int minutesPerPound = isBoneless ? 15 : 20;
```

