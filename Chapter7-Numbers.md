# Chapter 7 - Numbers

## Integers

-   An integer is a number without decimal points
-   typical sizes are 8-bit, 16-bit, 32-bit and 64-bit
-   can be signed and unsinged 
-   unsinged 8-bit can hold any integer from 0 to 255 , which is 256 possibility

```c
UInt32 x; // An unsinged 32-bit integer
SInt1 y;  // A signed 16-bit integer

char a; //8 bits
short b; // usuaully 16 bit
int c; // usually 32 bit
long d; // 32 or 64bits
long long e; // 64 bits

```



### Tokens for displayng integers

```c

#include <studio.h>
int main (int argc, const char * argv[]) {
    int x = 255;
    printf("x is %d. \n", x);
    printf("In octal, x is %o.\n", x);
    printf("In hexadecimal, x is %x.\n", x)
    return 0;
}


// should slip %l when printing long bit integer 

#include <stdio.h>
int main (int argc, const char * argv[])
{
    long x = 255;
    printf("x is %ld.\n", x);
    printf("In octal, x is %lo.\n", x); 
    printf("In hexadecimal, x is %lx.\n", x);
	return 0; 
}

// should use %u when printing unsigned decimal 
#include <stdio.h>
int main (int argc, const char * argv[])
{
	unsigned long x = 255; 
    printf("x is %lu.\n", x);
// Octal and hex already assume the number was unsigned 
    printf("In octal, x is %lo.\n", x);
	printf("In hexadecimal, x is %lx.\n", x);
	return 0; 
}

```

### Integer Operations

-   +, - ,* work as expected
-   \* is evaluated before + or -. 

```c
#include <stdio.h>
int main (int argc, const char * argv[]) {
	printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
	return 0; 
}
```

-   but not division
-   need to cating denominator when doing the divison

```c
#include <stdio.h>
int main (int argc, const char * argv[]) {
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d\n", 11 / 3);
    printf("11 / 3.0 = %f\n", 11 / (float)3);
return 0; 
}

// 11 / 3 = 3
```

### NSInteger and NSUInteger

-  Xcode supports the development of both 32-bit and 64-bit applications
-  32-bit then 32-bit, 64-bit then 64-bit
-  NSInterger is signed, NSUInteger is unsigned
-  Recommend way of outputting NSInteger or NSUInteger is casting them to appropriate long before trying to display them

```c
NSInteger x = -5;
NSUInteger y = 6;
printf("Here they are: %ld, %lu", (long)x, (unsigned long)y);
```

### Operator shorthand

-   x++; x--;
-   x += 5, x-=5, x*=5, x/= 5. x%=5;
-   use `abs()` for int type, use `labs()` for long type declared in `stdlib.h`



## Floating-point numbers

-   Printf() can also dispalys floating point numbers using the tokens `%f` and `%e` 

```c
int main (int argc, const char * argv[]) {
    double y = 12345.6789;
    printf("y is %f\n", y);
    printf("y is %e\n", y);
    
    printf("y is %.2f\n", y);  //limit to 2 dp
    printf("y is %.2e\n", y); 
    
    return 0;
}
// y is 12345.678900 , %f normal decimal notation, 6-digit
// y is 1.234568e+04 , %e scientific notation
```

### The math library

`#include <math.h>`

