# Python3

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-01
* @BasedOn: [Documentation][basedon]

[basedon]: https://docs.python.org/3/tutorial/introduction.html

<!-- TOC -->

1. [Overview](#overview)
2. [Syntax](#syntax)
3. [Variable types](#variable-types)
  1. [Initialize variable](#initialize-variable)
4. [Operations](#operations)
  1. [Strings](#strings)
    1. [Formatting](#formatting)
    2. [Substring](#substring)
  2. [Lists](#lists)
5. [Lists](#lists-1)
6. [Dictionaries](#dictionaries)
  1. [Deleting items](#deleting-items)
7. [Conditions](#conditions)
  1. [`if`](#if)
  2. [`in`](#in)
8. [Loops](#loops)
  1. [`for`](#for)
  2. [`while`](#while)
  3. [`...else`](#else)
9. [Functions](#functions)
10. [Objects](#objects)
  1. [Standard functions](#standard-functions)
    1. [Common](#common)
    2. [Parsing](#parsing)
    3. [Math](#math)
    4. [Str methods](#str-methods)
    5. [List methods](#list-methods)
    6. [Dictionary methods](#dictionary-methods)
    7. [Interactive mode (IPython)](#interactive-mode-ipython)
11. [Packages](#packages)
    1. [Import](#import)
    2. [Useful packages](#useful-packages)
12. [Numpy](#numpy)
13. [Commands](#commands)
  1. [Interactive mode](#interactive-mode)

<!-- /TOC -->

## Syntax

```python
# comment
var_name = 0 # without type
print(var_name) # without ; at the end
list_name = [ 0, 3.14, "lel", True, [ 1, '23' ] ] # lists are recursive
type(list_name) # returns 'list'
print("a"); print("b") # use ; to separate commands
a, b = 2, 3 # multi-assignments
if a == b: # no bracket, only :
    call1() # blocks via indentation
    call2() # may be 4 spaces or tab
# no need to close
```

## Variable types

- int
- float
- bool
    - `True` or `False`
- str
    - using `'` or `"`
    - can be formatted
- list
    - using `[` and `]`
    - may contain different types and other lists
    - reference types

> Note: Check type of variable with type() method.

### Initialize variable
```python
variable_name = "some_value"
some_number = 4
```

## Operations

- `+`, `-`, `*`, `/`, `%`
- `//` (floor division)
- `**` (power relationship)

- `==`, `!=`, `<`, `>`, `<=`, `>=`
- `is` (compares instances, not values)
- `not` (negation of boolean)

### Strings

```python
mystr = "hello" + " " + "world" "!" # auto-concatenation
mystr = "hello" * 3 # returns: "hellohellohello"
mystr = 'he"llo'
mystr = "he'llo"
mystr = r"h\e\l\l\o" # raw string (backslash doesn't escape chars)
# backslash remove auto-break
mystr = '''\
Hello
wordl!
''' # also works with """
mystr = ('These strings '
'are together')
```

#### Formatting

- `%s` string (can print any type)
- `%d` integer
- `%f` floating point
- `%.3f` floating point with 3 digits after dot
- `%x` lowercase or `%X` uppercase hex integers

```python
s1 = "hello"
s2 = "world"

var = "hello %s" % s2
var = "%s %s" % (s1, s2)
```
#### Substring

```python
s1 = "Hello world!"

var = s1[1:4] # returns: "ell"
var = s1[1:4:1] # same, returns: "ell"
var = s1[1::3] # skip 2 next, returns: "eood"
var = s1[::-1] # reverse, returns: "!dlrow olleH"
var = s1[20] # "IndexError"
var = s1[20:] # no error
```

### Lists

```python
a1 = [1, 2]
a2 = [3, 4]

var = a1 + a2 # returns: [1, 2, 3, 4]
var = a1 * 3 # returns: [1, 2, 1, 2, 1, 2]
```

## Lists

```python
list = [ 0, 3.14, "lel", True, [1, '23'], 9 ] # lists are recursive

list[1] #  points second element: 3.14
list[-1] # points last element: 9
list[4][1] # points: '23'

list[1:3] # points range: [ 3.14, "lel" ], 3rd isn't included
list[:3] # points from 0 to 2
list[4:] # points from 4 to the end of the list
list[0:6:2] # skip every second element

list[3] = "new value" # change value at index 3
"first" + list # add to the list at the start
list + [ "last", "one" ] # add 2 elements to the list at the end
del(list[3]) # delete element at index 3, shift the rest

another_list = list # reference list
another_list = list[:] # copy list
another_list = list(list) # copy list too
```

## Dictionaries


```python
dict1 = {}
dict1["keyA"] = 1
dict1["keyB"] = 2
dict1["keyC"] = 3

# or

dict1 = {
    "keyA" : 1,
    "keyB" : 2,
    "keyC" : 3
}

print(dict1) # returns: {'keyA': 1, 'keyB': 2, 'keyC': 3}

for key_var, val_var in dict1.items():
    print("%s: %s" % (key_var, val_var))
```
### Deleting items
```python
del dict1["A"]
# or
dict1.pop("A")
```

## Conditions

```python
print(2 == 2) # returns: True

print(2 == 2 and 2 == 1) # returns: False
print(2 == 2 or 2 == 1) # returns: True
```

### `if`

```python
if a == b and c == d:
    print("Some text")
elif a == b or c == d: # else if
    print("Some text")
else:
    print("Some text")
```

### `in`

```python
s1 = "world"

if s1 in ["hello", "world"]:
    print("Some text")

if s1 not in ["hello", "world"]:
    print("Some other text")
```

## Loops

### `for`

```python
list1 = [1, 2, 3, 4]

for element in list1:
    print(element)

for element in range(3, 8, 2)
    print(element)
```

### `while`

```python
count = 0
while count < 5:
    print("Some text")
    if count == 1:
        continue
    if count == 6:
        break
    count += 1
```

### `...else`

```python
while condition:
    if a == b:
        continue
    call1()
else: # is called only after condition was not met
    call2()

for el in elements:
    if a == b:
        break
    call1()
else: # is not called because of break
    call2)()
```

## Functions

```python
def func():
    print("Some text")

func()
```
```python
def func(a, b)
    print("%s - %s" % (a, b))

func("hello", "world")
```
```python
def func(a, b)
    return a + b

var = func(2, 3)
```

## Objects

```python
class MyClass
    var = "hello"

    def func(self):
        print("Some text")

obj = MyClass()

print(obj.var)

obj.func
```

### Standard functions

#### Common
- `print(var)`: print variable (only one type per call)
- `type(var)`: return type
- `del(var)`: delete variable
- `len(var)`: return length of list or string
- `range(start, end, step)`: generates list with numbers in range

#### Parsing
- `int("3")`: parse parameter to int
- `float("3.14")`: parse parameter to float
- `bool("True")`: parse parameter to bool
- `str(3.14)`: parse parameter to str

#### Math
- `max(list[, 1, 2, 3])`: return biggest item
- `round(var[, n])`: round variable to n or 0 digits after delimeter

#### Str methods
- `var.capitalize()`: Large first letter
- `var.upper()`: Large all letters
- `var.lower()`: Small all letters


- `var.count(s)`: count occurrences of s
- `var.startsqith(s)`: is starting with s?
- `var.endswith(s)`: is ending with s?


- `var.split(" ")`: split string to list

#### List methods
- `var.index(3.14)`: return index of element of value 3.14
- `var.count(3.14)`: count occurrences of 3.14
- `var.append(val)`: append value to list at the end
- `var.remove(val)`: remove first element of value equal val
- `var.reverse()`: reverse list

#### Dictionary methods
- `var.items()`: return list of items in pairs
- `var.pop()`: delete item from dictionary

#### Interactive mode (IPython)
- `help(function_name)`: return help text about the function

## Packages

#### Import
```python
import package_name
import package_name as pkg_alias
from package_name import item # not recommended
from package_name import item as item_alias # not recommended
```
> Note: `import` is not required to be at the beggining of the document

#### Useful packages

- math
- numpy
    - has `array` type which can do batch operations

## Numpy

> Note: Arrays in contrast to lists cannot have different types in it.

```python
import numpy as np

array1 = np.array(list) # array from list
array1 = np.array([ 1, 2, 3, 4, 5 ]) # array from literal list

array2 = array1 * 2 # multiply every element in array by 2
print(array2) # return: [ 2, 4, 6, 8, 10 ]
array3 = array1 < 5 # array that contain True/False values whenewer each element
                    # is smaller than 5
print(array3) # return: [ True, True, False, False, False ]

array4 = array1[array1 < 5] # filter by condition  
# or
array4 = array1[array3] # return only these elements that corresponding element
                        # of array3 is True   
print(array4) #return: [ 2, 4 ]

array5 = np.array([ 1, 2, 3 ]) + np.array([ 1, 2, 3 ])
print(array5) # return: [ 2, 4, 6 ]

array6 = np.array([ [ 1, 2, 3 ], [ 1, 2, 3 ] ])
array_multiply = np.array([ 2, 3 ])
array7 = array6 * array_multiply
print(array7) # return: [ [ 2, 4, 6 ], [ 3, 6, 9 ] ]

print(array7.shape) # return: (2, 3)
print(array7[ :, 2 ]) # return: [ 6, 9 ] only 3rd column
```

> TODO: Divide examples for sections

## Commands

### Interactive mode

```python
$ python
>>>
```

```python
$ python
>>> print("hello")
hello
>>>
```

```python
$ python
>>> myvar = 30
>>> print(myvar)
30
>>>
```

```python
$ python
>>> print("hello");\
... print("world")
hello
world
>>>
```