# Chapter 24 Collection Classes



## NSSet & NSMutableSet

-   A set is a collection that has no sense of order, and a particualr object can only appear in a set once

-   Sets are primarily useful for asking the question “Is it in there?

-   cannot access an object in an set by index 

```objective-c
- (BOOL)containsObject:(id)x;
```

-    it goes through its collection of objects looking for an object equal to x. 
-   If it finds one, it returns `YES`; otherwise it returns `NO`.

-   To check with equal, we use `isEqual`

```objective-c
if ([myDoctor isEqual:yourTennisPartner]) {
	NSLog(@"my doctor is equal to your tennis partner"); 
}


- (BOOL)isEqual:(id)other {
	return (self == other); 
}

if (myDoctor == yourTennisPartner) {
	NSLog(@"my doctor is equal to your tennis partner"); 
}

```

Some classes override **isEqual:**. For example, in **NSString**, **isEqual:** is overridden to compare the characters in the string. 



## Equal vs. identical

-   identical objects are always equals. 
-   Equal objects are not always identical

-   For `NSmutableArray` has two method
    -   `(NSUInteger)indexOfObject:(id)anObject;`
    -   `(NSUInteger)indexOfObjectIdenticalTo:(id)anObject;`



## NSDictionary/ NSMutableDictionary 

-   A dictionary is a collection of key-value paris
-   The key is typically a string, the value can be any sort of objects

-   Dictionaries are indexed by key: you provide a key and get back the value (an object) associated with that particular key. 



```objective-c
NSDictionary *numberOfMoons = @{ @"Mercury": @0,
                                @"Venus": @0,
                                @"Earth": @1,
                                @"Mars": @2,
                                @"Jupiter": @67,
                                @"Saturn": @62,
                                @"Uranus": @27,
                                @"Neptune": @13, };

```

-   The keys are **NSString** objects, and the values are **NSNumber** objects. Both are created on the spot using literal syntax.

`NSNumber *marsMoonCount = numberOfMoons[@"Mars"];//get 2 `

```objective-c
NSDictionary *innerPlanetMoons = @ {
    @"Mercury": @[],
    @"Venus": @[],
    @"Earth": @[@"Luna"],
    @"Mars": @[@"Deimos", @"Phobos"]
};

NSArray *array = innerPlanetMoons[@"Earth"];
```



## Immutable objects

- You do not trust the people you work with. 
- A gentler approach is to give them an **NSMutableArray** but tell them it is an **NSArray**.

```objective-c
// Returns an array of 30 odd numbers - (NSArray *)odds
- (NSArray *)odds 
{
NSMutableArray *oddsArray = [[NSMutableArray alloc] init]; 
    int i = 1;
    while ([oddsArray count] < 30) {
        [oddsArray addObject:[NSNumber numberWithInt:i];
         i += 2; 
         }
    return oddsArray;
}
         
Anyone calling this method assumes from its declaration

- (NSArray *)odds;
```



## Sorting

```objective-c
- (void)sortUsingDescriptors:(NSArray *)sortDescriptors;

NSSortDescriptor *lastAsc = [NSSortDescriptor sortDescriptorWithKey:@"lastName" ascending:YES];
```

```objective-c
NSSortDescriptor *voa = [NSSortDescriptor sortDescriptorWithKey:@"valueOfAssets" ascending:YES];
NSSortDescriptor *eid = [NSSortDescriptor sortDescriptorWithKey:@"employeeID" ascending: YES];
// Sort employees array by valueOfAssets at 1st , sort by employeeID second
[employees sortUsingDescriptors: @[voa, eid]];

```



## Filtering

-   When you filter a collection, you compare its objects to a logical statement to get a resultant collection that only contains objects for which the statement is true.

-   A *predicate* contains a statement that might be true, like “The employeeID is greater than 75.” There is a class called **NSPredicate**. **NSMutableArray** has a handy method for discarding all the objects that do not satisfy the predicate:

```objective-c
- (void)filterUsingPredicate:(NSPredicate *)predicate;
```

```objective-c
- (NSArray *)filteredArrayUsingPredicate:(NSPredicate *)predicate;
```

```objective-c
NSPredicate *predicate = [NSPredicate predicateWithFormat: @"holder.valueOfAssets > 70"];
NSArray *toBeReclaimed = [allAssets filteredArrayUsingPredicate:predicate]; 
NSLog(@"toBeReclaimed: %@", toBeReclaimed);
toBeReclaimed = nil;
```

```objective-c
// More on NSSet

- (NSSet *)filteredSetUsingPredicate:(NSPredicate *)predicate;
- (void)filterUsingPredicate:(NSPredicate *)predicate;
```


## Collections and ownership

-   When you add an object to a collection, the collection cliams ownership of it.
-   When you remove the object from the collecton, the collection gives up ownership.
-   This is true for **NSMutableArray**, **NSMutableSet**, and **NSMutableDictionary**



## C primitive types

```objective-c
NSMutableArray *list = [[NSMutableArray alloc] init]; 
[list addObject:@4];
[list addObject:@5.6];
```

```objective-c
NSPoint somePoint = NSMakePoint(100, 100);
NSValue *pointValue = [NSValue valueWithPoint:somePoint]; 
[list addObject:pointValue];
```



## Collections and nil

-   you are not allowed to add `nil` to any of the collection classes
-   we have `NSNull`

```objective-c
NSMutableArray *hotel = [[NSMutableArray alloc] init];
// Lobby on the ground floor
[hotel addObject:lobby];
// Pool on the second
[hotel addObject:pool];
// The third floor has not been built out
[hotel addObject:[NSNull null]];
// Bedrooms on fourth floor
[hotel addObject:bedrooms];
```

