---
title: intro
tags: 
draft: true
---
- compiled, statically typed.
- `var x = 10` <- initialise a variable (type infered)
- strongly typed, doesn't support implicit casting 🔥

assignment -> `var <varname> <dtype> = <value>`
alt syntax -> `<varname> := <value>`

more fancy assignment
- var x, y = 1, 2
- x, y := 1, 2

`const` -> immutable
### data types
- ints and uints -> int, int8, int 16, int32, int64, uint, unit8, etc.
- int will be int32 (32 bits) or int64 (64 bits) depending on the system architechture.
- float -> float32 or float64, no float.
- string -> use \" for single line string, and \` for multi-line strings.
- bool -> true or false.

default values -> go assigns default values to variables. for numeric values its 0, for bool its false, and for strings, its empty strings.
### strings
`len(string)` function -> returns number of bytes instead of no. of charecters.

easy way of fixing this issue is to cast a string into a list of runes.
`var s = []rune("hello")`

string builder
- strings in go are immutable.
- `sb.WriteString(str)` -> add strings to string builder
- `sb.String()` -> returns a string

type casting
- int(value), or float32(value), etc.

### printing
use the `fmt` package to print things to the console.
- `fmt.Println("Hello world")`
- `fmt.Printf("result=%v, type=%T", result, result)`
### conditionals
- if / else -> `if a==b && b==c {} else if ...`

switch case
```go
switch {
	case true:
		
}
```
### functions

```go
func add(a int, b int) int {
	return a + b
}
```

we can also return multiple values.
```go
func divide(a int, b int) (int, int) {
	const q = a / b
	const r = a % b
	return q, r
}
```


### error handling

go has a type for error -> `var err error = nil`

throw an error:
```go
import "errors"

func divide(a int, b int) (int, int, error) {
	if b==0 {
		err = errors.New("cannot divide by zero") // new error
		return 0, 0, err
	}
}
```

it is a general design pattern to return the error like this, this error can be handled after reading the function.

### arrays
- `var <name> [size]dtype`
	- e.g. `var arr [3]int`
	- initialise it like this -> `var arr [3] int = [3]int{1,2,3}`
- supports slicing. (inc,excl) -> `arr[1:3]`
- arrays are fixed size

### slices
- arrays, but with variable size.
- `var sl []int32 = []int32{1,2,3}`
- or, `var sl []int32 = make(dtype, length, capacity)`
	- e.g., `var sl []int32 = make(int32[], 4, 8)`

```go
append(sl, 7)      // add new elements
append(sl, arr...) // spread op
len(sl)            // no. of filled spaces
cap(sl)            // no. of elements it can accomodate
```

### map

```go
// INIT
var mp map[string]uint8 = make(map[string]uint8)

// with initial values
var mp = map[string]unit8{"Adam": 23, "Sara": 19}

var value = mp["Adam"]

// if value is non-existent, then,
// it returns the default value for the type
// in our case it is 0
var value = mp["Jane"]

// ok is false for non-existent values,
// true otherwise
var value, ok = mp["Jane"]

// delete
delete("Adam")
```

### iteration

go uses the range keyword to iterate over iterators. here are the different syntax for iterating.

```go
// arrays, slices
// i -> index, v -> value
for i,v := range sl {}

// maps
for key, value := range mp {}
```

standard for loop
```go
for <conditon> {
	// block
}

for <init>; <condition>; <update> {}

for {
	// infinite loop
}
```

### struct and interfaces

structs lets you define your own types.
```go
type MyType struct {
	age int8
	name string
}
```

now, you can use the struct as a type.
```go
var mytype MyType = MyType{age: 20, name: "sam"}
```