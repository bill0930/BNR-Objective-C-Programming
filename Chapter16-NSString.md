# Chapter 16 NSString

## Creating instnaces of NSString

`NSString *lament = @"Why me?;"`

-   no explicit message sent to the **NSString** class to create the instance
-   @"..." is Objective-C shorthand for creating an NSString object with given character string
-   @"..." is literal syntax
-   we create a literal instance of NSString, / NSString literal 
-   can contains Unicode character
    -   `NSString *slogan = @"I \u2661 New York!";`

-   Dynamically create a strings with `stringWithformat:`
    -   `NSString *dateString = [NSString stringWithFormat:@"The date is %@", now];`



## NSString methods

```objective-c
NSString *dateString = [NSString stringWithFormat:@"The date is %@", now];

// - (NSUInteger)length; 
NSUInteger charCount = [dateString length];

//	- (BOOL)isEqualToString:(NSString *)other;
if ([slogan isEqualToString:lament]) {
	NSLog(@"%@ and %@ are equal", slogan, lament); 
}

//	- (NSString *)uppercaseString;
NSString *angryText = @"That makes me so mad!";
NSString *reallyAngryText = [angryText uppercaseString];
```

## Class Reference

-   Apple maintains a *class reference* for each class in its APIs.

-   Methods for finding characters and substrings

-   **rangeOfString:**

    -   Declaration      
		
	>  ` - (NSRange)rangeOfString:(NSString *)searchString;]`
	
	-   Parameters 	  
	
	   >    `searchString` The string to search for
	
	-   Return Value	
	
	   >   An `NSRange` structure giving the location and length in the receiver of the first occurrence of `searchString`. Returns `{``NSNotFound``, 0}` if `searchString` is not found or is empty (`""`).
	


## NSRange

-   NSRange is `typeof` for a `struct`, it has two members 

```objective-c
typedef struct _NSRange {
    NSUInteger location;
    NSUInteger length;
} NSRange;

#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
	@autoreleasepool {
		NSString *listOfNames = @"Ward"; // a long list of names
		NSString *name = @"Ward";
		NSRange match = [listOfNames rangeOfString:name];
		if (match.location == NSNotFound) {
			NSLog(@"No match found!");
		} else {
			NSLog(@"Match found!");
		}
	}
	return 0;
}

```

-   https://developer.apple.com/documentation/