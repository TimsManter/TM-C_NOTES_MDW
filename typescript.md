# TypeScript

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2016-12
* @BasedOn: [Documentation](https://www.typescriptlang.org/docs/tutorial.html)

<!-- TOC -->

1. [Overview](#overview)
2. [Variables](#variables)
  1. [`let` keyword](#let-keyword)
  2. [`const` and `readonly` keywords](#const-and-readonly-keywords)
  3. [Types](#types)
  4. [Type assertions](#type-assertions)
  5. [Array destructuring](#array-destructuring)
  6. [Array spreading](#array-spreading)
  7. [Variables/properties operations](#variablesproperties-operations)
3. [Enums](#enums)
4. [Interfaces](#interfaces)
5. [Classes](#classes)

<!-- /TOC -->

## Variables

### `let` keyword

```typescript
let someVariable: type = "value"
```
`let` keyword is similar to `var` but makes variable accessible only inside
the block, where is defined instead of entire scope.

```typescript
function f() {
    if (condition) {
        var x = "value"
    }
    // x is accesible here
}

function f() {
    if (condition) {
        let x = "value" // let instead of var
    }
    // x is inaccesible here
}
```

### `const` and `readonly` keywords

> Note: Variables use `const` whereas properties use `readonly`.

### Types

* boolean
* number
    * decimal: 6
    * hex: 0xf00d
    * binary: 0b1010
    * octal: 0o744
* string
    * 'single'
    * "double"
    * \`template with ${ expression + 1 }  
    can be multiline\`
* array
    * someVar type[] = []
    * someVar: Array<type> = []
    * someVar: ReadonlyArray<type> = []
* tuple (multi-type)
    * someVar: [type1, type2, ...] = [x, y]
    * access by index - someVar[0]
* any
    * may be any type
    * may be array of different types - any[]
* void
    * useful as return type
* undefined
    * not useful
* null
    * not useful
* never
    * useful as return type
    * used when function has unreachable end

### Type assertions
Castig types without checking it's possible.

```typescript
let someValue: any = "this is a string";
// two ways to assert as string
let strLength: number = (<string>someValue).length;
let strLength: number = (someValue as string).length;
```

### Array destructuring
```typescript
let input = [1, 2];

// desctructuring variables
let [first, second] = input;
// equivalent for
let first = input[0];
let second = input[1];

// descructuring with rest
let [first, ...rest] = [1, 2, 3, 4];
// first is 1
// rest == [2, 3, 4]

// descructuring selected
let [, second, , fourth] = [1, 2, 3, 4];

// destructuring objects
let o = { a: "foo", b: 12, c: "bar" } // new object o
let { a, b } = o;
```
### Array spreading
```typescript
// spread variables
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
// bothPlus == [0, 1, 2, 3, 4, 5]

// spread properties
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };
//                     ^-----<------/
//        properties on the left are overwritten
// search == { food: "rich", price: "$$", ambiance: "noisy" }
```

> Note: Methods of the objects are not spreading to other objects.

### Variables/properties operations
```typescript
//swap variables
[first, second] = [second, first];

// properties renaming
let { a: newName1, b: newName2 } = o;
```

## Enums

```typescript
enum Color {Red, Green, Blue};
// enum Color {Red = 1, Green, Blue}; // can be overwritten
let c: Color = Color.Green;

let colorName: string = Color[2]; // get color name
// colorName == "Blue"
```

## Interfaces

```typescript
interface Skeleton {
    // property declarations
    requiredProperty: type;
    optionalProperty?: type;
    readonly roProperty: type;
    [propName: type]: any;

    // indexable types
    []

    // method declarations
    (param1: type1, param2: type2): returnType
    // ^--------------^----- do not need to match
}
```

## Classes

```ts
class Person {
    fullName: string;
    constructor(public firstName, public lastName) {
        this.fullName = firstName + " " + lastName;
    }
}

var user = new Person("Jane", "User");
```