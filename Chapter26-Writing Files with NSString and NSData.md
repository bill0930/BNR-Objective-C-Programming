# Chapter26-Writing Files with NSString and NSData

 how you would take the contents of an **NSString** and put it into a file

-   specify which *string encoding* you are using

-   string encoding means how each char is stored as an array of bytes.
-   ASCII , letter A is 01000001. UTF-16 letter A is 0000000001000001.
-   we usually use UTF-8



```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) { 
    @autoreleasepool {
		NSMutableString *str = [[NSMutableString alloc] init]; 
        for (int i = 0; i < 10; i++) {
            [str appendString:@"Aaron is cool!\n"]; 
        }
        [str writeToFile:@"/tmp/cool.txt" atomically:YES encoding:NSUTF8StringEncoding error:NULL];
        NSLog(@"done writing /tmp/cool.txt");
	}
return 0; }
```



File paths can be absolute or relative: 

-   absolute paths start with a / that represents the top of the file system, 
-   whereas relative paths start at the working directory of the program. Relative paths do not start with a /



## NSError

-   may get error, e.g. 
    -   wrtie-access to the directory or
    -    the directory may not exist or
    -   the filesystem may be fuil

-   The method needs a way to return a description of what went wrong in adiition to the boolean value for success or failur

```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) { 
    @autoreleasepool {
		NSMutableString *str = [[NSMutableString alloc] init]; 
        for (int i = 0; i < 10; i++) { [str appendString:@"Aaron is cool!\n"]; }
// Declare a pointer to an NSError object, but do not instantiate it.
// The NSError instance will only be created if there is, in fact, an error. 
        NSError *error;
// Pass the NSError pointer by reference to the NSString method 
        BOOL success = [str writeToFile:@"/tmp/cool.txt" 
                        atomically:YES 
                        encoding:NSUTF8StringEncoding
                        error:&error];
// Test the returned BOOL, and query the NSError if the write failed 
        if (success) {
			NSLog(@"done writing /tmp/cool.txt"); 
        } else {
			NSLog(@"writing /tmp/cool.txt failed: %@", [error localizedDescription]); 
        }
	}
return 0; }
```



If there is an error, **writeToFile:atomically:encoding:error:** will be responsible for creating a new **NSError** instance and then modifying the error pointer you declared to point to the new error object



```objc
- (BOOL)writeToFile:(NSString *)path 
    atomically:(BOOL)useAuxiliaryFile
        encoding:(NSStringEncoding)enc 
            error:(NSError **)error
                //The method expects an address where it can put a pointer to an instance of NSError.”

```



## Reading files with NSString

```objective-c
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) { 
    @autoreleasepool {
		NSError *error;
		NSString *str = [[NSString alloc] initWithContentsOfFile:@"/etc/resolv.conf"
                                                        encoding:NSASCIIStringEncoding
                                                           error:&error];
		if (!str) {
			NSLog(@"read failed: %@", [error localizedDescription]);
		} else {
			NSLog(@"resolv.conf looks like this: %@", str); 
        }
    }
	return 0; 
}
```



## Writing an NSData object to a file

```objective-c
// NSData object represents a bufgfer of bytes.

#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
		NSURL *url = [NSURL URLWithString: @"http://www.google.com/images/logos/ps_logo2.png"];
		NSURLRequest *request = [NSURLRequest requestWithURL:url]; NSError *error = nil;
		NSData *data = [NSURLConnection sendSynchronousRequest:request
                                              returningResponse:NULL
                                                          error:&error];
        if (!data) {
       		NSLog(@"fetch failed: %@", [error localizedDescription]);
        return 1; 
        }
        NSLog(@"The file is %lu bytes", (unsigned long)[data length]);
        
        BOOL written = [data writeToFile:@"/tmp/google.png" 
                        options:NSDataWritingAtomic 
                        error:&error];
        if (!written) {
        	NSLog(@"write failed: %@", [error localizedDescription]);
        return 1; }
        	NSLog(@"Success!");
        
        	NSData *readData = [NSData dataWithContentsOfFile:@"/tmp/google.png"]
           NSLog(@"The file read from the disk has %lu bytes", (unsigned long)[readData length]);
        }
		return 0; 
}
```



## Finding special Directories

```objc
// The function returns an array of paths 
NSArray *desktops = NSSearchPathForDirectoriesInDomains(NSDesktopDirectory, NSUserDomainMask, YES)
// But I know the user has exactly one desktop directory 
    NSString *desktopPath = desktops[0];
NSApplicationDirectory
• NSLibraryDirectory
• NSUserDirectory
• NSDocumentDirectory
• NSDesktopDirectory
• NSCachesDirectory
• NSApplicationSupportDirectory • NSDownloadsDirectory
• NSMoviesDirectory
• NSMusicDirectory
• NSPicturesDirectory • NSTrashDirectory
```

