---
title: "Week 4: Libraries"
draft: false
weight: 6
date: 2024-07-13
description: This is the fourth class of the CS50's Python course.
summary: This week introduces the concept of libraries and modules in Python, explaining how to import and use them, along with mentioning popular libraries for statistical analysis and file handling.
---

## Libraries

A piece of code that someone else wrote that you can use in your code.

## Modules

Is a library that has one or more functions built into it.

Re-usability code. 

### random

random is a built-in module in Python. It has a set of functions to generate random numbers.

[Documentation](https://docs.python.org/3/library/random.html)

## import

To use a module, you have to import it.

```python
import random

coin = random.choice(["head", "tails"])
print(coin)
```

### from

Is the keyword to import a specific function from a module.

```python
from random import choice

coin = choice(["head", "tails"])
print(coin)
```

### randint, shuffle

#### randint

```python
import random

number = random.randint(1, 10)
print(number)
```

#### shuffle

```python
import random

cards = ["jack", "queen", "king"]
random.shuffle(cards)
for card in cards:
    print(card)
```

## statistics

statistics is a built-in module in Python. It has a set of functions to calculate statistics.

[Documentation](https://docs.python.org/3/library/statistics.html)

```python
import statistics

print(statistics.mean([100, 90]))
```

## Command-line Arguments, sys

sys module, provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter.

[Documentation](https://docs.python.org/3/library/sys.html)

- sys.argv: argument vector, a list of strings representing the arguments.

```python
import sys

if len(sys.argv) < 2:
    print("Too few arguments")
elif len(sys.argv) > 2:
    print("Too many arguments")
else:
    print("hello, my name is", sys.argv[1])
```

### sys.exit

Exit from Python.

```python
import sys

if len(sys.argv) < 2:
    sys.exit("Too few arguments")
elif len(sys.argv) > 2:
    print("Too many arguments")

print("hello, my name is", sys.argv[1])
```

## slices

A slice is a portion of a list.

```python
import sys

if len(sys.argv) < 2:
    sys.exit("Too few arguments")

for arg in sys.argv[1:]:
    print("hello, my name is", arg)
```

## Packages, PyPI, pip

- Package: is a collection of modules.
- [PyPI](pypi.org): Python Package Index, is a repository of software for the Python programming language.
- pip: is a package installer for Python.

### cowsay 

[Documentation](https://pypi.org/project/cowsay/)

#### Install

```bash
pip install cowsay
```

#### Usage

```python
import cowsay
import sys

if len(sys.arg) == 2:
    cowsay.cow("hello, " + sys.argv[1])
```

### APIs, requests, JSON

- API: Application Programming Interface.
- [requests](pypi.org/project/requests): is a simple HTTP library for Python.
- [JSON](https://docs.python.org/3/library/json.html): JavaScript Object Notation, a language-independent data format.

#### Pretty print JSON

```python
import json
import requests
import sys

if len(sys.argv) != 2:
    sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=1&term=" + sys.argv[1])
print(json.dumps(response.json(), indent=2))
```

#### Printing the track name from the API

```python
import json
import requests
import sys

if len(sys.argv) != 2:
    sys.exit()

response = requests.get("https://itunes.apple.com/search?entity=song&limit=50&term=" + sys.argv[1])

o = response.json()
for result in o["results"]:
    print(result["trackName"]) 
```

## Custom Libraries

Create your own library.

### sayings.py

```python
def main():
    hello("world")
    goodbye("world")


def hello(name):
    print(f"hello, {name}")


def goodbye(name):
    print(f"goodbye, {name}")


if __name__ == "__main__":
    main()
```

### say.py

```python
import sys

from sayings import hello

if len(sys.argv) == 2:
    hello(sys.argv[1])
```
