# Objects

1980s, Brad Cox and Tom Love created the Objective-C language. 

For objects, they built upon the idea of structs allocated on the `heap` and added a `message-sending syntax`



## Objetcs

-   an object is similar to struct containing several pieces of related ata
-   In struct we called them member while in an object we call them instance variable
-   an object could have its own functions that act on the data it contains, which are called methods



## Classes

-   A *class* describes a certain type of object by listing the instance variables and methods that object will have.
-   A class defines a kind of object and also produces objects of that kind.
-   A class is a blueprint and factory



## Creating your first object

`#import <Foundation/Foundation.h>`

-   When Xcode created your project, it imported the Foundation framework for you.

-   A *framework* is a set of related classes, functions, constants, and types.

-   The Foundation framework contains fundamental classes that are used in all iOS apps and OS X applications.
    -   The **NSDate** class is in the Foundation framework.

-   Difference between **#import** and **#include**? 
    -   **#import** is faster and more efficient 
    -   the compiler sees the #include directive, it makes a dumb copy-and-paste of the contents of the file to include. 
    -    the compiler sees the #import directive, it first checks to see if another file may have already imported or included the file.

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
	@autoreleasepool {
	    // insert code here...
		NSDate *now = [NSDate date];
		NSLog(@"This NSDate object lives at %p", now);
	}
	return 0;
}
```

-   **NSLog()** prefaces its output with the date, time, program name, and process ID.



## Methods and Messages

-   Methods are like functions containing code to be executed on command. 
-   In Objective C, to execute the code in a method, you need to send a message to the object or calss that has that method



`NSDate` class has a `date` method. We need to send the `date` message to the `NSDate` class to execute the `date` method.

NSDate *now = [NSDate date];



## Message Sends

-   A message send is surrounded by square brackets and has two part:
    -   the receiver and selector

-   `NSDate *now = [NSDate date]`
    -   The receiver: 	a pointer to the object or class that has the method that you wan to execute
    -   The selector:       the name of the method that you want to execute

-   When the **date** method executed, the **NSDate** class claims some memory on the heap for an instnace of **NSDate**, initialzes the instance to the current date/time, and returns the address of the new object

```objective-c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
	@autoreleasepool {
	    // insert code here...
		NSDate *now = [NSDate date];
		NSLog(@"This NSDate object lives at %p", now);
        NSLog(@"The date is %@", now);
	}
	return 0;
}
```



## Another Message

-   We have an instnace of NSDate, you can send messages to this new object
-   you are going to send it the message `timeIntervalSince1970` 
    -   when send `timeIntervalSince1970` to the instance of `NSDate`,
    -   you get back the difference in seconds between the date/time that the NSDate instance presents and 
    -   12:00AM on Jan 1, 1970 in Greenwich, England
    -   (Why 1970? OS X and iOS are based on Unix, and 1970 is the start of the “Unix epoch.”)



```objective-c
double seconds = [now timeIntervalSince1970];
NSLog(@"It has been %f seconds since the start of 1970.", seconds);
```



## Class Methods vs Instance method

```objective-c
NSDate *now = [NSDate date];
double seconds = [now timeIntervalSince1970];

```

-   You sent the **date** message to the **NSDate** class. **date** is a *class method*. 
-   Typically, class methods create an instance of the class and initialize its instance variables.

-   In the second message send, you sent the **timeIntervalSince1970** message to the **NSDate** instance pointed to by now. 
-   **timeIntervalSince1970** is an *instance method*. 
-   Typically, instance methods give you information about or perform an operation on an instance’s instance variables.



## Sending a Bad message

```objective-c
// Sending bogus messages to see errors...
double testSeconds = [NSDate timeIntervalSince1970]; 
NSDate *testNow = [now date];

```

-   The receiver in this message send is the **NSDate** class, so the selector should be the name of an **NSDate** class method. This selector is not.



```objective-c
// Sending bogus messages to see errors...
double testSeconds = [NSDate timeIntervalSince1970]; 
NSDate *testNow = [now date];

// Mistyped selector name
testSeconds = [now fooIntervalSince1970];

// Typo! Lowecase i and s
testSeconds = [now timeintervalsince1970]
```



## Naming Convention

-   variable and methods name using Camel case:	date, bodyMassIndex
-   class names are capitialized: NSDate, Perosn, CLLocation, NSMutableArray
-   Many Apple-created types and constants are also capitalized. 
    -   For example, NSInteger is not a class, it is just a type of integer. 
    -   NSOKButton is a constant that is equal to 1.

## Chanllenge

```objective-c
int main(int argc, const char * argv[]) {
	@autoreleasepool {
	    // insert code here...
		NSHost *host = [NSHost currentHost];
		NSString *localizedName = [host localizedName];
		NSLog(@"%@", localizedName);
	}
	return 0;
}
```

