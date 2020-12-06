# Chapter 28 Blocks 



```objc
^{NSLog(@"This is an instruction within a block.");}
```

The caret (^) identifies this bit of code as a block.



a block can take arguments and return values. 

```objc
^(double divided, double divisor) {
    double quotient = dividend / divisor;
    return quotient;
}
```

This block takes two doubles as arguments and returns a double.



You can pass a block as an argument to a method that accepts a block. Many of Apple’s classes have

methods that accept blocks as arguments.

-   For instance, **NSArray**, **NSDictionary**, and **NSSet** allow block-based enumeration:

-    blocks as anonymous functions, closures, or lambdas. 



## Use block

```objective-c
// Declare the block variable
void (^devowelizer)(id, NSUInteger, BOOL *);

// Compose a block and assign it to the variable 
devowelizer = ^(id string, NSUInteger i, BOOL *stop) {
    NSMutableString *newString = [NSMutableString stringWithString:string];
    // Iterate over the array of vowels, replacing occurrences of each with an empty string
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
         withString:@""
         options:NSCaseInsensitiveSearch
         range:fullRange];
    }
    [devowelizedStrings addObject:newString];
};
```



```objective-c
void (^devowelizer)(id, NSUInteger, BOOL *) = ^(id string, NSUInteger i, BOOL *stop) {
        NSRange yRange = [string rangeOfString:@"y" options:NSCaseInsensitiveSearch];

        // Did I find a y?
        if (yRange.location != NSNotFound) {
            *stop = YES; // Prevent further iterations
            return;      // End this iteration
        }


        NSMutableString *newString = [NSMutableString stringWithString:string];
        // Iterate over the array of vowels, replacing occurrences of each with an empty string
        for (NSString *s in vowels) {
            NSRange fullRange = NSMakeRange(0, [newString length]);
            [newString replaceOccurrencesOfString:s
             withString:@""
             options:NSCaseInsensitiveSearch
             range:fullRange];
        }
        [devowelizedStrings addObject:newString];
		};
```



## PASSING A BLOCK

```objc
// Iterate over the array with your block 
[originalStrings enumerateObjectsUsingBlock:devowelizer]; 
NSLog(@"devowelized strings: %@", devowelizedStrings);

```



## typedef

```objc
typedef void (^ArrayEnumerationBlock)(id, NSUInteger, BOOL *);
ArrayEnumerationBlock devowelizer =  ^(id string, NSUInteger i, BOOL *stop) {...}
```



## Return value 

```objc
// Declare divBlock variable 
double (^divBlock)(double,double);

// Assign block to variable
divBlock = ^(double dividend, double divisor) {
double quotient = dividend / divisor;
    return quotient;
}

double myQuotient = divBlock(42.0, 12.5);
```



## Anonynmous blocks

```objective-c
// Option 1: Totally break it down
int i;
i = 5;
NSNumber *num = [NSNumber numberWithInt:i];
// Option 2: Declare and assign on one line int i = 5;
NSNumber *num = [NSNumber numberWithInt:i];
// Option 3: Skip the variable entirely 
NSNumber *num = [NSNumber numberWithInt:5];
```



## External Variable

```objective-c
// NOT GOOD!!!!!! this create a strong reference cycle.
myBlock = ^{
	NSLog(@"Employee: %@", self); 
};
```

```objc
//BETTER ,BUT
// However, because the reference is weak, the object that self points to could be deallocated while the block is executing.
__weak BNREmployee *weakSelf = self; // a weak reference
myBlock = ^{
	NSLog(@"Employee: %@", weakSelf);
};
```

```objc
//BEST
// because the innerSelf reference is local to the scope of the block, the strong reference cycle will only exist while the block is executing and will be broken automatically when the block ends.

_weak BNREmployee *weakSelf = self; // a weak reference 
myBlock = ^{
	BNREmployee *innerSelf = weakSelf; // a block-local strong reference
	NSLog(@"Employee: %@", innerSelf); 
};

```

## **Modifying external variables**

```objective-c
__block int counter = 0;
void (^counterBlock)() = ^{ counter++; }; ...
counterBlock(); // Increments counter to 1 
counterBlock(); // Increments counter to 2
```



