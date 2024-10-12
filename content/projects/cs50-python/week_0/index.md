---
title: "Week 0: Functions, Variables"
draft: false
weight: 10
date: 2024-04-18
description: This is the very first class of the CS50's Python course.
summary: This week covers fundamental programming concepts including functions, data types, and debugging techniques, providing a foundational understanding for writing and troubleshooting code.
---

## Hello Bison in Python
```python
print("Hello Bison!")
```

 ## Functions

- We just used the `print` function.

- Argument: value passed to a function.

- Side effects: printing to the console.

## Bugs and Debugging

- Bugs: mistakes in the code.

- Debugging: finding and fixing bugs.  

## Return values and Variables

- Return values: values returned by functions.

- Variables: store values for later use.

## Comments and Pseudocode

- Comments: notes to self and others.

- Pseudocode: planning code before writing it.

## Multiple function arguments

- String: a sequence of characters.

- Concateation: combining strings.

### Table of Data Types

| Data Type   | Description                                       |
|-------------|---------------------------------------------------|
| `int`       | Integer numbers (e.g., 5, -3, 100)                |
| `float`     | Floating point numbers (e.g., 3.14, -0.001, 2.0)  |
| `complex`   | Complex numbers (e.g., 3 + 4j, -2.5 + 0.1j)       |
| `str`       | String (e.g., "hello", 'world', "123")            |
| `list`      | List (e.g., [1, 2, 3], ['a', 'b', 'c'])           |
| `tuple`     | Tuple (e.g., (1, 2, 3), ('a', 'b', 'c'))          |
| `set`       | Set (e.g., {1, 2, 3}, {'a', 'b', 'c'})            |
| `dict`      | Dictionary (e.g., {'key': 'value'}, {1: 'one', 2: 'two'}) |
| `bool`      | Boolean (True or False)                           |
| `bytes`     | Immutable bytes sequence (e.g., b'hello', b'\x00\x01\x02') |

## Named Parameters 

### Documentation for print function

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

- *objects: zero or more objects to print.
- sep: how to separate objects.
- end: what to print at the end.
- file: where to print.
- flush: whether to forcibly flush the stream.

### Parameters vs Arguments

- Parameters: variables in the function definition.
- Arguments: values passed to the function.

### Small pieace of code to demonstrate how to change the end parameter behavior

```python
print("Hello ", end="")
print("Bison!")
```
The expected output is `Hello Bison!`.

### Named parameters vs Positional parameters

- Named parameters: they are optional and can be passed in any order.
- Positional parameters: they are required and must be passed in the correct order.

## Escaping Characters

- Escape character: backslash (\).

## f-strings

- f-string: formatted string literal.

### Example of code using f-strings

```python
name = "Bison"
print(f"Hello, {name}!")
```
The expected output is `Hello, Bison!`.

## String Methods

- .strip(): remove whitespace.

- .capitalize(): capitalize the first letter.

- .title(): capitalize the first letter of each word.

- .lstrip(): remove whitespace from the left.

- .rstrip(): remove whitespace from the right.

### Example of code using .strip() and .title()

```python
name = input("What's your name? ").strip().title()

print(f"Hello, {name}!")
```

## Style 

- Style: how code looks and is organized.

- PEP 8: Python Enhancement Proposal 8.

## split 

- .split(): split a string into a list.

### Example of code using .split()

```python
names = input("Enter names separated by commas: ").split(", ")
print(names)
```
Expected output: `['Alice', 'Bob', 'Charlie']`.

## Integers and Operators

- Integer: whole numbers.

- Operators: symbols that perform operations.

### Table of Operators

| Operator | Name           | Description                        |
|----------|----------------|------------------------------------|
| +        | Addition       | Adds two numbers.                  |
| -        | Subtraction    | Subtracts two numbers.             |
| *        | Multiplication | Multiplies two numbers.            |
| /        | Division       | Divides two numbers.               |
| //       | Floor division | Divides two numbers and rounds down. |
| %        | Modulus        | Returns the remainder of the division. |
| **       | Exponentiation | Raises a number to the power of another. |

### Interactive mode 

The interactive mode is a way to run Python code line by line.

## Calculator.py

```python
x = input("What's x? ")
y = input("What's y? ")

z = x + y
print(z)
```

## Type Conversion

- Type conversion: converting one data type to another.

- int(): convert to integer.

### Example of code using int()

```python
x = int(input("What's x? "))
y = int(input("What's y? "))

print(x + y)
```

## Foating Point Values

- Floating point values: decimal numbers.

- float(): convert to floating point.

### Example of code using float()

```python
x = float(input("What's x? "))
y = float(input("What's y? "))

print(x + y)
```

### Rounding Numbers

- round(): round a number to a specified number of decimal places.

```python
round(number[, ndigits])
```
#### Example of code using round()

```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = round(x + y)

print(z)
```

## Numeric Formatting

- f-string: formatted string literal.


### Example of code using f-string to format a number

```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = round(x + y)

print(f"{z:,}")
```

## Division 

- /: division.

### Example of code using / and //

```python
x = float(input("What's x? "))
y = float(input("What's y? "))

z = x / y

print(f"{z:.2f}")
```

## Defining Functions

- def: define a function.

### Example of code defining a function

```python
def main():
    name = input("What's your name? ")
    hello(name)


def hello(to="Bison"):
    print("Hello ", to)


main()
```

## Scope 

- Scope: where a variable is accessible.

## Return Values

- return: return a value from a function.

### Example of code using return

```python
def main():
    x = int(input("What's x? "))
    print("x squared is", square(x))

def square(n):
    return pow(n, 2)

main()
```
