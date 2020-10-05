# Chapter 15 Objects and Memory

## On pointers and their values

-   Objects can only be accessed via a pointer, and it is practical
-   The pointer and the object that it points at are not the same thing

-   `now` is a pointer that can hold an address of a location in memory where an instance of **NSDate** lives.



```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
    NSDate *currentTime = nil;
    NSLog(@"currentTime's value is %p", currentTime);
        // currentTime points at 0x0
	}
	return 0; 
}
```

```objective-c
NSDate *currentTime = [NSDate date]; 
NSLog(@"currentTime's value is %p", currentTime);
// The currentTIme now points to an NSDate object existed on the heap


sleep(2);

currentTime = [NSDate date];
NSLog(@"currentTime's value is now %p", currentTime);
// The currentTIme now points to ANOTHER NSDate object existed on the heap
// The original NSDate object is still here.

```

-    If we lose only pointer to an object, then we can no longer access it – even if it continues to exist on the heap.



## Memory Management

-   Memory management is about managing Heap Memory
-   Heap meomory is a heaping pile of memory where the objects live

-   Managing the heap is important because objects can be large and because your program only gets so much heap memory for its own use
-   Running low on memory can cause Mac app to perform badly and will cause an iOS app crash



## ARC (Automatic Reference Counting)

-   The setting that instructs the compiler to ensure the destruction of unreferenced objects is called ARC. 
-   Each object keeps a count of how many references to itself there are
-   When your project has ARC enabled, the compiler adds code to your project to tell each object when it gains or loses a reference
-   When you change `currentTime` to point at a new object, the original object loses a reference, and ARC decrements its reference count. 
-   The new date object’s reference count is incremented



