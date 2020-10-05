# Chapter17 - NSArray

**NSArray** is another commonly used Objective-C class. An instance of **NSArray** holds a list of pointers to other objects



## Creating NSArray

```objective-c
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // Create three NSDate objects
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0]; 
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        
        // Create an array containing all three
        // Notice that the instance of NSArray has pointers to the NSDate objects.
        NSArray *dateList = @[now, tomorrow, yesterday];
	}
		return 0; 
}
```

-   **NSArray** has a literal syntax for creating instances.
-   The array’s contents are in a comma-delimited list, surrounded by square brackets, and preceded with @. 
-   No explicit message send is necessary
-   An instance of **NSArray** is *immutable*. No further change.



## Accesing Arrays

```objective-c
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
    @autoreleasepool {
		// Create three NSDate objects
		NSDate *now = [NSDate date];
		NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0]; 
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        
		// Create an array containing all three
		NSArray *dateList = @[now, tomorrow, yesterday];
        
		// Print a couple of dates
		NSLog(@"The first date is %@", dateList[0]); 
        NSLog(@"The third date is %@", dateList[2]);
        NSLog(@"The fourth date is %@", dateList[3]); // Crash! Out-of-range errors
        
		// How many dates are in the array? 
        NSLog(@"There are %lu dates", [dateList count]);
}
		return 0; 
}
```

## Iterating over Array

```objective-c
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
    @autoreleasepool {
		// Create three NSDate objects
		NSDate *now = [NSDate date];
		NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0]; 
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        
		//Iterate over the array
        NSUInteger dataCount = [dateList count];
        for (int i = 0; i < dateCount; i++) {
            NSDate *d = dataList[i];
            NSLog(@"Here is a date: %@", d);
        }
        
        //Iterate over the array
        NSUInteger dataCount = [dateList count];
        for (NSDate *d in dateList) {
            NSLog(@"Here is a date: %@", d);
        }
	}
		return 0; 
}
```

## NSMutableArray 

-   same as NSArray but Mutable

```objective-c
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
    @autoreleasepool {
		// Create three NSDate objects
		NSDate *now = [NSDate date];
		NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0]; 
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        
		// Create an empty mutable array
		NSMutableArray *dateList = [NSMutableArray array]; // can also use alloc and init
		
        // Add two dates to the array
        [dateList addObject:now];
        [dateList addObject:tomorrow];
        
        // Add yesterday at the beginning of the list
        [dateList insertObject:yesterday atIndex:0];
        
        // Iterate over the array
        for (NSDate *d in dateList) {
			NSLog(@"Here is a date: %@", d); 
        }
        
        // Remove yesterday
        [dateList removeObjectAtIndex:0];
        NSLog(@"Now the first date is %@", dateList[0]);
	}
		return 0; 
}
```

## Old-style array method

-   The **arrayWithObjects:** and **objectAtIndex:** method

```objective-c
// Create an array containing three pointers (nil terminates the list)
NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

// Before subscripting was introduced, 
// developers used the objectAtIndex: method to access an item in an array:
NSLog(@"The first date is %@", [dateList objectAtIndex:0]); 
NSLog(@"The third date is %@", [dateList objectAtIndex:2]);

id selectedDog = dogs[[tableView selectedRow]];
id selectedDog = [dogs objectAtIndex:[tableView selectedRow]];
```

