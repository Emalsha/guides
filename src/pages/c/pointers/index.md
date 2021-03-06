---
title: Pointers
---
# Pointers in C
By now you're aware that C is a low-level language, and nothing shows that better than pointers. Pointers are variables that get you the variable value by "pointing" to a memory location rather than storing the value of the variable itself. This allows for some handy tricks, and is also what gives us access to arrays and file handling, among other things.

## Making and Using a Pointer
```c
#include <stdio.h>
int main(void){
    double my_double_variable = 10.1;
    double *my_pointer;

    my_pointer = &my_double_variable;

    printf("%f\n", my_double_variable);
    ++my_double_variable;
    printf("%f\n", *my_pointer);

    return 0;
}
```

In this code, there are two declarations. The first is a typical variable initialization which creates a `double` and sets it equal to 10.1. New in our declarations is the usage of `*`. The asterisk (`*`) is usually used for multiplication, but when we use it by placing it in front of a variable it tells C that this is a pointer variable.  

The next line tells the compiler where that somewhere else actually is. By using `&` in this way, it becomes the 'dereferencing operator', and returns the memory location of the variable it's looking at.

With that in mind, let's take another look at this chunk of code:
```c
double *my_pointer;

my_pointer = &my_double_variable;
```
`my_pointer` has been declared, and it's been declared as a pointer. The C compiler now knows that `my_pointer` is going to point to a memory location. The next line assigns `my_pointer` a memory location value using the `&`.

Now let's take a look what referring to a memory location means for your code:
```c
printf("%f\n", my_double_variable);
++my_double_variable;
printf("%f\n", *my_pointer);
```
Notice that in order to get the value of the data at `*my_pointer`, you'll need to tell C that you want to get the value the variable is pointing at. Try running this code without that asterisk, and you'll be able to print the memory location, because that's what the `my_variable` variable is actually holding.

You can declare multiple pointer in a single statement as with standard variables, like so: 
```
int *x, *y;
```
Notice that the `*` is required before each variable. This is because being a pointer is considered as part of the variable and not part of the datatype.

## Practical Uses of Pointers
### Arrays
The most common application of a pointer is in an array. Arrays, which you'll read about later, allow for a group of variables. You don't actually have to deal with `*` and `&` to use arrays, but that's what they're doing behind the scenes.

### Functions
Sometimes you want to adjust a variable in a function, but if you pass it to an array, it has its own copy to work with. If instead you pass that memory location, however, you can access it from outside of its normal scope. This is because you are touching the original memory location itself, allowing you to adjust something in a function and having it make changes elsewhere.

### Tricks with Memory Locations
Whenever it can be avoided, it's a good idea to keep your code easy to read and understand. In the best case scenario, your code will tell a story- it will have easy to read variable names and make sense if you read it out loud, and you'll use the occasional comment to clarify what a line of code does.

Because of that, you should be careful when using pointers. It's easy to make something confusing for you to debug or for someone else to read. However, it is possible to do some pretty neat things with them.

Take a look at this code, which turns something from uppercase to lowercase:
```c
#include <stdio.h>
#include <ctype.h>

char *lowerCase (char *string) {
    char *p = string;
    while (*p) {
        if (isupper(*p)) *p = tolower(*p);
        p++;
    }
    return string;
}
```
This starts by taking a string (something you'll learn about when you get into arrays) and runs through each location. Notice the p++. This increments the pointer, which means that it is looking at the next memory location. Each letter is a memory location, so in this way the pointer is looking at every letter and deciding what to do for each one.

### Const Qualifer
The qualifier const can be applied to the declaration of any variable to specify that its value will not be changed ( Which depends upon where const variables are stored, we may change value of const variable by using pointer ).

# Pointer to variable
We can change the value of ptr and we can also change the value of object ptr pointing to.
Following code fragment explains pointer to variabel
```
#include <stdio.h>
int main(void)
{
    int i = 10;
    int j = 20;
    int *ptr = &i;        /* pointer to integer */
    printf("*ptr: %d\n", *ptr);
  
    /* pointer is pointing to another variable */
    ptr = &j;
    printf("*ptr: %d\n", *ptr);
  
    /* we can change value stored by pointer */
    *ptr = 100;
    printf("*ptr: %d\n", *ptr);
  
    return 0;
}
```
# Pointer to constant
We can change pointer to point to any other integer variable, but cannot change value of object (entity) pointed using pointer ptr.
```
#include <stdio.h> 
int main(void)
{
    int i = 10;   
    int j = 20;
    const int *ptr = &i;    /* ptr is pointer to constant */
  
    printf("ptr: %d\n", *ptr); 
    *ptr = 100;        /* error: object pointed cannot be modified
                     using the pointer ptr */
  
    ptr = &j;          /* valid */
    printf("ptr: %d\n", *ptr);
  
    return 0;
}
```
# Constant pointer to variable
In this we can change the value of the variable the pointer is pointing to. But we can't change the pointer to point to 
another variable.
```
#include <stdio.h>
int main(void)
{
   int i = 10;
   int j = 20;
   int *const ptr = &i;    /* constant pointer to integer */
  
   printf("ptr: %d\n", *ptr);
  
   *ptr = 100;    /* valid */
   printf("ptr: %d\n", *ptr);
  
   ptr = &j;        /* error */
   return 0;
}
```
# constant pointer to constant
Above declaration is constant pointer to constant variable which means we cannot change value pointed by pointer as well as we cannot point the pointer to other variable.
```
#include <stdio.h>
  
int main(void)
{
    int i = 10;
    int j = 20;
    const int *const ptr = &i;        /* constant pointer to constant integer */
  
    printf("ptr: %d\n", *ptr);
  
    ptr = &j;            /* error */
    *ptr = 100;        /* error */
  
    return 0;
}
```

# Before you go on...
## A review
* Pointers are variables, but instead of storing a value, they store a memory location.
* `*` and `&` are used to access values at memory locations and to access memory locations, respectively.
* Pointers are useful for some of the underlying features of C.
