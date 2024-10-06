---
title: "Week 3: Exceptions"
draft: false
weight: 7
date: 2024-07-10
description: This is the third class of the CS50's Python course.
summary: This week focuses on error management in Python, detailing different types of exceptions and methods to handle them, ensuring robust and error-free code execution.
---

## Exceptions

That means that something went wrong in the program. It is an error that happens during the execution of the program.

## Syntax Error

This is just and introductory example. The error is in the syntax of the code. It is a mistake in the code that the python interpreter can not execute.

```python
print("Hello World)
```

This error is a error that you need to fix, you can't create a code to handle this error. 

## ValueError

This error happens when you try to convert a string to a number, but the string is not a number.

```python 
x = int(input("What's x? "))
print(f"x is {x}")
```

This programs works fine if you input a number, but if you input a string, it will raise a ValueError. 

## try, except

You can handle exceptions with the try and except blocks. 

```python
try:
    x = int(input("What's x? "))
    print(f"x is {x}")
except ValueError:
    print("x is not an integer")
```

## NameError

This error happens when you try to use a variable that is not defined. 

```python
try:
    x = int(input("What's x? "))
except ValueError:
    print("x is not an integer")

print(f"x is {x}")
```

## else

You can use the else block to run a code if the try block does not raise an exception. 

```python
try:
    x = int(input("What's x? "))
except ValueError:
    print("x is not an integer")
else:
    print(f"x is {x}")
```

## Reprompting, break

You can use a while loop to reprompt the user if the input is not valid. 

```python
while True:
    try:
        x = int(input("What's x? "))
    except ValueError:
        print("x is not an integer")
    else:
        break

print(f"x is {x}")
```

## get_int

You can create a function to get an integer from the user. 

```python
def main():
    x = get_int()
    print(f"x is {x}")

def get_int():
    while True:
        try:
            return x = int(input("What's x? "))
        except ValueError:
            print("x is not an integer")

main()
```

## pass

You can use the pass statement to do nothing. 

```python
def main():
    x = get_int()
    print(f"x is {x}")

def get_int():
    while True:
        try:
            return x = int(input("What's x? "))
        except ValueError:
            pass

main()
```

*Note: In this case I wouln't use the pass argument, I think as a user would be weird to just be asked again and again for the same input.*

## function arguments

This is a refined version of the get_int function. 

```python
def main():
    x = get_int("What's x? ")
    print(f"x is {x}")

def get_int(prompt):
    while True:
        try:
            return x = int(input(prompt))
        except ValueError:
            pass

main()
```

## raise

This was just a quick mention of the raise statement.
