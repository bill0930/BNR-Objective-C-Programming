

# Object Instance Variables and Properties

-   Instance variable
    -   simply C type, like `int` `float`
    -   pointers to other objects, like `_hireDate`
-   An object instance variable points to another object
-   describes a relationship between the two objects
-   Usually fall into one of three categories:
    -   Object-type attributes (NSString, NSDate)
    -   To-one relationships (BNREmployee,BNRPerson)
    -   To-Many relationships  (NSArray, NSMutableArray )

```objective-c
@interface BNREmployee : BNRPerson
@property (nonatomic) unsigned int employeeID; // not a pointer
@property (nonatomic) unsigned int officeAlarmCode;	// not a pointer
@property (nonatomic) NSDate *hireDate;
@property (nonatomic) NSString *lastName;
@property (nonatomic) BNRPerson *spouse;
@property (nonatomic) NSMutableArray *children;
```



## Object ownership and ARC

-   The idea of `object ownership` is that when an object has an object instance variable, the object with the pointer is said to own the object that is being pointed to.

-   Because of ARC, an object knows how many `owners` it currently has. 
    -   e.g. An instance of BNRPerson has three owners (three pointers are pointing to this instance)
-   When an object has zero owners, if figures no one needs it around anymore and deallocates itself.



##  Adding a to-many relationship to BNREmployee


• When an object is added to the collection, the collection establishes a pointer to the object, and the object gains an owner.

• When an object is removed from a collection, the collection gets rid of its pointer to the object, and the object loses an owner.

```objective-c
#import "BNRPerson.h"
@class BNRAsset;

NS_ASSUME_NONNULL_BEGIN

@interface BNREmployee : BNRPerson
{
	NSMutableArray *_assets;
}

@property (nonatomic) unsigned int employeeID;
@property (nonatomic) unsigned int officeAlarmCode;
@property (nonatomic) NSDate *hireDate;
@property (nonatomic, copy) NSArray *assets;

- (double)yearsOfEmployment;
- (void)addAsset:(BNRAsset *)a;
- (unsigned int)valueOfAssets;

@end
```



-   using `@class` instead of `#import` gives the compiler less information, but makes the processing of this particular file faster. 

-   The property has type `NSArray`, behind the scenes, the assets array is actually an instnace of `NSMutableArray` (which you can add and rmeove items in BNREmployee.m)

-   With a to-many relationship, you need to create the collection object (an array, in this case) before you put anything in it.

