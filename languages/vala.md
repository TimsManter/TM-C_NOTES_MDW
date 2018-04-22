# Vala

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)  
* @CreationDate: 2017-01
* @BasedOn: [GNOME Wiki][basedon]

[basedon]: https://wiki.gnome.org/Projects/Vala/Tutorial

<!-- TOC -->

1. [Overview](#overview)
2. [Hello World!](#hello-world)
3. [Types](#types)
    1. [Cast](#cast)
    2. [Inference](#inference)
4. [Strings](#strings)
  1. [Initialize](#initialize)
5. [Numbers](#numbers)
6. [Parsing](#parsing)
7. [Arrays](#arrays)
8. [Slice](#slice)
  1. [String](#string)
  2. [Array](#array)
9. [Class](#class)
  1. [Constructor and destructor](#constructor-and-destructor)
10. [Operators](#operators)
11. [Control](#control)
12. [Method](#method)
  1. [Delegate](#delegate)
  2. [Lambda expresion](#lambda-expresion)
13. [Namespace](#namespace)
14. [Struct](#struct)
15. [Interface](#interface)
16. [Signal (event)](#signal-event)
17. [Property](#property)

<!-- /TOC -->

## Hello World!

```vala
class Demo.HelloWorld : GLib.Object {
    public static int main(string[] args) {
        stdout.printf("Hello, World\n");
        return 0;
    }
}
```

## Types

- Byte
    - `char`
    - `uchar`
- Character
    - `unichar` (32-bit)
- Integer
    - `int`
    - `uint`
- Long Integer
    - `long`
    - `ulong`
- Short Integer
    - `short`
    - `ushort`
- Sized Integers
    - `int8`
    - `int16`
    - `int32`
    - `int64`
    - `uint8`
    - `uint16`
    - `uint32`
    - `uint64`
- Float
    - `float`
    - `double`
- Bool
    - `bool`
- Compound
    - `struct`
- Enumeration
    - `enum`
- Text
    - `string`
        - immutable
        - UTF-8


#### Cast

```vala
int i = 10;
float j = (float) i;
```
#### Inference

```vala
var p = new Person();     // Person p = new Person();
var s = "hello";          // string s = "hello";
var l = new List<int>();  // List<int> l = new List<int>();
var i = 10;               // int i = 10;
```
## Strings

### Initialize
```vala
string text = "Some text.";

string verbatim_text = """This variable is "verbatim string".
All line breaks and escapes are preserved \n \t \\ etc.
Even single ' and double " quotes.""";

int a = 1, b = 2;
string string_template = @"$a * $b = $(a * b)";
```

## Numbers

```vala
uint8 b = text[4]; // Get one byte
```
## Parsing

```vala
bool b = bool.parse("false");           // false
int i = int.parse("-52");               // -52
double d = double.parse("6.67428E-11"); // 6.67428E-11
string s1 = true.to_string();           // "true"
string s2 = 21.to_string();             // "21"
```
## Arrays

> Note: Jagged array not yet supported.

```vala
int[] a = new int[10]; // empty array
int[] b = { 2, 4, 6, 8 };

int l = b.lenght // 4

int[,] c = new int[3,4];
int[,] d = {{2, 4, 6, 8},
            {3, 5, 7, 9},
            {1, 3, 5, 7}};
d[2,3] = 42;

int l_0 = c.lenght[0] // 3
int l_1 = c.lenght[1] // 4
```
## Slice

> Note: Just like in Python.
### String
```vala
string text = "hello world";
string s1 = text[6:8];    // "wo"
string s2 = text[-10:-8]; // "el"
```
### Array
> Note: It doesn't work for multi-dimentional arrays.
```vala
int[] array = { 2, 4, 6, 8 };
int[] slice = array[1:3]; // { 4, 6 }
```

## Class

```vala
class Track : GLib.Object, IInterface {
    private bool terminated = false; // a private field
    public double mass;              // a public field
    public double name { get; set; } // a public property
    public void terminate() {        // a public method
        terminated = true;
    }
}
```
### Constructor and destructor
```vala
public class Button : Object {
    public Button() { }
    public Button.with_label(string label) { this() } // named constructor
    public Button.from_stock(string stock_id) {       // other name
        this.with_label("lel" + stock_id);            // chain constructor
    }
    public ~Button() { }
}

new Button();
new Button.with_label("Click me");
new Button.from_stock(Gtk.STOCK_OK);
```

## Operators

- `=`
- `+`, `-`, `/`, `*`, `%`
- `+=`, `-=`, `/=`, `*=`, `%=`
- `++`, `--`
- `|`, `^`, `&`, `~`, `|=`, `&=`, `^=`
- `<<`, `>>`, `<<=`, `>>=`
- `==`, `!=`, `<`, `>`, `<=`, `>=`
- `!`, `&&`, `||`
- `? :` (one-instruction if)
- `??` (null check)
- `in` (right contains left)

## Control

- `while`
- `do...while`
- `for`
- `foreach` (with `in`)
- `if...else`
- `switch...case...break`

## Method

> Note: Method overloading with same name is not permited.
```vala
void f(int x, string s = "hello", double z = 0.5) { } // default parameters

f(2);
f(2, "hi");
f(2, "hi", 0.75);

string? method_name(string? text, Foo? foo, Bar bar) { } // nullable parameters
```

### Delegate

```vala
delegate void DelegateType(int a);

void f1(int a) { }

void f2(DelegateType d, int a) {
    d(a);       // Calling a delegate
}

void main() {
    f2(f1, 5);  // Passing a method as delegate argument to another method
}
```

### Lambda expresion

```vala
delegate int DelegateType(int param);

DelegateType lambda = (x) => { return 0; }
```

## Namespace

> Note: `using GLib;` is added implicitly.
```vala
namespace NameSpace { }

using NameSpace;
```
## Struct

```vala
struct Name { }

Color c1 = Color();  // or Color c1 = {};
Color c2 = { 0.5, 0.5, 1.0 };
Color c3 = Color() {
    red = 0.5,
    green = 0.5,
    blue = 1.0
};
```

## Interface

```vala
interface IName : IBase { }
```

## Signal (event)

```vala
public class Test : GLib.Object {
    public signal void sig_1(int a);

    public static int main(string[] args) {
        Test t1 = new Test(); // signals are part of classes

        t1.sig_1.connect( (t, a) => { } ); // connect lambda to signal
        t1.sig_1(5); // emit signal

        return 0;
    }
}
```

## Property

```vala
class Person : Object {
    private int _age = 32;

    public int age {
        get { return _age; }
        set { _age = value; }
        default = 32; // default value of property
    }
}

obj.notify.connect((s, p) => { });
obj.notify["age"].connect((s, p) => { });
```