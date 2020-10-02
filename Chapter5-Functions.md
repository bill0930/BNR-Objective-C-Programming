# Chapter 5 - Functions

## When should I use a function?

-   when you find yourself repeating work that is very similar in nature
-   help reduce effort in doing repetitve task

## How do I write and use a function?

```c
void congratulateStudent(char *student, char *course, int numDays)
{
	printf("%s has done as much %s Programming as I could fit into %d days.\n", student, course, numDays)
}

int main(int argc, const char * argv[]) {
    congratulateStudent("Kate", "Cocoa", 5); 
    congratulateStudent("Bo", "Objective-C", 2); 
    congratulateStudent("Mike", "Python", 5); 
    congratulateStudent("Liz", "iOS", 5); 
    
    return 0;
}

/** OUTPUT
Kate has done as much Cocoa Programming as I could fit into 5 days.
Bo has done as much Objective-C Programming as I could fit into 2 days. Mike has done as much Python Programming as I could fit into 5 days. Liz has done as much iOS Programming as I could fit into 5 days
**/
```

-   `void congratulateStudent(char *student, char *course, int numDays)`
    -   Each params has two parts, the type of data the argument represents and the name of the params
    -   params are separated by commas, and placed in parantheses to the right of the name of the function
    -   `void` nothing needed to return
    -   when called congratulateStudent(), you passed it values.
        -   value passed to a function are know as `arguments`
        -   The argument's value is then assigned to the corresponding parameter name
        -   That parameter name can be used inside the function as a variable that contains the passed-in value.

## How functions work together

```c
int main (int argc, const char * argv[])
{
congratulateStudent("Kate", "Cocoa", 5); sleep(2);
congratulateStudent("Bo", "Objective-C", 2); sleep(2);
congratulateStudent("Mike", "Python", 5); sleep(2);
congratulateStudent("Liz", "iOS", 5);
return 0; 
}

```

## Standard Library

-   Among the things that were installed as part of OS X were files containing a collection of precompiled functions. Those collections are called standard libraries

-   **Printf()** in stdio.h, **sleep()** in unistd.h

-   two purpose for standard library

    -   represents big chunks of code that you do not need to write and maintain thus empower you to build much bigger, better programs than you would be able to do otherwise.
    -   ensure that most programs look and feel similar

    

## Local Variables, frames, stack

### Local Variables

-   Local variables are variables declared inside a function

-   Local vaiables exist only during the execution of that function and can only accessed from within that function

- ```c
  void showCookTimeForTurkey(int pounds)
  {
  int necessaryMinutes = 15 + 15 * pounds;
  printf("Cook for %d minutes.\n", necessaryMinutes); 
  }
  ```
  
- `necessaryMinutes` is a local variable that only come into existence when **showCookTimeForTurkey** starts to execute and will cease to exist once that function completes execution.

- The parameters of the function, pounds is also a local variable

### Frames

- local variables are stored in the `frame` for that function

### Stack

-   Programmers use the word *stack* to describe where the `frames` are stored in memory. 

## Scope

-   Any pair of curly braces {...} define the scope of the code 
-   A variable cannot be accessed outside of the scope that it is declared in 

```c
void showCookTimeForTurkey(int pounds)
{
int necessaryMinutes = 15 + 15 * pounds; 
    printf("Cook for %d minutes.\n", necessaryMinutes); 
    if (necessaryMinutes > 120) {
        int halfway = necessaryMinutes / 2;
        //printf("Rotate after %d of the %d minutes.\n", halfway, necessaryMinutes); 
    }
        printf("Rotate after %d of the %d minutes.\n", halfway, necessaryMinutes); 
}
```

-   for the 2nd prinf, it could not access halfway, so the program will not run 

## Recursion

-   A function that call itself called recursion

```c
#include <stdio.h>

void singSongFor(int numberOfBottles) {
	if (numberOfBottles == 0) {
		printf("There are simply no more bottles of beer on the wall.\n\n");
	} else {
		printf("%d bottles of beer on the wall. %d bottles of beer.\n", numberOfBottles, numberOfBottles);
		int oneFewer = numberOfBottles - 1;
		printf("Take one down, pass it around, %d bottles of beer on the wall.\n\n", oneFewer);
		singSongFor(oneFewer); // This function calls itself!
		
		printf("Put a bottle in the recycling, %d empty bottles in the bin.\n",numberOfBottles);
	}
}

int main(int argc, const char * argv[]) {
	singSongFor(4);
	return 0;
}

/**
4 bottles of beer on the wall. 4 bottles of beer.
Take one down, pass it around, 3 bottles of beer on the wall.
3 bottles of beer on the wall. 3 bottles of beer.
Take one down, pass it around, 2 bottles of beer on the wall.
2 bottles of beer on the wall. 2 bottles of beer.
Take one down, pass it around, 1 bottles of beer on the wall.
1 bottles of beer on the wall. 1 bottles of beer.
Take one down, pass it around, 0 bottles of beer on the wall.
There are simply no more bottles of beer on the wall.

Put a bottle in the recycling, 1 empty bottles in the bin. 
Put a bottle in the recycling, 2 empty bottles in the bin. 
Put a bottle in the recycling, 3 empty bottles in the bin. 
Put a bottle in the recycling, 4 empty bottles in the bin.

**/

```

-   **main()**called**singSongFor(4)**.
-   **singSongFor(4)** printed a verse and called **singSongFor(3)**.
-   **singSongFor(3)** printed a verse and called **singSongFor(2)**.
-   **singSongFor(2)** printed a verse and called **singSongFor(1)**.
-   **singSongFor(1)** printed a verse and called **singSongFor(0)**.
-   **singSongFor(0)** printed “There are simply no more bottles of beer on the wall.” And returned.
-   **singSongFor(1)** resumed execution, printed the recycling message, and returned.
-   **singSongFor(2)** resumed execution, printed the recycling message, and returned.
-   **singSongFor(3)** resumed execution, printed the recycling message, and returned.
-   **singSongFor(4)** resumed execution, printed the recycling message, and returned.
-   **main()** resumed, returned, and the program ended.

## Looking at frames in the debugger

-   you can use the deubbger to browse the frames on the stack
-   we can set breakpoint
    -   a breakpoint is a location in code where you want the debugger to pause the execution of your program
    -   The program is temporarily frozen, and you can examine it more closely
-   In the stack trace, frames are identified by the name of their function

## return

-   You know what type of data a function will return by the type that precedes the function name

-   ```c
    #include <stdio.h>
    float fahrenheitFromCelsius(float cel)
    {
    	float fahr = cel * 1.8 + 32.0;
    	printf("%f Celsius is %f Fahrenheit\n", cel, fahr); return fahr;
    }
    int main(int argc, const char * argv[])
    {
    	float freezeInC = 0;
    	float freezeInF = fahrenheitFromCelsius(freezeInC); printf("Water freezes at %f 	degrees Fahrenheit.\n", freezeInF); 
        return 0 // NO ERROR 
    }
    ```

    

## Global and static variables

- **Global variables** is that the variables can be accessed from any function at any time
- we delcared global varaibles outside of a paricular function
- Static variable is that the variables is only accessible from the code in thhe file where it was delcared

