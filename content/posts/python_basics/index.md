---
title: "Python Quick Guide"
draft: false
date: 2024-10-04
description: This is a really small and compact tutorial of Python, this is just a testfile to try code-related .md features. 
summary: "This is another test post in which I give a really simple and brief python guide"
---

## 1. Variables and Data Types

In Python, variables are declared by simply assigning them a value:

```python
name = "Alice"  # String
age = 25        # Integer
height = 1.65   # Float
is_student = True  # Boolean
```

## 2. Control Structures

### Conditionals

```python
if age >= 18:
    print("You are an adult")
elif age >= 13:
    print("You are a teenager")
else:
    print("You are a child")
```

### Loops

#### For Loop

```python
for i in range(5):
    print(i)  # Prints 0 to 4
```

#### While Loop

```python
counter = 0
while counter < 5:
    print(counter)
    counter += 1
```

## 3. Functions

Defining and using functions:

```python
def greet(name):
    return f"Hello, {name}!"

message = greet("John")
print(message)  # Prints: Hello, John!
```

## 4. Lists and Dictionaries

### Lists

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("date")
print(fruits[1])  # Prints: banana
```

### Dictionaries

```python
person = {
    "name": "Charles",
    "age": 30,
    "city": "New York"
}
print(person["city"])  # Prints: New York
```

## 5. Modules

Importing and using modules:

```python
import random

number = random.randint(1, 10)
print(f"Random number: {number}")
```

## 6. Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Error: Division by zero")
finally:
    print("Operation completed")
```

## 7. List Comprehensions

```python
squares = [x**2 for x in range(5)]
print(squares)  # Prints: [0, 1, 4, 9, 16]
```

---

**Note**: This guide covers the basics of Python. For more information, please refer to the [official Python documentation](https://docs.python.org/).
