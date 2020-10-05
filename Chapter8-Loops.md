# Chapter 8 Loops

```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
	printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n"); 
    printf("Aaron is Cool\n");
    printf("Aaron is Cool\n");
    printf("Aaron is Cool\n");
	return 0; 
}

```



## The while loop

```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
	int i = 0;
    while (i < 12) {
        printf("%d. Aaron is Cool \n", i);
    }
	return 0; 
}


```



## The for loop

```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
	for (int i = 0; i < 12; i++) {
    	printf("%d. Aaron is Cool \n", i);
    }
    return 0;
}


```



## Break

-   exit the loop statement

```c
int main(int argc, const char * argv[])
{
	for (int i = 0; i < 12; i++) {
    	printf("Checking i = %d. \n", i)
            if (i + 90 == i * i ){
                break;
            }
        printf("The answer is %d.\n", i);
        return 0;
    }
    
}
```



## Continue

-   Forget the rest of this run through the code block, and start the next run through the code block 

```c
int main(int argc, const char * argv[])
{
int i;
for (i = 0; i < 12; i++) {
    if (i % 3 == 0) {
    continue; 
    }
	printf("Checking i = %d\n", i); 
    if (i + 90 == i * i) {
		break; 
    }
}
	printf("The answer is %d.\n", i); 
    return 0;
}
/**
Checking i = 1 
Checking i = 2 
Checking i = 4 
Checking i = 5 
Checking i = 7 
Checking i = 8 
Checking i = 10 
The answer is 10.
*/
```



## do-while loop

-   Seldom use
-   do not cehck the expression until it has executed the block
-   ensure the block is always executed at least once.

```c
int main(int argc, const char * argv[])
{
	int i = 0;
    do {
        printf("%d. Aaron is Cool\n", i);
        i++;
    } while (i < 12);
    return 0;
}
```

