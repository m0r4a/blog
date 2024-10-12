---
title: "CS50-Python certification"
draft: false
weight: 10
date: 2024-08-14
description: My CS50-Python course notes
summary: Here you will find a short summary of the key concepts of each week of the CS50P course in addition to the posts on the detailed notes of each week.
---

## CS50’s Introduction to Programming with Python

### Github repository

[Here](https://github.com/m0r4a/CS50-python) you can check the Github repository used trough the course.

### Certificate 

[Here](https://certificates.cs50.io/1e3fea88-dbb4-48cf-a84f-d066a1df57bf.pdf?size=letter) you can see my certificate of the course.

### [Week 0: Functions, Variables](./week_0)

This week covers fundamental programming concepts including functions, data types, and debugging techniques, providing a foundational understanding for writing and troubleshooting code.

<details>
  <summary>Key concepts</summary>

| Concept             | Details                                      |
|---------------------|----------------------------------------------|
| `Functions`         | A block of code that performs a specific task.|
| `Bugs and Debugging`| Mistakes in the code and how to fix them.     |
| `Data Types`        | The type of data that a variable can store.   |
| `Named Parameters`  | Parameters that are passed by name.           |
| `String Methods`    | Methods that can be used with strings.        |
| `Integers and Operators` | Operators that can be used with integers.|
| `Type Conversion`   | Converting one data type to another.          |

</details>

### [Week 1: Conditionals](./week_1)

This week discusses control flow elements like conditionals and logical operators, which are essential for making decisions in code and controlling how it executes.

<details>
  <summary>Key concepts</summary>

| Concept               | Details                                                   |
|-----------------------|-----------------------------------------------------------|
| `Comparison Operators`| Operators that compare two values.                        |
| `if`                  | A way to run code conditionally.                          |
| `elif`                | A way to run code conditionally if the first condition is false. |
| `else`                | A way to run code if all other conditions are false.       |
| `or`                  | A way to combine conditions.                              |
| `not equal`           | A way to check if two values are not equal.               |
| `and`                 | A way to combine conditions.                              |
| `chains`              | A way to combine multiple conditions.                     |
| `modulo`              | A way to get the remainder of a division.                 |
| `boolean`             | A way to represent true or false values.                  |
| `pythonic expressions`| A way to write code in a more concise way.                |
| `match`               | A way to match a value to a pattern.                      |

</details>

### [Week 2: Loops](./week_2)

This week focuses on loops in programming, detailing how to iterate over data structures using for and while loops, and discussing concepts such as nested loops and list iteration.

<details>
  <summary>Key concepts</summary>

| Concept              | Details                                                     |
|----------------------|-------------------------------------------------------------|
| `Loops`              | The ability of doing something multiple times.              |
| `while`              | A way to repeat a block of code while a condition is true.   |
| `for`                | A way to repeat a block of code a number of times.           |
| `Validating input`   | A way to ensure that the input is correct.                  |
| `Iteration with Lists`| A way to iterate over a list.                               |
| `len`                | A way to get the length of a list.                          |
| `Dictionaries`       | A way to store key-value pairs.                             |
| `List of Dictionaries`| A way to store a list of dictionaries.                     |
| `Nested Loops`       | A way to have a loop inside another loop.                   |

</details>

### [Week 3: Exceptions](./week_3)

This week focuses on error management in Python, detailing different types of exceptions and methods to handle them, ensuring robust and error-free code execution.

<details>
  <summary>Key concepts</summary>

| Concept               | Details                                                      |
|-----------------------|--------------------------------------------------------------|
| `Exceptions`          | A way to handle errors in the code.                         |
| `Syntax Error`        | A mistake in the code that the Python interpreter cannot execute. |
| `ValueError`          | An error that happens when you try to convert a string to a number, but the string is not a number. |
| `try, except`         | A way to handle exceptions.                                 |
| `NameError`           | An error that happens when you try to use a variable that is not defined. |
| `else`                | A way to run code if the try block does not raise an exception. |
| `Reprompting, break`  | A way to reprompt the user if the input is not valid.      |
| `get_int`            | A way to create a function to get an integer from the user. |
| `pass`                | A way to do nothing.                                       |
| `function arguments`  | A way to pass arguments to a function.                      |
| `raise`               | A way to raise an exception.                                |
</details>

### [Week 4: Libraries](./week_4)

This week introduces the concept of libraries and modules in Python, explaining how to import and use them, along with mentioning popular libraries for statistical analysis and file handling.

<details>
  <summary>Key concepts</summary>

| Concept                          | Details                                                                 |
|----------------------------------|-------------------------------------------------------------------------|
| `Libraries`                      | A piece of code that someone else wrote that you can use in your code. |
| `Modules`                        | A library that has one or more functions built into it.                |
| `import`                         | To use a module, you have to import it.                                |
| `from`                           | The keyword to import a specific function from a module.               |
| `statistics`                     | A built-in module in Python that has a set of functions to calculate statistics. |
| `Command-line Arguments, sys`    | The sys module provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter. |
| `Packages, PyPI, pip`            | Package: A collection of modules. PyPI: Python Package Index, a repository of software for Python. pip: a package installer for Python. |
| `Custom Libraries`               | Create your own library.                                               |
</details>

### [Week 5: Unit Tests](./week_5)

This week highlights the importance of testing in software development, discussing unit tests and the use of frameworks like pytest to ensure code quality and reliability.

<details>
  <summary>Key concepts</summary>

| Concept                    | Details                                                        |
|----------------------------|----------------------------------------------------------------|
| `Unit Tests`              | A way to test the code you wrote.                             |
| `assert`                   | A way to test the code you wrote.                             |
| `AssertionError`           | A way to handle an AssertionError.                            |
| `pytest`                   | A testing framework that makes it easy to write small tests.  |
| `Side Effects and Testing` | A way to test the code you wrote.                             |
| `Collection of Tests`      | A way to group tests together.                                |
</details>

### [Week 6: File I/O](./week_6)

This week covers file input/output operations, explaining how to read and write data, manage file formats like CSV, and manipulate data structures such as lists and dictionaries.

<details>
  <summary>Key concepts</summary>

| Concept                        | Details                                                            |
|--------------------------------|--------------------------------------------------------------------|
| `File I/O`                    | A way to read and write data to and from files.                   |
| `lists`                       | Data is stored in a list, but the moment the program is closed, the data is lost. |
| `open`                        | Used to open a file.                                              |
| `with`                        | Used to open a file and automatically close it when the block is done. |
| `Reading from a file`         | Use the `read` method to read the entire file, or `readline` to read one line at a time. |
| `sorted`                      | Used to sort a list.                                             |
| `Comma-Separated Values (CSV)` | A file format used to store tabular data.                        |
| `sort keys`                   | Used to sort a list of dictionaries by a key.                    |
| `Lambda Functions`            | A way to create small anonymous functions.                        |
| `CSV Library`                 | A library that can be used to read and write CSV files.          |
| `Images, PIL Library`         | A library that can be used to read and write images.             |
</details>

### [Week 7: Regular Expressions](./week_7)

This week explores regular expressions as powerful tools for string matching and validation, detailing how to use them effectively within Python programs.

<details>
  <summary>Key concepts</summary>

| Concept                           | Details                                                              |
|-----------------------------------|----------------------------------------------------------------------|
| `Regular Expressions`             | A pattern that we can use to match strings.                         |
| `Validation with Regular Expressions` | A way to validate strings using regular expressions.              |
| `re Library`                     | A library that allows us to define a pattern to match strings.      |
| `Regular Expressions Patterns`    | A set of symbols that can be used to match strings.                |
</details>

### [Week 8: Object-Oriented Programming](./week_8)

This week outlines the principles of OOP, including classes, objects, and inheritance, emphasizing how these concepts facilitate code organization and reuse.

<details>
  <summary>Key concepts</summary>

| Concept                          | Details                                                              |
|----------------------------------|----------------------------------------------------------------------|
| `Object-Oriented Programming (OOP)` | A programming paradigm that uses "objects" to design applications and computer programs. |
| `Tuples`                        | A collection of objects that are ordered and immutable.             |
| `Dictionaries`                  | A collection of key-value pairs that is more powerful than a list.  |
| `Classes and Objects`           | A class is a blueprint or a mold for creating objects.              |
| `Instance Methods`              | Functions defined inside a class used to perform operations on objects of that class. |
| `Types and Classes`             | A type is a category of values, and a class is a blueprint for creating objects. |
| `Class methods`                 | Methods that are bound to the class and not the object of the class. |
| `Static methods`                | Methods that are bound to the class and not the object of the class. |
| `Inheritance`                   | A way to create a new class that is based on an existing class.     |
| `Operator Overloading`          | A way to define how an operator behaves when used with a class.     |
</details>

### [Week 9: Et Cetera](./week_9)

This week presents advanced programming features like sets, global variables, type hints, and comprehensions, enhancing Python’s functionality and readability while promoting best practices.

<details>
  <summary>Key concepts</summary>

| Concept                          | Details                                                            |
|----------------------------------|--------------------------------------------------------------------|
| `set`                            | A collection of unique elements; an unordered collection of items. |
| `global`                         | Used to declare that a variable inside the function is global (outside the function). |
| `constants`                      | A type of variable whose value cannot be changed.                  |
| `Type Hints, mypy`              | A static type checker for Python.                                  |
| `Docstrings`                    | A string that appears right after the definition of a function, class, or module. |
| `argparse`                      | A module in the Python standard library that allows you to parse command-line arguments. |
| `unpacking`                      | A way to assign the elements of an iterable to multiple variables.  |
| `map`                           | A function that applies a given function to each item of an iterable (list, tuple, etc.). |
| `List Comprehensions`           | A way to create lists in Python.                                   |
| `filter`                         | A function that filters elements of an iterable based on a given function. |
| `Dictionary Comprehensions`     | A way to create dictionaries in Python.                            |
| `enumerate`                     | A function that adds a counter to an iterable.                     |
| `Generators, Iterators`   | A way to create iterators in Python.                               |
</details>

---

# Weeks in detail
