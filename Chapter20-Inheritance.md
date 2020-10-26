# Chapter 20 - Inheritance

```objective-c
@interface BNRPerson: NSObject
// BNRPerson to be the subclass of NSObject
@end
  
@interface BNREmployee: BNRPerson
// BNRPerson to be the subclass of NSObject
@end
```

```objective-c
 // BNREmployee.h
#import "BNRPerson.h"
@interface BNREmployee : BNRPerson
@property (nonatomic) unsigned int employeeID; 
@property (nonatomic) unsigned int officeAlarmCode; 
@property (nonatomic) NSDate *hireDate;
- (double)yearsOfEmployment;
@end
```

```objective-c
// BNREmployee.m
@implementation BNREmployee
- (double)yearsOfEmployment
{
  // Do I have a non-nil hireDate? 
  if (self.hireDate) {
  // NSTimeInterval is the same as double
  NSDate *now = [NSDate date];
  NSTimeInterval secs = [now timeIntervalSinceDate:self.hireDate]; 
    return secs / 31557600.0; // Seconds per year
} else {
  return 0; 
	}
}
@end
```

```objective-c
#import <Foundation/Foundation.h>
#import "BNREmployee.h"
int main(int argc, const char * argv[])
{
 		@autoreleasepool {
        // Create an instance of BNREmployee
        BNRPerson *mikey = [[BNREmployee alloc] init];
        // Give properties interesting values using setter methods 
        mikey.weightInKilos = 96;
        mikey.heightInMeters = 1.8;
        // Log some properties using getter methods
        NSLog(@"mikey has a weight of %d", mikey.weightInKilos); 
        NSLog(@"mikey has a height of %f", mikey.heightInMeters);
        // Log the body mass index
        float bmi = [mikey bodyMassIndex]; 
        NSLog(@"mikey has a BMI of %f", bmi);
		}
return 0; 
}
```

- Even though we do not import BNRPerson, the code still works
  - The compiler will find the #import "BNRPerson.h" statement in the BNREmployee.h



## Overriding methods

when subclass needs to do something differently than its superclass.

```objective-c
// BNREmployee.m
#import "BNREmployee.h"
@implementation BNREmployee
// (double)yearsOfEmployment {
//  ....
// }
 
- (float)bodyMassIndex 
  // we override bodyMassIndex method which was defined in BNRPerson
{
  return 19.0;
}
@end
```

## super 

```objective-c
- (float)bodyMassIndex {
  float normalBMI = [super bodyMassIndex];
	return normalBMI * 0.9;
}
```

## Inheritance hierarchy

- **NSObject** has many methods but only one instance variable:  the `isa` pointer
- Every object’s `isa` pointer points at the class that created it.
  - When you have a **BNRPerson** instance, that object “is a” **BNRPerson**.
  - When you have an **NSString** instance, that object “is a[n]” **NSString**.)

