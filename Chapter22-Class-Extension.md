# Chapter 22 Class Extension

We just declared properties, instance variables, and methods in the class header file. 

The header is where a class advertises its properties and methods so that other objects will know how to interact with it.



`officeAlarmCode` should be private 

-    The employee object needs to be able to access its alarm code,
-    while non-employee objects do not need access to the alarm code and should not have it
-   we could use class extension.

Typically, class extensions are added to the class implementation file above the @implementation block where methods are implemented. 

In BNREmployee.m, create a class extension. Then declare the officeAlarmCode property there:

```objective-c
#import "BNREmployee.h"
// A class extension
@interface BNREmployee ()
@property (nonatomic) unsigned int officeAlarmCode;
@end
    
@implementation BNREmployee
...
```

A class extension starts with @interface and finishes off with @end. 

In fact, an extension looks a lot like a header, and both are known as “interfaces.” However, in an extension, instead of the colon and the superclass name found in the header, there is a pair of empty parentheses.





## Hiding mutability

-   In `BNREmployee.h`, you declared an assets property that is an **NSArray**, an **addAsset:** method, and an _assets instance variable that is an **NSMutableArray**
-   A developer will see both the property and the instance variable advertised in the header and will be uncertain which you intended outsiders to use.
-   solution: move `_assets` instance variable to BNREmployee's class extension.

```objective-c
BNREmployee.m
// A class extension
@interface BNREmployee ()
{
	NSMutableArray *_assets;
}

@property (nonatomic) unsigned int officeAlarmCode;

@end

@implementation BNREmployee
    //...
```

-   Now the array of assets is only adverised as an immutable array.
-   non-BNREmployee objects will need to use the `addAsset:` method to manipulate this array. 



## Headers and inheritance

-   A subclass has no access to its superclass's  class extension.
-   `BNREmployee` is a subclass of `BNRPerson`.
-    `BNREmployee` knows about what is declared in BNRPerson's header but knows nothing about anything that `BNRPerson` may have decalred in a class extension.
-   corresponding error : `“No visible @interface declares the instance method`



## Headers and generated instance variables

When a class declares a property in its header, only the *accessors* for this property are visible to other objects. 

Non-**BNREmployee** objects (including subclasses) cannot directly access the instance variables generated by property declarations.

e.g.

```objective-c
BNRPerson.h
@property (nonatomic) NSMutableArray *friends;
```

Even though BNREmployee is a subclass of BNRPerson, you cannot access the _friends instanfe variable:

```objective-c
[_friends addObject:@"Susan"]; // Error!
[self.friends addObject:@"Susan"]; // Correct
```

