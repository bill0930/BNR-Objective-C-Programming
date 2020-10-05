# Chapter 14 - More Message

## Message with arguments

```objective-c
[receiver selector: argument]
[now dateByAddingTimeInterval: 10000]
```

-   `dateByAddingTimeInterval` accetpts the number of seconds by which the new NSDate should differ from the original one. 
-   A negative number would give you an NSDate in the past
-   In TimeAfterTime, use **dateByAddingTimeInterval:** to create a second date that is 100,000 seconds (a bit over a day) later than the date pointed to by now:

```objective-c
NSDate *later = [now dateByAddingTimeInterval:100000]; 
NSLog(@"In 100,000 seconds it will be %@", later);
```

-   When a method has an argument, the colon is an essential part of the method’s name. 
-   There is no method named **dateByAddingTimeInterval**. 
-   There is only **dateByAddingTimeInterval:**.



## Multiple Arguments

```objective-c
int main(int argc, const char * argv[]) {
	@autoreleasepool {
		NSDate *now = [NSDate date];
		NSLog(@"This NSDate object lives at %p", now);
		NSLog(@"The date is %@", now);
		
		unsigned long day = [cal ordinalityOfUnit:NSDayCalendarUnit
												inUnit:NSMonthCalendarUnit
												forDate:now];
		NSLog(@"This is day %lu of the month", day);
	}
	return 0;
}
```

`unsigned long day = [cal ordinalityOfUnit:NSDayCalendarUnit
							inUnit:NSMonthCalendarUnit
							forDate:now];`

-   Notice that you split the **ordinalityOfUnit:inUnit:forDate:** message send into three lines.

-   Objective-C programmers often line up the colons so that it is easy to tell the parts of the method name from the arguments



## Nesting Message sends

```objective-c
NSDate *now = [NSDate date];
double seconds = [now timeIntervalSince1970];
NSLog(@"It has been %f seconds since the start of 1970", seconds

// Nesting 
double seconds = [[NSDate date] timeIntervalSince1970];
NSLog(@"It has been %f seconds since the start of 1970", seconds);
```

-   **date** is sent to the **NSDate** class, and the result of that (a pointer to the newly-created instance) is sent **timeIntervalSince1970**.
-   counterproductive, makes code hrder to read and harder to debug 



## alloc and init 

-   ONLY the always right case to nest two messag eends, 
-   `alloc` method returns a point to a new instance that needs to be initialized
    -   exit in memory but no ready to receive messages
-   `Init`method initialises an instance so that it is ready to work



```objective-c
NSDate *now = [[NSDate alloc] init];
NSDate *now = [NSDate date];
```

-   There is no difference in the two ways of creating an instance of **NSDate**.
-   date method is a `convenicence method`



## sending messages to nil

-   we use `nil` when referring to the value of an empty pointer declared as pointing to an Objective-C object type, 
-   `NULL` when referring to any other pointer, such as to a struct

```objective-c
if (fido != nil) {
    [fido goGetTheNewspaper];   
}

Dog *fido = nil;
[fido goGetTheNewspaper];

// If you are sending messages and nothing is happening, make sure you are not sending messages to a pointer that has been set to nil.
// If you send a message to nil, the return value is meaningless and should be disregarded.

Dog *fido = nil;
Newspaper *daily = [fido goGetTheNewspaper];

```



## id

-   When declaring a pointer to hold the address of an object, most of the time you specify the class of the object that the pointer will refer to

```objective-c
NSDate *expiration;

//	create a pointer without knowing exactly what kind of object the pointer will refer to
//	a pointer to some kind of Objective-C object

id delegate; // asterisk

NSDateComponents *comps = [[NSDateComponents alloc] init]; 
[comps setYear:1969];
[comps setMonth:4];
[comps setDay:30];
[comps setHour:13];
[comps setMinute:10];
[comps setSecond:0];

NSCalendar *g = [[NSCalendar alloc] initWithCalendarIdentifier:NSGregorianCalendar]; 
NSDate *dateOfBirth = [g dateFromComponents:comps];

```



















