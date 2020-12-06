# Chapter25 Constants

```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
NSLog(@"\u03c0 is %f", M_PI);
}
return 0; 
}
// When you build and run it, you should see:
// π is 3.141593
```



## Prepocessor directives

-   Compiling a file of C, C++, or Objective-C code is done in two passes
    1.  the preprocessor runs through the file
    2.  The output from the preprocessor then goes into the real compiler
-   Preprocessor directives start with #, and the three most popular are `#include`,` #import`, and `#define`.



### #include and #import

- `#include` and `#import` both request that the preprocessor read a file and add it to its output.

- Usually, you are including a file of declarations (a .h file), and those declarations are used by the compiler to understand the code it is compiling.

    - `#import` ensures that the preprocessor only includes a file once.
    - ` #include` will allow you to include the same file many times.
    - mail.m has `\#import <Foundation/Foundation.h>`
    - `Foundation.h` has  `\#include <CoreFoundation/CoreFoundation.h>`
    - `CoreFoundation.h` has  `#include <math.h>`

    

### #define

-   “Whenever you encounter A, replace it with B before the compiler sees it.” Look at the line from math.h again:
-   `#define M_PI 3.14159265358979323846264338327950288` (TOEKN-SPACE-VALUE)

```objective-c
NSLog(@"%d is larger", MAX(10, 12));
#define MAX(A,B) ((A) > (B) ? (A) : (B))
NSLog(@"%d is larger", ((10) > (12) ? (10) : (12)));
```

-   When you use #define to do function-like stuff instead of simply substituting a value, you are creating a *macro*.



## Global Variable

Instead of using #define, Objective-C programmers commonly use global variables to hold constant values.

```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        
	NSLog(@"\u03c0 is %f", M_PI); NSLog(@"%d is larger", MAX(10, 12));
	NSLocale *here = [NSLocale currentLocale];
	// NSString *currency = [here objectForKey:@"currency"]; 
    NSString *currency = [here objectForKey:NSLocaleCurrencyCode];
        NSLog(@"Money is %@", currency);
}
return 0; }

extern NSString * const NSLocaleCurrencyCode; //NSLocale.h
NSString * const NSLocaleCurrencyCode = @"currency"; //NSLocale.n
```



## Enum

-   to define a set of constants

```objective-c
enum BlenderSpeed { 
    BlenderSpeedStir = 1, 
    BlenderSpeedChop = 2, 
    BlenderSpeedLiquify = 5, 
    BlenderSpeedPulse = 9, 
    BlenderSpeedIceCrush = 15
}BlenderSpeed;

@interface Blender : NSObject
{
    // speed must be one of the five speeds
    enum BlenderSpeed speed;
}
// setSpeed: expects one of the five speeds 
- (void)setSpeed:(enum BlenderSpeed)x;
@end
```



```objective-c
typedef enum { BlenderSpeedStir, 
              BlenderSpeedChop, 
              BlenderSpeedLiquify, 
              BlenderSpeedPulse, 
              BlenderSpeedIceCrush
} BlenderSpeed;

// iOS 6+
typedef NS_ENUM(int, BlenderSpeed) { 
    BlenderSpeedStir, 
    BlenderSpeedChop, 
    BlenderSpeedLiquify, 
    BlenderSpeedPulse, 
    BlenderSpeedIceCrush
};
```

