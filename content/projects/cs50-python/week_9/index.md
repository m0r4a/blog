---
title: "Week 9: Et Cetera"
draft: false
weight: 1
date: 2024-08-12
description: This is the class of the final project for the CS50's Python course.
summary: A set is a collection of unique elements. It is an unordered collection of items. Sets are used to store multiple items in a single variable. It is a collection data type in Python. 
---

## set

A set is a collection of unique elements. It is an unordered collection of items. Sets are used to store multiple items in a single variable. It is a collection data type in Python. 

[Doumentation](https://docs.python.org/3/library/stdtypes.html#set)

### Example without using `set`

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
    {"name": "Padma", "house": "Ravenclaw"},
]

houses = []
for student in students:
  if student["house"]  not in houses:
    houses.append(student["house"])


for house in sorted(houses):
  print(house)
```

### Example without re-inveting the wheel: using `set`

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
    {"name": "Padma", "house": "Ravenclaw"},
]

houses = set()
for student in students:
  houses.add(student["house"])

for house in sorted(houses):
  print(house)
```

## global

The global keyword is used to declare that a variable inside the function is global (outside the function). If you want to change a global variable inside a function, you can use the global keyword to declare which variables are global.

### Example where you use a variable that lives outside the function

```python
balance = 0


def main():
  print("Balance:", balance)


if __name__ == "__main__":
  main()
```

### Example of code that tries to change a global variable inside a function

```python
balance = 0


def main():
  print("Balance:", balance)
  deposit(100)
  withdraw(50)
  print("Balance:", balance)


def deposit(n):
  balance += n


def withdraw(n):
  balance -= n


if __name__ == "__main__":
  main()
```

The result is a `UnboundLocalError` because the variable `balance` is not defined inside the function `deposit`.

Apparently is okey to read a global variable inside a function, but if you want to change it, you need to use the `global` keyword.

### Example of code that changes a global variable inside a function

```python
balance = 0


def main():
  print("Balance:", balance)
  deposit(100)
  withdraw(50)
  print("Balance:", balance)


def deposit(n):
  global balance
  balance += n


def withdraw(n):
  global balance
  balance -= n


if __name__ == "__main__":
  main()
```

### Example of code with OOP

```python
class Account:
  def __init__(self):
    self._balance = 0

  @property
  def balance(self):
    return self._balance

  def deposit(self, n):
    self._balance += n

  def withdraw(self, n):
    self._balance -= n


def main():
  account = Account()
  print("Balance:", account.balance)
  account.deposit(100)
  account.withdraw(50)
  print("Balance:", account.balance)


if __name__ == "__main__":
  main()
```

Usually using global variables is not a good practice. It is better to use classes and objects.

_Note for myself: the instance variable `balance` and all the other instance variables by definition can be accessed by all the methods of the class._

## constants

A constant is a type of variable whose value cannot be changed.

### Example of code with "constants"

```python
MEOWS = 3

for _ in range(MEOWS):
  print("meow")

```

There's actually no way to define a constant in Python. The convention is to use uppercase letters for the variable name to indicate that it should be treated as a constant.

### Constants in OOP

```python
class Cat:
  MEOWS = 3

  def meow(self):
    for _ in range(Cat.MEOWS): # or self.MEOWS
      print("meow")


cat = Cat()
cat.meow()
```

## Type Hints, mypy

`mypy` is a static type checker for Python. It is a tool that can be used to check the types of variables and functions in your code.

