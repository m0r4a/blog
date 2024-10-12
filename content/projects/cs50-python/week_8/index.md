---
title: "Week 8: Object-Oriented Programming"
draft: false
weight: 2
date: 2024-08-03
description: This is the eighth class of the CS50's Python course.
summary: This week outlines the principles of OOP, including classes, objects, and inheritance, emphasizing how these concepts facilitate code organization and reuse.
---

## Object-Oriented Programming (OOP)

Object-Oriented Programming (OOP) is a programming paradigm that uses "objects" to design applications and computer programs. It utilizes several techniques from previously established paradigms, including modularity, polymorphism, and encapsulation. OOP is based on the concept of "objects," which can contain data in the form of fields, often known as attributes, and code in the form of procedures, often known as methods.

### Tuples

A tuple is a collection of objects that are ordered and immutable. Tuples are sequences, just like lists. The differences between tuples and lists are, the tuples cannot be changed unlike lists and tuples use parentheses, whereas lists use square brackets.

```python
def main():
  student = get_student()
  print(f"{name} from {house}")


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return name, house


if __name__ == "__main__":
  main()
```

### Dictionaries

A dictionary is a little bit more powerful than a list. It is a collection of key-value pairs. Dictionaries are used to store data values in key:value pairs.

```python
def main():
  student = get_student()
  if student["name"] == "Padma":
    student["house"] = "Ravenclaw"
  print(f"{student['name']} from {student['house']}")


def get_student():
  return student = {
    "name": input("Name: "),
    "house": input("House: ")
  }


if __name__ == "__main__":
  main()
```

### Classes and Objects

- A `class` is a blueprint or a mold for creating objects. 

- A `class` is a user-defined blueprint or prototype from which objects are created. 

- An `object` is an instance of a class that has attributes and methods.


