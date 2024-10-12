---
title: "Week 6: File I/O"
draft: false
weight: 4
date: 2024-07-20
description: This is the sixth class of the CS50's Python course.
summary: This week covers file input/output operations, explaining how to read and write data, manage file formats like CSV, and manipulate data structures such as lists and dictionaries.
---

## File I/O

File I/O (input/output) is a way to read and write data to and from files. This is useful for saving data to a file, or reading data from a file.

## lists

Usually the data is stored in a list but the moment the program is closed, the data is lost. This is where file I/O comes in. It allows you to save the data to a file, and read it back in when the program is run again.

### Code example of storing data in a list

```python
names = []

for _ in range(3):
    names.append(input("What's your name? "))


for name in sorted(names):
    print(f"hello, {name}")
```

## open

The `open` function is used to open a file. It takes two arguments, the name of the file, and the mode to open the file in. The mode can be `r` for read, `w` for write, or `a` for append.

[Documentation](https://docs.python.org/3/library/functions.html#open)

### Code example of opening a file in write mode

```python
name = input("What's your name? ")

file = open("names.txt", "w")
file.write(name)
file.close()
```

### Code example of opening a file in append mode  

```python
name = input("What's your name? ")

file = open("names.txt", "a")
file.write(f"{name}\n")
file.close()
```

## with

The `with` statement is used to open a file and automatically close it when the block is done. This is useful because it ensures that the file is closed, even if an error occurs.

[Documentation](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement)

### Code example of using the with statement

```python
name = input("What's your name? ")

with open("names.txt", "a") as file:
    file.write(f"{name}\n")
```

## Reading from a file

To read from a file, you can use the `read` method to read the entire file, or the `readline` method to read one line at a time.

The value returned by the `read` method is a string, while the value returned by the `readline` method is a list of strings.

[Documentation](https://docs.python.org/3/tutorial/inputoutput.html#methods-of-file-objects)

### Code example of reading from a file

```python
with open("names.txt", "r") as file:
    for line in file:
        print("hello,", line.rstrip())

```

## sorted

The `sorted` function is used to sort a list. It takes a list as an argument, and returns a new list with the elements sorted.

[Documentation](https://docs.python.org/3/library/functions.html#sorted)

### 1. Code example of sorting a list (straightforward code)

```python
names - []

'''
When you want to open a file in read mode
you don't need to specify the mode because
it is the default mode.
'''
with open ("names.txt") as file:
    for line in file:
        names.append(line.rstrip())

for name in sorted(names):
    print(f"hello, {name}")
```

### 2. Code example of sorting a list (tighter code)

```python
with open("names.txt", "r") as file:
    for line in sorted(file):
        print("hello,", line.rstrip())
```

## Comma-Separated Values (CSV)

Comma-Separated Values (CSV) is a file format used to store tabular data. Each line in the file represents a row in the table, and the values are separated by commas.

The `csv` module in Python can be used to read and write CSV files.

[Documentation](https://docs.python.org/3/library/csv.html)

### CSV file example

```
Hermione,Gryffindor
Harry,Gryffindor
Ron,Gryffindor
Draco,Slytherin
```

### 1. Code example of reading from a CSV file without the csv module

```python
with open(sudents.csv) as file:
    for line in file:
        row = line.rstrip().split(",")
        print(f"{row[0]} is in {row[1]}")
```

### 2. Code example of reading from a CSV file without the csv module and using dictionaries

```python
students = []

with open(sudents.csv) as file:
    for line in file:
        name, house = line.rstrip().split(",")
        student = {"name": name, "house": house}
        students.append(student)

for student in students:
    print(f"{student['name']} is in {student['house']}")
```

## Sort keys

The `sorted` function can take a `key` argument to specify a function to use to extract a comparison key from each element in the list.

[Documentation](https://docs.python.org/3/library/functions.html#sorted)

### Code example of sorting a list of dictionaries by a key

```python
students = []

with open("students.csv") as file:
    for line in file:
        name, house = line.rstrip().split(",")
        student = {"name": name, "house": house}
        students.append(student)


def get_name(student):
    return student["name"]


for student in sorted(students, key=get_name):
    print(f"{student['name']} is in {student['house']}")
```

## Lambda functions

Lambda functions are small anonymous functions that can have any number of arguments, but only one expression.

[Documentation](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions)

### Code example of using a lambda function

```python
students = []

with open("students.csv") as file:
    for line in file:
        name, house = line.rstrip().split(",")
        student = {"name": name, "house": house}
        students.append(student)


for student in sorted(students, key=lambda student: student["name"]):
    print(f"{student['name']} is in {student['house']}")
```

## New CSV file example

```
Harry,Number Four, Privet Drive
Ron,The Burrow
Draco,Malfoy Manor
```

## CSV Library

The `csv` module in Python can be used to read and write CSV files. It provides a `DictReader` class to read CSV files as dictionaries, and a `DictWriter` class to write dictionaries to CSV files.

[Documentation](https://docs.python.org/3/library/csv.html)

### Code example of reading from a CSV file using the csv module: reader

```python
import csv

students = []

with open("students.csv") as file:
    reader = csv.reader(file)
    for name, home in reader:
        students.append({"name": name, "home": home})


for student in sorted(students, key=lambda student: student["name"]):
    print(f"{student['name']} is from {student['home']}")
```

### Code example of reading from a CSV file using the csv module: DictReader

#### New CSV file example

```
name,home
Harry,Number Four, Privet Drive
Ron,The Burrow
Draco,Malfoy Manor
```

#### Code

```python
import csv

students = []

with open("students.csv") as file:
    reader = csv.DictReader(file)
    for row in reader:
        sudents.append({"name": row["name"], "home": row["home"]})

for student in sorted(students, key=lambda student: student["name"]):
    print(f"{student['name']} is from {student['home']}")
```

### Code example of writing to a CSV file using the csv module: writer

#### In the CSV file

```
name,home
```

#### Code

```python
import csv

name = input("What's your name? ")
home = input("Where's your home? ")

with open("students.csv", "a") as file:
    writer = csv.writer(file)
    writer.writerow([name, home])
```

### Code example of writing to a CSV file using the csv module: DictWriter

#### Code

```python
import csv

name = input("What's your name? ")
home = input("Where's your home? ")

with open("students.csv", "a") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "home"])
    writer.writeheader() # This didn't appear in the video but is necessary to write the header
    writer.writerow({"name": name, "home": home})
```

## Images, PIL library

The Python Imaging Library (PIL) adds image processing capabilities to your Python interpreter. This library supports many file formats, and provides powerful image processing and graphics capabilities.

[Documentation](https://pillow.readthedocs.io/en/stable/)

### Code example of creating a simple gif

```python
import sys

from PIL import Image

images = []

for arg in sys.argv[1:]:
    image = Image.open(arg)
    images.append(image)

images[0].save(
        "costumes.gif", save_all=True, append_images=[images[1]], duration=200, loop=0
)
```