[Documentation](https://mypy.readthedocs.io/en/stable/)

### Example of code where an error is detected by `mypy`

```python
def meow(n):
  for _ in range(n):
    print("meow")


number = input("Number: ")
meow(number)
```

MyPy will detect the error because the function `input` returns a string, and the function `meow` expects an integer.

### Example of code with type hints

```python
def meow(n: int):
  for _ in range(n):
    print("meow")


number: int = input("Number: ")
meow(number)
```

The code is still wrong, but now `mypy` can detect the error much quicker by adding type hints.

### Correct version of the code

```python
def meow(n: int):
  for _ in range(n):
    print("meow")


number: int = int(input("Number: "))
meow(number)
```

### Return type hints: error version

```python
def meow(n: int) -> None:
  for _ in range(n):
    print("meow")


number: int = int(input("Number: "))
meows: str = meow(number)
print(meows)
```

### Return type hints: correct version

```python
def meow(n: int) -> str:
  return "meow\n" * n


number: int = int(input("Number: "))
meows: str = meow(number)
print(meows, end="")
```

## Docstrings

A docstring is a string that is used to document a function, method, or class. It is used to describe what the function does, what parameters it takes, and what it returns.

There's a standarized way on how to document your functions, methods, and classes in Python, the PEP (Python Enhancement Proposal) is the [PEP 257](https://www.python.org/dev/peps/pep-0257/)

### Example of code with a docstring

```python
def meow(n: int) -> str:
  """
  Meow n times.

  :param n: Number of times to meow.
  :type n: int
  :raise TypeError: If n is not an int.
  :return: A string of n meows, one per line.
  :rtype: str
  """
  return "meow\n" * n


number: int = int(input("Number: "))
meows: str = meow(number)
print(meows, end="")
```

## argparse

The `argparse` module is used to parse command-line arguments in Python. It is a standard module that comes with Python.


[Documentation](https://docs.python.org/3/library/argparse.html)

### Example of code with `argparse`

```python
import argparse

parser = argparse.ArgumentParser(description="Meow like a cat.")
parser.add_argument("-n", default=1, help="number of times to meow", type=int)
args = parser.parse_args()

for _ in range(args.n):
  print("meow")
```

_Note: if you specify that the argument is a type `int`, you don't need to convert it to an integer._

## unpacking

Unpacking is the process of extracting values from a collection, such as a list or a tuple, and assigning them to variables.

### A very simple example of unpacking

```python
first, _ = input("What's your name? ").split(" ") # Here is the unpacking
print(f"hello, {first}")
```

We used `the foo, bar = "foo bar".split(" ")` to unpack the values of the list returned by the split method.

### Unpacking a list

```python
def total(galleons, sickles, knuts):
  return (galleons * 17 + sickles) * 29 + knuts

coins = [100, 50, 25]

print(total(*coins), "Knuts") # Here is the unpacking
```

We used the `*` operator to unpack the values of the list `coins` and pass them as arguments to the function `total`.

### Unpacking a dictionary

```python
def total(galleons, sickles, knuts):
  return (galleons * 17 + sickles) * 29 + knuts


coins = {"galleons": 100, "sickles": 50, "knuts": 25}

print(total(**coins), "Knuts") # Here is the unpacking
```

We used the `**` operator to unpack the values of the dictionary `coins` and pass them as arguments to the function `total`.

### `*args` and `**kwargs`

- `*args` is used to pass a variable number of arguments to a function.
- `**kwargs` is used to pass a variable number of keyword arguments to a function.

```python
def f_positional(*args, **kwargs):
  print("Positional:", args)


# The output of this function is: Positional: (100, 50, 25)
f_positional(100, 50, 25)


def f_keyword(*args, **kwargs):
  print("Keyword:", kwargs)


# The output of this function is: Keyword: {'galleons': 100, 'sickles': 50, 'knuts': 25}
f_keyword(galleons=100, sickles=50, knuts=25)
```

## map

The `map` function is used to apply a function to each item in a list or other iterable.

```python
map(function, iterable)
```

[Documentation](https://docs.python.org/3/library/functions.html#map)

### Example of code without using `map`

```python
def main():
  yell("This", "is", "CS50")


def yell(*words):
  uppercased = []
  for word in words:
    uppercased.append(word.upper())
  print(*uppercased)


if __name__ == "__main__":
  main()
```

### Example of code using `map`

```python
def main():
  yell("This", "is", "CS50")


def yell(*words):
  """
  We use str.upper instead of something.upper()
  because instead of actually applying the method
  to the string, we are just passing the method
  itself to the map function.
  """
  uppercased = map(str.upper, words)
  print(*uppercased)


if __name__ == "__main__":
  main()
```

## List Comprehensions

List comprehensions are a concise way to create lists in Python. They are used to create a new list by applying an expression to each item in an existing list.

### Example of code using a list comprehension instead of a `for` loop or `map`

```python
def main():
  yell("This", "is", "CS50")


def yell(*words):
  uppercased = [word.upper() for word in words]
  print(*uppercased)


if __name__ == "__main__":
  main()
```

## filter

The `filter` function is used to filter items from a list or other iterable.

```python
filter(function, iterable)
```

[Documentation](https://docs.python.org/3/library/functions.html#filter)

### Example of code without using `filter`

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
    {"name": "Padma", "house": "Ravenclaw"},
]

gryffindors = [
  student["name"] for student in students if student["house"] == "Gryffindor"
]

for gryffindor in sorted(gryffindors):
  print(gryffindor)
```

In the code above, we used a list comprehension with a conditional to filter the students that belong to the house Gryffindor.

### Example of code using `filter`

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
    {"name": "Padma", "house": "Ravenclaw"},
]


def is_gryffindor(s):
  return s["house"] == "Gryffindor"


gryffindors = filter(is_gryffindor, students)

for gryffindor in sorted(gryffindors, key=lambda s: s["name"]):
  print(gryffindor["name"])
```

## Dictionary Comprehensions

Dictionary comprehensions are a concise way to create dictionaries in Python. They are used to create a new dictionary by applying an expression to each item in an existing dictionary.

### Example of code not using a dictionary comprehension

```python
students = ["Hermonie", "Harry", "Ron"]

gryffindors = []

for student in students:
  gryffindors.append({"name": student, "house": "Gryffindor"})

print(gryffindors)
```

### Example of code using a dictionary comprehension

```python
students = ["Hermonie", "Harry", "Ron"]

gryffindors = {student: "Gryffindor" for student in students}

print(gryffindors)
```

## enumerate

The `enumerate` function is used to add a counter to an iterable.

```python
enumerate(iterable, start=0)
```

[Documentation](https://docs.python.org/3/library/functions.html#enumerate)

### Example of code without using `enumerate`

```python
students = ["Hermonie", "Harry", "Ron"]

for i in range(len(students)):
  print(i + 1, students[i])
```

### Example of code using `enumerate`

```python
students = ["Hermonie", "Harry", "Ron"]

for i, student in enumerate(students, start=1):
  print(i + 1, student)
```

## Generators, Iterators, yield

A generator is a function that returns an iterator. It generates values using the `yield` keyword.

[What's a generator?](https://docs.python.org/3/glossary.html#term-generator)

### Example of code that not works due the lack of using a generator

```python
def main():
  n = int(input("What's n? "))
  for i in range(n):
    print(sheep(i))


def sheep(n):
  flock = []
  for i in range(n):
    flock.append("🐑" * i)

  return flock


if __name__ == "__main__":
  main()
```

The problem in the code above is that the function `sheep` first generates all the values and then returns them all at once. This is not efficient because it uses a lot of memory.

### Example of code using a generator

```python
def main():
  n = int(input("What's n? "))
  for i in range(n):
    print(sheep(i))


def sheep(n):
  for i in range(n):
    yield "🐑" * i


if __name__ == "__main__":
  main()
```

The word `yield` is used to return a value at the time, that way we don't need to store all the values in memory but just one at a time.

`yeild` is returning an iterator, so we can use it in a `for` loop.
