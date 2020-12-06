# Chapter 27- Call backs

When your code has finished executing, the program ends.

In this chapter, you are going to create a program that does not just start, execute, and end. 

Instead, this program is *event-driven*. It will start and wait for an event.  

When that event happens, the program will execute code in response. 

A *callback* lets you write a piece of code and then associate that code with a particular event. When the event happens, your code is executed.



1.  Target-action

    -   send the message to this object when this event happens
    -   The object receiving the message is the *target*. 
    -   The selector for the message is the *action*.
2.  Helper objects

    - When one of the events related to this role occurs, send a message to the helper object.” 
    - Helper objects are often known as *delegates* or *data sources*.
3.  Notifications
    -   When an event happens, a notification associated with that event will be posted to the notification center
    -   This object is interested in this kind of notification. When one is posted, send this message to the object
4.  Blocks
	-  A block is a just a chunk of code to be executed.



## RunLoops

In an event-driven program, there needs to be an object that does the sitting and waiting for events. In OS X and iOS, this object is an instance of **NSRunLoop**.

`        [[NSRunLoop currentRunLoop] run];`

The console does not report the familiar Program ended with exit code: 0. The run loop is waiting for something to happen.



## Coding

```objective-c
//  BNRLogger.h
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@interface BNRLogger : NSObject <NSURLConnectionDelegate, NSURLConnectionDataDelegate> {
	NSMutableData *_incomingData;
}

@property (nonatomic) NSDate *lastTime;
- (NSString *)lastTimeString;
- (void)updateLastTime:(NSTimer *)t;
@end

NS_ASSUME_NONNULL_END
```

```objective-c
//
//  BNRLogger.m
#import "BNRLogger.h"

@interface BNRLogger () //EXTENSION
- (void)zoneChange:(NSNotification *)note;
@end

@implementation BNRLogger

- (void)zoneChange:(NSNotification *)note {
	NSLog(@"The system time zone has changed!");
}

- (NSString *)lastTimeString {
	static NSDateFormatter *dateFormatter = nil;
	
	if (!dateFormatter) {
	dateFormatter = [[NSDateFormatter alloc] init];
		[dateFormatter setTimeStyle:NSDateFormatterMediumStyle];
		[dateFormatter setDateStyle:NSDateFormatterMediumStyle];
		NSLog(@"created dateFormatter");
	}
	return [dateFormatter stringFromDate:self.lastTime];
}

- (void)updateLastTime:(NSTimer *)t{
	NSDate *now = [NSDate date];
	[self setLastTime:now];
	NSLog(@"Just set time to %@", self.lastTimeString);
}

// Called each time a chunk of data arrives
- (void)connection:(NSURLConnection *)connection didReceiveData:(NSData *)data {
	NSLog(@"received %lu bytes", [data length]);
	// Create a mutable data if it does not already exist
	if (!_incomingData) {
		_incomingData = [[NSMutableData alloc] init];
	}
	
	[_incomingData appendData:data];
}

// Called when the last chunk has been processed
- (void)connection:(NSURLConnection *)connection didReceiveResponse:(NSURLResponse *)response {
	NSLog(@"Got it all!");
	NSString *string = [[NSString alloc] initWithData:_incomingData encoding:NSUTF8StringEncoding];
	_incomingData = nil;
	NSLog(@"string has %lu characters", [string length]);
	// Uncomment the next line to see the entire fetched file
	NSLog(@"The whole string is %@", string);
	
}

// Called if the fetch fails
- (void)connection:(NSURLConnection *)connection didFailWithError:(NSError *)error {
	NSLog(@"connection failed: %@", [error localizedDescription]);
	_incomingData = nil;
}

@end

```

```objective-c
//
//  main.m
//

#import <Foundation/Foundation.h>
#import "BNRLogger.h"
int main(int argc, const char * argv[]) {
	@autoreleasepool {
	    // insert code here...
		BNRLogger *logger = [[BNRLogger alloc] init];
		
		[[NSNotificationCenter defaultCenter] addObserver:logger
												 selector:@selector(zoneChange:) name:NSSystemTimeZoneDidChangeNotification object:nil];
		
		NSURL *url = [NSURL URLWithString:@"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
		NSURLRequest *request = [NSURLRequest requestWithURL:url];
		
		__unused NSURLConnection *fetchConn = [[NSURLConnection alloc] initWithRequest:request delegate:logger startImmediately:YES];
		
		__unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
														  target:logger
														selector:@selector(updateLastTime:)
														userInfo:nil
														 repeats:YES];
		[[NSRunLoop currentRunLoop] run];
		// . Notice that the run method never returns. The console does not report the familiar Program ended with exit code: 0. The run loop is waiting for something to happen.
	}
	return 0;
}

```

## Which to use

-   Objects that **do one thing** use target-action

-   Objects that have more complicated lives (like an **NSURLConnection**) use helper objects, and the

    most common type of helper object is the delegate.

-   Objects that might need to trigger callbacks in several other objects (like **NSTimeZone**) use notifications.

    

## Callbacks and object ownership

-   Inherent in any of these callback schemes is the risk of strong reference cycles. 
-   Often the object you create has a pointer to the object that is going to call back
-   And it has a pointer to the object you created.

solutions

```objective-c
// If an object is an observer, it will typically
remove itself from the notification center in its dealloc method:
- (void)dealloc {
      [[NSNotificationCenter defaultCenter] removeObserver:self];
  }

// . If you create an object that is a delegate or data source, your object should “excuse” itself in its dealloc method:
- (void)dealloc {
        [windowThatBossesMeAround setDelegate:nil];
        [tableViewThatBegsForData setDataSource:nil];
   }

// If you create an object that is a target, your object should zero the target pointer in its dealloc method:
- (void)dealloc {
        [buttonThatKeepsSendingMeMessages setTarget:nil];
}
```

