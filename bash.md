# Template

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreateDate: 2017-11
* @Category: Language
* @BasedOn: [HOWTO][basedon]

[basedon]: http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html

## Overview

<!-- TOC -->

- [Overview](#overview)
- [Redirections](#redirections)
  - [Descriptors](#descriptors)
  - [Operators](#operators)
  - [Pipe](#pipe)
- [Variables](#variables)
- [Conditionals](#conditionals)
  - [`if`](#if)
  - [`select`](#select)
- [Loops](#loops)
  - [`for` loop](#for-loop)
  - [`while` loop](#while-loop)
  - [`until` loop](#until-loop)
- [Functions](#functions)
- [Read input](#read-input)
- [Write](#write)
- [Return value](#return-value)
- [Arithmetic](#arithmetic)
  - [Operators](#operators-1)
- [Comparison](#comparison)
  - [Integer](#integer)
  - [String](#string)
- [Commands](#commands)

<!-- /TOC -->

## Redirections

### Descriptors

Index | Name | Description
--- | --- | ---
0 | stdin | Standard input
1 | stdout | Standard output
2 | stderr | Standard error

### Operators

Operator | Syntax | Description
--- | --- | ---
`<` | `[n]<file` | Redirect input; n defaults to 0 to `file`
`>` | `[n]>&m|file` | Redirect output; n defaults to 1 to `m` or `file`
`>>` | `[n]>>file` | Apend output to `file`
`&>` or `>&` or `> 2>&1` | `[n]&>&m|file` or `[n]>&&m|file` or `[n]>file 2>&1` | Redirect stdout and stderr to `m` or `file`

> Note: `&` is necessary when using descriptor on the right side of
> operator cause of interpreter would read number as filename.

> Note: There are more operators nevertheless they're are less common.

### Pipe

`command1 | command2`

> Note: Pipe is used to redirect output of the first command to input of
> the second one.

## Variables

> Note: Variables have no data types.

```bash
# Define variable
MYVAR="Hello" # Cannot contain spaces

# Use variable
echo $MYVAR

# Local varriable 
HELLO="Hello"
function hello {
  local HELLO="World"
  echo $HELLO
}
echo $HELLO # "Hello"
hello # "World"
echo $HELLO # "Hello"
```

## Conditionals

### `if`
```bash
if [ expression ]; then
  statement1
  statement2
fi

if [ expression ]; then
  statement1
else
  statement2
fi

if [ expression1 ]; then
  statement1
else if [ expression2 ]; then
  statement2
else
  statement3
fi
```

### `select`
```bash
OPTIONS="Hello Quit"
select opt in $OPTIONS; do
  if [ "$opt" = "Quit" ]; then
  echo done
  exit
  elif [ "$opt" = "Hello" ]; then
  echo Hello World
  else
  clear
  echo bad option
  fi
done
```

## Loops

### `for` loop
```bash
for i in expression; do
  statement
done
```

### `while` loop
```bash
while [ expression ]; do
  statement # repeat as long as expression is true
done
```

### `until` loop
```bash
until [ expression ]; do
  statement # repeat as long as expression is false
done
```

## Functions
```bash
function myfun {
  echo "Hello"
}

function otherfun {
  echo $1
}

myfun # "Hello"
otherfun "World" # "World"
```

## Read input
```bash
echo Please, enter your firstname and lastname
read FN LN 
echo "Hi! $LN, $FN !"
```

## Write
```bash
echo 1 + 1 # 1 + 1
echo $((1 + 1)) # 2
echo $[1 + 1] # 2
```

## Return value
```bash
cd /dada &> /dev/null
echo $?
```

## Arithmetic

### Operators

Operator | Description
--- | ---
`+` | Add
`-` | Substract
`*` | Multiply
`/` | Divide
`%` | Remaind

## Comparison

> Note: Spaces around an operator are important!

> Note: Additional `""` prevents syntax error when variable is null.

### Integer

Operator | Syntax | Description
--- | --- | ---
`-eq` | `[ "$A" -eq "$A" ]` | Equal
`-ne` | `[ "$A" -ne "$A" ]` | Not equal
`-gt` | `[ "$A" -gt "$A" ]` | Greater than
`-ge` | `[ "$A" -ge "$A" ]` | Greater than or equal
`-lt` | `[ "$A" -lt "$A" ]` | Less than
`-le` | `[ "$A" -le "$A" ]` | Less than or equal
`<` | `(("$A" < "$B"))` | Less than
`<=` | `(("$A" <= "$B"))` | Less than ot equal
`>` | `(("$A" > "$B"))` | Greater than
`>=` | `(("$A" >= "$B"))` | Greater than or equal

### String

> Note: Using `[[ ]]` instead of `[ ]` may prevent many logic errors when
> using with operators.

Operator | Syntax | Description
--- | --- | ---
`=` or `==` | `[ "$A" = "$B" ]` | Equal
`!=` | `[ "$A" != "$B" ]` | Not equal
`<` | `[[ "$A" < "$B" ]]` or `[ "$A" \< "$B" ]` | Less than (ASCII)
`>` | `[[ "$A" > "$B" ]]` or `[ "$A" \> "$B" ]` | Greater than (ASCII)
`-z` | `[ -z "$A" ]` | Empty string (length == 0)
`-n` | `[ -n "$A" ]` | Not empty (length > 0)

## Commands

Command | Description
--- | ---
`sed` | Stream editor
`awk` | Data/text processing
`grep` | Filtering lines
`wc` | Counter
`sort` | Sorting lines