[Documentation](https://docs.python.org/3/tutorial/classes.html)

#### Simple use of a class

```python
class Student:
  ...


def main():
  student = get_student()
  print(f"{student.name} from {student.house}")


def get_student():
  student = Student()
  student.name = input("Name: ")
  student.house = input("House: ")
  return student


if __name__ == "__main__":
  main()
```

### Instance Methods

#### Table of methods

| Method         | Description                                                                |
|----------------|----------------------------------------------------------------------------|
| `__init__()`   | Constructor method, called when a new instance is created.                 |
| `__del__()`    | Destructor method, called when an instance is about to be destroyed.       |
| `__repr__()`   | Returns an official string representation of the instance, useful for debugging. |
| `__str__()`    | Returns a readable string representation, used by `print()`.               |
| `__call__()`   | Allows an instance to be called as a function.                             |
| `__eq__()`     | Defines behavior for the equality operator `==`.                           |
| `__ne__()`     | Defines behavior for the inequality operator `!=`.                         |
| `__lt__()`     | Defines behavior for the less-than operator `<`.                           |
| `__le__()`     | Defines behavior for the less-than-or-equal-to operator `<=`.              |
| `__gt__()`     | Defines behavior for the greater-than operator `>`.                        |
| `__ge__()`     | Defines behavior for the greater-than-or-equal-to operator `>=`.           |
| `__len__()`    | Defines behavior for the built-in `len()` function.                        |
| `__getitem__()`| Defines behavior for indexing `obj[key]`.                                  |
| `__setitem__()`| Defines behavior for assigning to indexed elements `obj[key] = value`.     |
| `__delitem__()`| Defines behavior for deleting indexed elements `del obj[key]`.             |
| `__iter__()`   | Defines behavior for the iterator protocol.                                |
| `__next__()`   | Defines behavior for retrieving the next item from an iterator.            |
| `__contains__()`| Defines behavior for the membership test operators `in` and `not in`.     |
| `__enter__()`  | Defines behavior for entering a context (used with `with` statement).      |
| `__exit__()`   | Defines behavior for exiting a context (used with `with` statement), handles exceptions. |
| `__getattr__()`| Defines behavior for accessing an attribute that does not exist.           |
| `__setattr__()`| Defines behavior for setting an attribute's value.                         |
| `__delattr__()`| Defines behavior for deleting an attribute.                                |
| `__hash__()`   | Defines behavior for the built-in `hash()` function.                       |
| `__eq__()`     | Defines behavior for the equality operator `==`.                           |
| `__ne__()`     | Defines behavior for the inequality operator `!=`.                         |

#### The Constructor Method: `__init__`

- The `__init__` method is a special method in Python classes that is called when a new instance of the class is created.

```python
class Student:
  def __init__(self, name, house):
    if not name:
      raise ValueError("Missing name")
    if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
      raise ValueError("Invalid house")
    self.name = name
    self.house = house


def main():
  student = get_student()
  print(f"{student.name} from {student.house}")


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return Student(name, house)  #Constructor call


if __name__ == "__main__":
  main()
```

#### The String Method: `__str__`

- The `__str__` method is called by the `str()` built-in function and by the `print()` function to compute the "informal" or nicely printable string representation of an object.

```python
class Student:
  def __init__(self, name, house):
    if not name:
      raise ValueError("Missing name")
    if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
      raise ValueError("Invalid house")
    self.name = name
    self.house = house


  def __str__(self):
    return f"{self.name} from {self.house}"


def main():
  student = get_student()
  print(f"{student.name} from {student.house}")


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return Student(name, house)  #Constructor call


if __name__ == "__main__":
  main()
```

#### Custom Methods

```python
class Student:
  def __init__(self, name, house, patronus):
    if not name:
      raise ValueError("Missing name")
    if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
      raise ValueError("Invalid house")
    self.name = name
    self.house = house
    self.patronus = patronus


  def __str__(self):
    return f"{self.name} from {self.house}"


  def charm(self):
    match self.patronus:
      case "Stag":
        return "🐴"
      case "Otter":
        return "🦦"
      case "Jack Russell Terrier":
        return "🐶"
      case _:
        return "🦄"


def main():
  student = get_student()
  print("Expecto Patronum!")
  print(sudent.charm())


def get_student():
  name = input("Name: ")
  house = input("House: ")
  patronus = input("Patronus: ")
  return Student(name, house, patronus)  #Constructor call


if __name__ == "__main__":
  main()
```

### Properties, Getters, and Setters

- `Properties` are a special kind of attribute that can be accessed like an attribute, but are computed like a method.
- `@property` is a decorator that allows you to define a method that can be accessed like an attribute.
- `Getters` are methods that allow you to **access** the value of a property.
- `Setters` are methods that allow you to **change** the value of a property.

```python
class Student:
  def __init__(self, name, house):
    if not name:
      raise ValueError("Missing name")
    self.name = name
    self.house = house


  def __str__(self):
    return f"{self.name} from {self.house}"


  # Getter
  '''
  This is the getter method. This is the "function"
  that will be called when you try to get the value of the property.
  like this: print(student.house)
  '''
  @property
  def house(self):
    return self._house


  # Setter
  '''
  This is the setter method. This is the "function"
  that will be called when you try to set the value of the property.
  like this: student.house = "Gryffindor"
  '''
  @house.setter
  def house(self, house):
    if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
      raise ValueError("Invalid house")
    self._house = house


def main():
  student = get_student()
  student.house = "Number Four, Privet Drive"
  print(student)


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return Student(name, house)  #Constructor call


if __name__ == "__main__":
  main()
```

## Types and Classes

- All this time `int` was a class: `class int(x, base=10)`.
- The str has been a class all along: `class str(object='')`.
  - All the time we used `str.lower()` we have been taking an object of class str and calling the method lower on it.
  - `str.strip([chars])` is the same thing, a method of the str class.
- `list` is a class, everytime we created a list we were creating an object of the class list: `class list([iterable])`.
  - `list.append(x)` is a method of the list class.
- `dict` is a class, everytime we created a dictionary we were creating an object of the class dict: `class dict(**kwarg)`.

### A small example

```python
print(type(50))
print(type("Hello, World!"))
print(type([]))
print(type({}))
```

Output:

```
<class 'int'>
<class 'str'>
<class 'list'>
<class 'dict'>
```

## Class methods

Sometimes is not really necessary to associate a function with object of a class but rather with the class itself. 

Sometimes you want that the class have certain behaivor or certain functionality that is not related to the object itself but rather to the class. That means that no matter how is the object created, the class will have that functionality.

For that he got another decorator called `@classmethod`, we use this decorator to define a method that is associated with the class rather than the object.

### Sorting hat example

In this example we're gonna implement a sorting hat that will assign a house to a student.

```python
import random

class Hat:
  def __init__(self):
    self.houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]


  def sort(self, name):
    print(name, "is in", random.choice(self.houses))


hat = Hat()
hat.sort("Harry")
```

### Class method example

The code of above works but it's not really necessary to create an object of the class Hat to sort a student. 

And it has a feature/bug, you can create more than one hat, and that's not a functionality that we want. We could do something like this:

```python
hat1 = Hat()
hat2 = Hat()
hat3 = Hat()
```

In the world of harry potter the sorting hat is not an object that you can create, it's just one and only one hat that you put on the head of the student and it will sort the student.

We have been using `instance methods`: writing functions inside of classes that are automatically passed a reference to self, the current object, but sometimes you don't need that, sometimes it suffices to just know what the class is and assume that might not even be an object of that class.

So in this case we can use a class really as a container for data and/or functions that is somehow conceptually related to the class but not necessarily to the object. Here is where `@classmethod` comes in.



```python
import random

class Hat:

  # This is a list of houses that is shared by all the instances of the class
  houses = ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]


  @classmethod
  def sort(cls, name):   # We dont reference self, we reference cls now which is the class itself
    print(name, "is in", random.choice(cls.houses))


Hat.sort("Harry")
```

### Class method example 2: improving old code

#### This is the first version of `students.py`:

```python
class Student:
  def __init__(self, name, house):
    if not name:
      raise ValueError("Missing name")
    self.name = name
    self.house = house


  def __str__(self):
    return f"{self.name} from {self.house}"


  # Getter
  '''
  This is the getter method. This is the "function"
  that will be called when you try to get the value of the property.
  like this: print(student.house)
  '''
  @property
  def house(self):
    return self._house


  # Setter
  '''
  This is the setter method. This is the "function"
  that will be called when you try to set the value of the property.
  like this: student.house = "Gryffindor"
  '''
  @house.setter
  def house(self, house):
    if house not in ["Gryffindor", "Hufflepuff", "Ravenclaw", "Slytherin"]:
      raise ValueError("Invalid house")
    self._house = house


def main():
  student = get_student()
  student.house = "Number Four, Privet Drive"
  print(student)


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return Student(name, house)  #Constructor call


if __name__ == "__main__":
  main()
```

#### Let's do some clean up to focus on the important parts:

```python
class Student:
  def __init__(self, name, house):
    self.name = name
    self.house = house


  def __str__(self):
    return f"{self.name} from {self.house}"


def main():
  student = get_student()
  student.house = "Number Four, Privet Drive"


def get_student():
  name = input("Name: ")
  house = input("House: ")
  return Student(name, house)  #Constructor call


if __name__ == "__main__":
  main()
```

#### Let's improve the code using class methods

The original code wasn't bad, but might be a little weird in the long run to have a function related to the class as a separate function outside of the class such as `get_student()`.

So what we can do is to move that function inside of the class and make it a class method.

```python
class Student:
  def __init__(self, name, house):
    self.name = name
    self.house = house


  def __str__(self):
    return f"{self.name} from {self.house}"


  @classmethod
  def get(cls):
    name = input("Name: ")
    house = input("House: ")
    return cls(name, hosue)


def main():
  student = Student.get()
  print(student)


if __name__ == "__main__":
  main()
```

## Satic methods

`@staticmethod` is a decorator that allows you to define a method that does not operate on the instance of the class or the class itself.

Anyway this is a rabbit hole that the course will not go down, but it's good to know that it exists.

## Inheritance

Turns out, via OOP (Object Oriented Programming), there's an opportunity to design your classes in a heirarchical way , whereby you can have one class "inherit" from or borrow attributes that is metods or variables from another class if they are all have those in common.

### Tryign this concept: `wizard.py`

```python
class Wizard:
  def __init__(self, name):
    if not name:
      raise ValueError("Missing name")
    self.name = name

  ...


class Student(Wizard):
  def __init__(self, name, house):
    super().__init__(name) # Super have the habilitiy to call the constructor of the parent class
    self.house = house


  ...


class Professor(Wizard):
  def __init__(self, name, subject):
    super().__init__(name)
    self.subject = subject

    ...


wizard = Wizard("Albus")
student = Student("Harry", "Gryffindor")
professor = Professor("Severus", "Defense Against the Dark Arts")
```

### Exceptions hierarchy

```text
BaseException
  +-- KeyboardInterrupt
  +-- Exception
    +-- ArithmeticError
    |  +-- ZeroDivisionError
    +-- AssertionError
    +-- AttributeError
    +-- EOFError
    +-- ImportError
    |  +-- ModuleNotFoundError
    +-- LookupError
    |  +-- KeyError
    +-- NameError
    +-- SyntaxError
    |  +-- IndentationError
    +-- ValueError
```

## Operator Overloading: `vault.py`

Operator overloading is a specific case of polymorphism, where different operators have different implementations depending on their arguments.

In other words, a `+` doesn't always mean addition, it can mean concatenation if the operands are strings for example.

[Documentation](https://docs.python.org/3/reference/datamodel.html#special-method-names)

- `__add__` is a special method that is called when the `+` operator is used.

```python
class Vault:
  def __init__(self, galleons=0, sickles=0, knuts=0):
    self.galleons = galleons
    self.sickles = sickles
    self.knuts = knuts


  def __str__(self):
    return f"{self.galleons} galleons, {self.sickles} sickles, {self.knuts} knuts"


  def __add__(self, other):
    galleons = self.galleons + other.galleons
    sickles = self.sickles + other.sickles
    knuts = self.knuts + other.knuts
    return Vault(galleons, sickles, knuts)


potter = Vault(100, 50, 25)
print(potter)

weasley = Vault(25, 50, 100)
print(weasley)

total = Vault(galleons, sickles, knuts)
print(total)
```

