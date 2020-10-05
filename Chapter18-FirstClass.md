# Chapter 18 - Your First Class

## First Class

Write a **BNRPerson** class, which will be similar to the struct `Person` you wrote in Chapter 11. This class, like all Objective-C classes, will be defined in two files:

-   **BNRPerson.h** is the class’s *header* and will contain the **declarations** of instance variables and methods.
-   **BNRPerson.m** is the *implementation file*. This is where you write out the code for, or *implement*, each method.



A header file starts with `@interface` and finishes off with` @end`. Notice that you declared the instance variables first and inside of curly braces.



By convention, instance variable names start with an underscore (“_”). Using the underscore prefix lets you easily tell instance variables from local variables when reading code



`Control` - `Command` - `up` arrow to switc .h and .m file

```objective-c
//  BNRPerson.h
//  BNRProject

#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@interface BNRPerson : NSObject
{
	//BNRPerson has two instance variable
	float _heightInMeters;
	int _weightInKilos;
}

// BNRPerson has methods to read and set its instance variables
- 	(float)heightInMeters;
- 	(void)setHeightInMeters:(float)h;
- 	(int)weightInKilos;
- 	(void)setWeightInKilos:(int)w;

// BNRPerson has a method that calculates the Body Mass Index
- 	(float)bodyMassIndex;

@end

NS_ASSUME_NONNULL_END

```

```objective-c
//  BNRPerson.m
//  BNRProject

#import "BNRPerson.h"

@implementation BNRPerson

- (float)heightInMeters
{
	return _heightInMeters;
}

- (void)setHeightInMeters:(float)h
{
	_heightInMeters = h;
}

- (int)weightInKilos
{
	return _weightInKilos;
}

- (void)setWeightInKilos:(int)w
{
	_weightInKilos = w;
}

- (float)bodyMassIndex
{
	return _weightInKilos / (_heightInMeters * _heightInMeters);
}

@end
```



```objective-c
int main(int argc, const char * argv[]) {
    
	@autoreleasepool {
	    
		// Create an instance of BNRPerson
		BNRPerson *mikey = [[BNRPerson alloc] init];
		
		// Give the instance variables interesting values using setters
		[mikey setWeightInKilos:96];
		[mikey setHeightInMeters:1.8];
		
		// Log the instance variables using the getters
		float height = [mikey heightInMeters];
		int weight = [mikey weightInKilos];
		NSLog(@"mikey is %.2f meters tall and weighs %d kilograms", height, weight);
		
		// Log some values using custom methods
		float bmi = [mikey bodyMassIndex];
		NSLog(@"mikey has a BMI of %f", bmi);
		
	}
	
	return 0;
}

```



## Access methods

```objective-c
// we access the data members of the structure directly using .(dot) opreate
mikey.weightInKilos = 96; 
mikey.heightInMeters = 1.8;

```

-   In object-oriented thinking, however, code that is outside of a class should not directly read or write to the instance variables of an instance of that class. Only code within the class can do that.

-   a class will provide methods that let external code (like in **main()**) access the instance variables of an instance. This is what you have done in **BNRPerson**

```objective-c
int weight = [mikey weightInKilos]; 
float height = [mikey heightInMeters];
```

-   The **heightInMeters** and **weightInKilos** methods are *getter methods*. A getter method, or *getter*, allows code outside of a class to read, or get, the value of an instance variable.
-   **BNRPerson** also has the methods **setHeightInMeters:** and **setWeightInKilos:**. These are *setter methods*. A setter method, or *setter*, allows code outside of a class to change, or set, the value of an instance variable.



## Accessor naming conventions

-   Getter methods are given the name of the instance variable minus the underscore.

```objective-c
// Instance variable declarations
{
   float _heightInMeters;
   int _weightInKilos;
}

// Getter method declarations 
- (float)heightInMeters;
- (int)weightInKilos;

```



-   Setter methods start with **set** followed by the name of the instance variable minus the underscore. 
-   Notice that the case of the setter’s name adjusts to preserve the camel-casing. Thus, the first letter of the instance variable name is uppercase in the setter’s name.

```objective-c
// Setter method declarations - notice difference in casing! 
- (void)setHeightInMeters:(float)h;
- (void)setWeightInKilos:(int)w;

```



## self

-   self is a pointer to the object that is running the method 
-   it is used shen an object wants to send a message to itself

```objective-c
- (float)bodyMassIndex
{
    //return _weightInKilos / (_heightInMeters * _heightInMeters);
    
    float h = [self heightInMeters];
    return [self weightInKilos] / (h * h);
}

// self could also be as an argument to let other objects know where the current object is
- (void)addYourselfToArray:(NSMutableArray *)theArray
{
    [theArray addObject:self];
}

```

Here you use `self` to tell the array where the instance of **BNRPerson** lives. It is literally the **BNRPerson**

instance’s address.



## Multiple Files

-   When Xcode builds your project, it compiles each of the .m and .c files into machine code.
-   Then, it links those files together with any libraries into the executable file. 
-   In this section of the book, all of your executables have been link to the Foundation framework.



## Class Prefixes

-   Objective-C is not namespaced. 
    -    if you write a program with a class called **Person** in it, and you link in a library of someone else’s code that also declares a **Person** class, the compile cannot tell the difference and get a compiler error
-   Apple recommends that you prefix each of your class names with three or more letters, to make your class names more unique and less likely to collide with someone else’s class name
    -   We use **BNR** prefix



