# Chapter 30 Property Lists

-   Sometimes you need a file format that can be read by both computers and people.
-   A property list is a combination of any of the following things:
    -   NSArray
    -   NSDictionary
    -   NSString
    -   NSData
    -   NSDate
    -   NSNumber(integer, float, Boolean)



```objc
//
//  main.m
//  Stockz
//
//  Created by CHI YU CHAN on 31/10/2020.
//

#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
	@autoreleasepool {
	    // insert code here...
		NSMutableArray *stocks = [[NSMutableArray alloc] init];
		
		NSMutableDictionary *stock;
		stock = [NSMutableDictionary dictionary];
		[stock setObject:@"AAPL" forKey:@"symbol"];
		[stock setObject:[NSNumber numberWithInt:200] forKey:@"shares"];
		[stocks addObject:stock];
		
		stock = [NSMutableDictionary dictionary];
		[stock setObject:@"GOOG" forKey:@"symbol"];
		[stock setObject:[NSNumber numberWithInt:160] forKey:@"shares"];
		[stocks addObject:stock];
		
		[stocks writeToFile:@"/tmp/stocks.plist" atomically:YES];
		
		NSArray *stockList = [NSArray arrayWithContentsOfFile:@"/tmp/stocks.plist"];
		
		for (NSDictionary *d in stockList) {
			NSLog(@"I have %@ shares of %@", [d objectForKey:@"shares"], [d objectForKey:@"symbol"]);
		}
	}
	return 0;
}

```

