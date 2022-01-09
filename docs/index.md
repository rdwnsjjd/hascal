# Introduction
[Hascal](https://hascal.github.io) is a general-purpose open source programming language that makes it easy to build simple,optimal, reliable, and efficient software. 

## Installation
Prequistes :

- python v3.8 or higher
- pyinstaller 
- GCC/G++>=8.0.0 on your `$PATH`

First clone Hascal's source :
```
$ git clone https://github.com/hascal/hascal
```

Install prequistes(not gcc only python libs,if you already installed prequistes, skip this part):
```
$ make deps
```

Build hascal excutable file :

  - On POSIX(Linux,MacOS,BSDs) :
  ```
  $ make
  ```
  - On Windows :
  ```
  $ make windows
  ```

***Now your Hascal compiler is ready to use in `src/dist` folder!!!***
NOTE: But you can add Hascal to `$PATH` for easily use.

## Hello World
```typescript
function main() : int {
    print("Hello World")
    return 0
}
```
Save this snippet into a file named `hello.has`. Now do: `hascal hello.has`.

Congratulations - you just wrote and executed your first Hascal program!

As in many other languages (such as C++ and Rust), `main` is the entry point of your program.

`print` is one of the few built-in functions. It prints the value passed to it to standard output.

## `config.json` :
You can use `config.json` to configure your Hascal compiler.

- `compiler` : your c++ compiler name(e.g : `g++`,`clang++`)
- `optimize` : optimize level(0,1,2,3)
- `flags` : flags list for your compiler(e.g:`["-pthread"]`)
- `no_check_g++` : if you don't use g++, set this to `1`
- `c++_version` : your c++ standard(e.g:`c++17` or `c++20`).note: c++ version must be greater than or equal to c++17
- `g++_out` : if you want to see g++ output, set this to `1`
- `c++_out` : if you want to see generated c++ code, set this to `1`

example :
```json

{
    "compiler":"g++",
    "optimize":"-O2",
    "flags":["-pthread"],
    "no_check_g++":1,
    "c++_version":"c++17",
    "g++_out":1,
    "c++_out":1
}
```

## Comments
```typescript
// This is a single line comment
```

## Variables
```typescript
var foo : int
var foobar : int = 1

var bar = 1
function main() : int {
    print(foo,foobar)
    return 0
}
```

## Functions
```typescript
function add(x:int,y:int): int {
    return x + y
}

// overloading function
function add(x:int,y:int,z:int): int {
    return x + y + z
}

function add2(x:int,y:int){
    print(x + y)
}

function main(): int {
    print(add(1,2))
    print(add(1,2,3))
}
```
Again, the type comes after `:` and `:` comes after the argument's name.

## Hascal Types

### Primitive types
```typescript
bool // boolean value

string // string literal

int // integer value

float // floating point 
double // double floating point(soon)
```

### Strings
```typescript
function main() : int {
    var text = "Hello World"
    print(text[0]) // output : H 

    var text2 = "Hello\tWorld"
    print(text2) // output : Hello   World
    return 0
}
```

### String operators
```typescript
function main() : int {
    var text = "Hello "
    print(text + "World") // output : Hello World 
    return 0
}
```
All operators in Hascal must have values of the same type on both sides. You cannot concatenate an integer to a string:
```typescript
function main() : int {
    var text = "age = "
    var age = 23
    print(text + age) // error : Mismatched type 'string' and 'int' :2 
    return 0
}
```
We have to either convert age to a string:
```typescript
function main() : int {
    var text = "age = "
    var age = 23
    print(text + to_string(age)) // error : Mismatched type 'string' and 'int' :3
    return 0
}
```

### Numbers
```typescript
function main() : int {
    var a : int = 123 // or : var a = 123
    var b : float = 1.23 // or : var b = 1.24
    return 0
}
```
This will assign the value of `123` to `a` and `1.23` to `b`.

### Arrays
#### Basic Array Concepts
Arrays are collections of data elements of the same type. They can be represented by a list of elements surrounded by brackets. The elements can be accessed by appending an index (starting with 0) in brackets to the array variable:
```typescript
function main() : int {
    var a = [1,2,3] // int array with length 3
    var b = [1.0,2.0,3.0] // float array with length 3
    print(a[0])
    a[0] = 4
    print(a[0])
    return 0
}
```

#### Array Initialization
The basic initialization syntax is as described above. The type of an array is determined by the first element:

- `[1, 2, 3]` is an array of ints (`[int]`).
- `["a", "b"]` is an array of strings (`[string]`).

#### Array Size
You can get length of array's elements with `len` function :
```typescript
function main() : int {
   var a = [1,2,3]
   print(len(a)) // output : 3
}
```

#### Array append
You can append elements to array with `append` function :
```typescript
function main() : int {
   var a = [1,2,3]
   append(a,4)
   for e in a {
       print(e)
   }
   return 0
}
```

## Importing Libraries
Libraries can imported with `use` keyword :
```typescript
use os
function main() : int {
   system("gcc --version")
   return 0
}
```
If you want to import a local library, you can use `local` keyword :
```typescript
local use addlib //import add()
function main() : int {
   print(add(1,2))
   return 0
}
```

## If
```typescript
var x = 1
var y = 2
function main() : int {
   if x == y {
       // something
   } else if not x != y {
       // something
   } else if x == y and x != 2 {
       // something
   } else if x != y or x == 10 {
       // something
   } else {
       // something
   }
   return 0
}
```
`if` statements are pretty straightforward and similar to most other languages. Unlike other C-like languages, there are no parentheses surrounding the condition and the braces are always required.
> You can see Hascal's conditional operators, [here](cond_op/index.html)

## For Loop
```typescript
function main() : int {
   var a = [1,2,3]
   for i in a {
       print(i) // prints elements of `a` variable
   }
   return 0
}
```

## While Loop
```typescript
function main() : int {
   var a = 1
   while a <= 100 {
       print(a)
       a = a + 1
   }
   return 0
}
```
## Structs
```typescript
struct Color {
    var r : int
    var g : int
    var b : int
    var name = "Transparent" // optional value
}

struct RGB : Color {
    // struct inheritance
}

function main() : int {
    var a : Color
    a.r = 1
    a.g = 110
    a.b = 255
    print(a.r,a.g,a.b)
   
    var b = Color(34,156,255,"AColor")

    var c = RGB(255,0,0,"AColor")
    return 0
}
```

## Inline C++ Code
You can use inline c++ code in hascal with `cuse` keyword :
```typescript
cuse '#include <cstdio>'
cuse 'int main(){printf("%d",1);return 0;}'
// output : 1
```

## Include C++ Code
You can include C++ code in your Hascal file with `cuse` keyword :

`add.cc` :
```cpp
int add(int x, int y) {
    return x + y;
}
```
`add.hpp` :
```cpp
// nothing but should be exist
// if you want to include a c++ header file, you should include it in this file and not in `xxx.cc`
// e.g :
// #include <cmath>
```

`main.has` :
```typescript
// if you want to include a local file use `local` keyword 
// but if you want to include a file in hascal standard library folder don't use `local` keyword
local cuse add 

function add(a:int,b:int): int

function main() : int {
    print(add(1,2))
    return 0
}
```