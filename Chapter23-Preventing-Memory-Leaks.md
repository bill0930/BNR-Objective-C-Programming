# Chapter 23 Preventing Memory Leaks

-   Employee owns assets 
-   assets owns employee
-   This may create strong reference cycles



## Strong referene cycles

-   The asset owns the employee,  and the employee owns the assets array

-   These objects should be getting deallocated to free up memory, but they are not.

-   Common source of memory leaks

We can use  Apple’s profiling tool, **Instruments**. When you *profile* a program, you monitor it while it runs to see what is happening behind the scenes with your code and the system

. To give you time to profile, put in a hundred seconds of **sleep()** at the end of your **main()** function:

```objective-c

...
}
sleep(100);
return 0; }
```



## Weak reference

-   the way to fix strong reference cycle is to use a weak reference.

-    A *weak reference* is a pointer that *does not* imply ownership



## zeroing of weak referneces

if we wanted an array of all assets, even ones that have not been assigned to a particular employee, we could add the assets to an array as they are created

```objective-c
NSMutableArray *allAssets = [[NSMutableArray alloc] init];
[allAssets addObject:asset];
NSLog(@"allAssets: %@", allAssets);
allAssets = nil;
```



## Summary

-   A strong reference will keep the object it points to from being deallocated. A weak reference will not. 
-   Thus instance variables and properties that are marked as weak are pointing at objects that might go away
-   If this happens, that instance variable or property will be set to nil, instead of continuing to point to where the object used to live.