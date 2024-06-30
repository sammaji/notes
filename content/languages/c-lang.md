---
title: c-lang
tags:
  - c
  - programming-language
  - cheatsheet
draft: true
---
## comments

```c
// single line comments

/**
	multi-line comments
**/
```

## macros
pre-processors directives or macros are values are replaced during compilation. they are not statements.

e.g, `#define X 10` -> will replace `X` in all the places where it is used, during compilation.

### include directive
include the contents of a file.
e.g, `#include <math.h>` -> will make the contents of the `math.h` file available for use.

## pointers in c
all these statements are correct.

```c
int *x;
int* x;
int * x;
```

but its better to choose the first one because, when you have multiple pointers, it will be easier to read. below are two statements, both mean the same. x is pointer and y is an integer.

```c
int *x, y; // easy to read
int* x, y; // confusing as y is not a pointer
```
## data types

### integers
`0xHEX` -> represents a hex number
`10u` -> unsigned integer
`10l` -> long
`xe2` -> x * 10 ^ 2

### floating point
`float x = 10.0f` -> float values
`double x = 10.0d` -> double values
`double x = 10.0l` -> high precision double values\
### char
single characters, enclosed by single quotes.
### string
string constants, an array of char, enclosed by double quotes.

```c
char *s = "hello";
char s[] = "world";
```

## user defined types
### typedef
you can use `typedef` to set aliases for datatypes.

```c
typedef int units;
unit x = 10;
```
### enums

```c
enum day {Mon, Tue, Wed};
enum day Mon, Tue, Wed;

// with values
enum day {Mon=1, Tue, Wed};

// grouping enums
enum day {Mon, Tue, Wed} week_day, {Sat, Sun} week_end;
```

### storage class specifiers
control how a variable is stored.
- `auto` -> only know within its scope. only known to the function in which it is declared. this is the default behaviour.
- `static` -> local variable which exists and retains it's value even after the control is transferred.
- `global` -> global variable known to all functions in the file.
- `register` -> local variable stored in the cpu register (fastest access).

e.g, `auto int x = 10;`

#### use of static
```c
int counter() {
  static int count = 0;
  count++;
  return count;
}

int main() {
  for (int i=0; i<5; i++) {
    printf("current count = %d\n", counter());
  }
}

/**
OUTPUT
------
current count = 1
current count = 2
current count = 3
current count = 4
current count = 5

**/
```

here, after every function call, we the `count` is retained by the function, which increments it.

if you use static with functions, then that function will only be callable from that file only. it's somewhat like the `private` keyword is java.
#### use of register
using register stores a value to CPU register, making read write extremely fast.

```c
#include <time.h>

int main() {
register int count;

clock_t start = clock();
for (count = 0; count < 1000000000l; count++) {}
clock_t end = clock();
double time = (double)(end-start)*1000/CLOCKS_PER_SEC;

printf("%fms\n", time);
return 0;
}
```

- since CPU registers have limited space, the compiler might choose to not put the value in the register.
- registers don't have memory addresses, so you cannot take pointers.
---
## quantifiers
#### const
declares a constant.

---
## operators in C
### logical operators
- `0` is considered `falsy`. any other number is `truthy`. e.g, `0 && 1 = 0 (false)`
### prefix and postfix
```c
// prefix
// add first, then assign
++p

// postfix
// assign first, then add
p++
```
### special operators
`sizeof (value)` -> returns the no. of bytes occupied by the object.
### eval of arithmetic expressions
- first, parenthesised sub expressions are evaluated. if nested parenthesis are present, the innermost parenthesis is evaluated first.
- arithmetic expressions are evaluated in two passes.
- in the first pass, the high priority operators are evaluated. in the second pass the low priority values are evaluated.
- `*`, `/`, `%` -> are high priority operators
- `+`, `-` -> low priority operators
### type conversion - implicit
- c support both implicit and explicit conversions.
- tries to convert all the values in an expression to the highest precedence type.
- `least` - `short/char` -> `int` -> `uint` -> `lint` -> `ulint` -> `float`-> `double` -> `ldouble` - `highest`
- e.g, `double + int` -> `double`
- during assignment, c might convert a higher type to lower type.
- e.g, `int x = double` -> `int`

