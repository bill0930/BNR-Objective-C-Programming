# Chapter 6 Format Strings

## printf

-   accepts a strings as an argument and prints it to the log

-   A string is a "string" of characters strung together like beads on a necklace.

-   ```c
    // Print the beginning of the novel
    printf("It was the best of times.\n");
    printf("It was the worst of times.\n");
    ```

-   you can store a literal string in a variable type char *
-   `char *myString = "Here is a string";`



```c
// Write the beginning of the novel
char *firstLine = "It was the best of times.\n"; char *secondLine = "It was the worst of times.\n";
// Print the beginning of the novel
 printf(firstLine);
 printf(secondLine);
```



## using tokens 

-   prinf function can do more than print literal strings
-   can also use it to create custom strings at runtime using tokens and varaibles



```c
void congratulateStudent(char *student, char *course, int numDays)
{
	printf("%s has done as much %s Programming as I could fit into %d days.\n", student, course, numDays);
    
}

```

-   When you pass a string containing one or more tokens to **printf()**, the string that you pass is called the *format string*. 
-   In this example, the format string includes three tokens: %s, %s, and %d.



## Escape sequences

-   \n = put at the end of your strings is `escape sequences`
-   \, it is a `escape character`

Example: 

`printf("\"It doesn't happen all at once,\" said the Skin Horse.\n");`

Output

`"It doesn't happen all at once," said the Skin Horse.`

