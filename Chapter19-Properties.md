# Chapter 19 Properties

-   a convenient shortcut called *properties* that
    -    lets you <u>skip declaring instance variables</u> 
    -    and <u>declaring and implementing accessor methods</u>. 



## Declaring Properties

```objective-c
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@interface BNRPerson : NSObject

// BNRPerson has two properties
@property (nonatomic) float heightInMeters;
@property (nonatomic) int weightInKilos;

// BNRPerson has a method that calculates the Body Mass Index
- (float)bodyMassIndex;

@end

NS_ASSUME_NONNULL_END
```

```objective-c
#import "BNRPerson.h"

@implementation BNRPerson

- (float)bodyMassIndex
{
	return _weightInKilos / (_heightInMeters * _heightInMeters);
}

@end
```



-   A property declaration begins with **@property** and includes the type of the property and its name.
-   **nonatomic** is a property attribute

-   They are simply written using a terser (and more stylish) syntax.
-   The compiler created instance variables named **_heightInMeters** and **_weightInKilos**. However, you do not see these variables in your code
-   Apple recommends using properties, and so do we.



## Propety attributes

-   A property declaration can have one or more *property attributes*
-   Property attributes appear in a comma- delimited list in parentheses after the @property annotation
-   Properties are either `readonly` or `readwrite` , default value is `readonly`
-   `nonatomic` & `atomic` , about multithreading, default value is `atomic`
-   `copy` for `NSString` and `NSArray`

```objective-c
@property (nonatomic) float heightInMeters;
@property (nonatomic) int weightInKilos;

@property (nonatomic, readonly) double circumferenceOfEarth;
//	create a circumferenceOfEarth getter method but not a setCircumferenceOfEarth: setter method.

@property (nonatomic, readwrite) double humanPopulation;
```



## Dot notation

-   Apple introudcted a shorthand dot notation for calling those accessors
-   This notation looks just like the notation used for accessing the members of a struct.
-   RMB -> when using dot notation with an object, a message is being sent.
-   it calls either the getter method (**weightInKilos**) or the setter method (**setWeightInKilos:**) 

