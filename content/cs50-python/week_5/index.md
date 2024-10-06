---
title: "Week 5: Unit Tests"
draft: false
weight: 5
date: 2024-07-14
description: This is the fifth class of the CS50's Python course.
summary: This week highlights the importance of testing in software development, discussing unit tests and the use of frameworks like pytest to ensure code quality and reliability.
---

## Unit Tests

Is a way to test the code you wrote.

## Testing calculator.py

### Calculator.py code

```python
def main():
    x = int(input("What's x? "))
    print("x squared is", square(x))


def square(n):
    return n * n


if __name__ == "__main__":
    main()
```

### test_calculator.py code

```python
from calculator import square


def main():
    test_square()


def test_square():
    if square(2) != 4:
        print("2 squared is not 4")
    if square(3) != 9:
        print("3 squared is not 9")


if __name__ == "__main__":
    main()
```

## assert

_testing [this code](#calculatorpy-code)_

```python
def main():
    test_square()


def test_square():
    assert square(2) == 4
    assert square(3) == 9


if __name__ == "__main__":
    main()
```

## AssertionError

How to handle an AssertionError

### First "bad" try

_testing [this code](#calculatorpy-code)_

```python
def main():
    test_square()


def test_square():
    try:
        assert square(2) == 4
    except AssertionError:
        print("2 squared is not 4")
    try:
        assert square(3) == 9
    except AssertionError:
        print("3 squared is not 9")


if __name__ == "__main__":
    main()
```

### Second "bad" try with more examples

_testing [this code](#calculatorpy-code)_

```python
def main():
    test_square()


def test_square():
    try:
        assert square(2) == 4
    except AssertionError:
        print("2 squared is not 4")
    try:
        assert square(3) == 9
    except AssertionError:
        print("3 squared is not 9")
    try:
        assert square(-3) == 9
    except AssertionError:
        print("-3 squared is not 9")
    try:
        assert square(0) == 0
    except AssertionError:
        print("0 squared is not 0")


if __name__ == "__main__":
    main()
```

## pytest

### Installation

```bash
$ pip install pytest
```

### Documentation

[pytest documentation](https://docs.pytest.org/en/latest/)

### Same test with pytest and all the tests in one function

_testing [this code](#calculatorpy-code)_

```python
from calculator import square

def test_square():
    assert square(2) == 4
    assert square(3) == 9
    assert square(-2) == 4
    assert square(-3) == 9
    assert square(0) == 0
```

And then run the test with `pytest test_calculator.py`

```bash
$ pytest test_calculator.py
```

### Categories of tests

_testing [this code](#calculatorpy-code)_

```python
from calculator import square

def test_positive():
    assert square(2) == 4
    assert square(3) == 9


def test_negative():
    assert square(-2) == 4
    assert square(-3) == 9


def test_zero():
    assert square(0) == 0
```

### Testing for exceptions

_testing [this code](#calculatorpy-code)_

```python
import pytest

from calculator import square

def test_positive():
    assert square(2) == 4
    assert square(3) == 9


def test_negative():
    assert square(-2) == 4
    assert square(-3) == 9


def test_zero():
    assert square(0) == 0


def test_str():
    with pytest.raises(TypeError):
        square("cat")
```

## Side Effects and Testing

### hello.py code

```python
def main():
    name = input("What's your name? ")
    hello(name)


def hello(to="world"):
    print(f"hello, ", to)


if __name__ == "__main__":
    main()
```

### test_hello.py code

_testing [this code](#hellopy-code)_

```python
from hello import hello


def test_arguement():
    assert hello("David") == "hello, David"
```

- The test will fail because the function `hello` prints the message instead of returning it.

- Printing the message is a side effect.

- Is a good practice to avoid side effects in functions as much as possible so the function can be tested.

### New testable version of hello.py

```python
def main():
    name = input("What's your name? ")
    print(hello(name))


def hello(to="world"):
    return f"hello, {to}"


if __name__ == "__main__":
    main()
```

- This is a better version because the assert tests are meant to check the return value of the function and not the side effects.

### test_hello.py code

_testing [this code](#new-testable-version-of-hellopy)_

```python
from hello import hello


def test_default():
    assert hello() == "hello, world"


def test_arguement():
    for name in ["Hermione", "Harry", "Ron"]:
        assert hello(name) == f"hello, {name}"
```

## Collections of tests

With a structure like this:

```
project/
    hello.py
    test/
        __init__.py
        test_hello.py
```

### test_hello.py code

```python
from hello import hello

def test_default():
    assert hello() == "hello, world"


def test_arguement():
    assert hello("David") == "hello, David"
```

### __init__.py

Even if it's empty, `__init__.py`  have the effect of telling Python that the directory is not just a module, but a package.

### Running the tests

```bash
$ pytest test
```
