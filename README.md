# Stoopid
This is my attempt at the version of Ooid that I tended toward, but the
version that I don't think Ooid is or should be. It's going to an overly
simple version and I don't even know if it will be turing complete.
## Types
Only integers because I am lazy. I think they should be unbounded, but I
will not implement that. There will be conditional functions, so I use C
style booleans. I.e. 0 is false, everything else is true.
## Function Definitions
Function defintions include a name at the top with spaces on each side.
The inputs are on the edges and are connected to functions within the
function definition. Definitions can be nested. When a function is
called it runs the closest matching definition. 
```
+-- brand new function definition --+
|  +-- nested definition --+        |
|  |                       |        |
|  |  +---+  +---+         |        |
|  i--x + y--o 1 |         |        |
|  |  +-o-+  +---+         |        |
|  |    |                  |        |
|  +----o------------------+        |
|                                   |
|  +-------------------+            |
|--i nested definition |            |
|  +--o----------------+            |
|     |                             |
|  +--i----------------+            |
|  | nested definition |            |
|  +--o----------------+            |
|     |                             |
+-----o-----------------------------+
```
## Function Calling
A function runs as soon as it has all of its inputs. If a function never
receives all of its inputs it won't run. A builtin function outputs
immediately. A user-defined function runs all of the functions within it
before outputting.

I would like functions to run on fixed time steps, such that all
functions that can run on a given step do run. In this case if there are
more than one input and/or more than one output running on the same step
it should crash the program.
## Commands
### Input
```
+-------+
| input |
+---o---+
```
Receives input from outside the program. I am leaving this to be used
however.
### Output
```
+---i----+
| output |
+--------+
```
Outputs whatever is passed to `i`. I am leaving this to be used however.
### Number
```
+-------+
| 12345 |
+---o---+
```
Puts whatever number is written in the function name `o`. Numbers are
base 10.
### Arithmetic
```
+---+  +---+  +---+  +---+
x + y  x - y  x * y  x / y
+-o-+  +-o-+  +-o-+  +-o-+
```
Does `o = x op y`. Division is integer division
### Comparisons
```
+---+  +---+  +---+
x = y  x > y  x < y
+-o-+  +-o-+  +-o-+
```
Does what you expect.
### Boolean
```
+---+  +---+  +-i-+
x & y  x | y  | ! |
+-o-+  +-o-+  +-o-+
```
Boolean and, or, and not. They are not bitwise, and will return either 0
or 1.
### Split
```
+---i---+
a split b
+-------+
```
Puts `i` on `a` and `b`.
### Maybe
```
+---i---+
| maybe c
+---o---+
```
Outputs `i` on `o` if `c`.
### Choose
```
+--t--f--+
| choose c
+---o----+
```
If `c` puts `t` on `o` otherwise puts `f` on `o`.
