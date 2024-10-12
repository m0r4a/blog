---
title: "Week 7: Regular Expressions"
draft: false
weight: 3
date: 2024-07-26
description: This is the seventh class of the CS50's Python course.
summary: This week explores regular expressions as powerful tools for string matching and validation, detailing how to use them effectively within Python programs.
---

## Regular Expressions

Know as a regex is just a pattern that we can use to match strings.
It is a powerful tool that allows us to search for strings that match a certain pattern.

## Validation with Regular Expressions

```python
email = input("Whats your email? ").strip()

username, domain = email.split("@")

if username and domain.ends with(".edu"):
    print("Valid")
else:
    print("Invalid")
```

## re Library

This library let us define a pattern that we can use to match strings.

[Documentation](https://docs.python.org/3/library/re.html)

- re.search(pattern, string, flags=0)

```python
import re

email = input("Whats your email? ").strip()

if re.search("@", email):
    print("Valid")
else:
    print("Invalid")
```

### Regular Expressions Patterns

#### Symbols

| Symbol        | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `.`           | Matches any character except a newline.                                     |
| `^`           | Matches the start of the string.                                            |
| `$`           | Matches the end of the string.                                              |
| `*`           | Matches 0 or more repetitions of the preceding pattern.                     |
| `+`           | Matches 1 or more repetitions of the preceding pattern.                     |
| `?`           | Matches 0 or 1 repetition of the preceding pattern.                         |
| `{n}`         | Matches exactly n repetitions of the preceding pattern.                     |
| `{n,}`        | Matches n or more repetitions of the preceding pattern.                     |
| `{n,m}`       | Matches between n and m repetitions of the preceding pattern.               |
| `[]`          | Matches any one of the characters inside the brackets.                      |
| `[^]`         | Matches any character not inside the brackets.                              |
| `|`           | Matches either the pattern before or the pattern after the pipe.            |
| `()`          | Groups patterns and captures the matched text.                              |
| `(?:...)`     | Groups patterns without capturing the matched text.                        |
| `\`           | Escapes special characters or denotes a special sequence.                   |
| `\d`          | Matches any digit; equivalent to `[0-9]`.                                   |
| `\D`          | Matches any non-digit; equivalent to `[^0-9]`.                              |
| `\w`          | Matches any word character (alphanumeric plus underscore); equivalent to `[a-zA-Z0-9_]`. |
| `\W`          | Matches any non-word character; equivalent to `[^a-zA-Z0-9_]`.              |
| `\s`          | Matches any whitespace character (spaces, tabs, newlines).                  |
| `\S`          | Matches any non-whitespace character.                                       |
| `\b`          | Matches a word boundary.                                                    |
| `\B`          | Matches a non-word boundary.                                                |

#### Code using Regular Expression Patterns

```python
import re

email = input("Whats your email? ").strip()

if re.search(r".+@.+\.edu", email):
    print("Valid")
else:
    print("Invalid")
```

#### Matching Start and End

- `^` Matches the start of the string.
- `$` Matches the end of the string.

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^.+@.+\.edu$", email):
    print("Valid")
else:
    print("Invalid")
```

#### Sets of Characters

- `[]` Matches any one of the characters inside the brackets.
- `[^]` Matches any character not inside the brackets.

##### 1. `[^@]+`

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^[^@]+@[^@]+\.edu$", email):
    print("Valid")
else:
    print("Invalid")
```

##### 2. `[a-zA-Z0-9_]+`

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^[a-zA-Z0-9_]+@[a-zA-Z0-9_]+\.edu$", email):
    print("Valid")
else:
    print("Invalid")
```

#### Character Classes

- `\d` Matches any **digit**; equivalent to `[0-9]`.
- `\D` Matches any _non-digit_; equivalent to `[^0-9]`.
- `/s` Matches any **whitespace** character (spaces, tabs, newlines).
- `\S` Matches any _non-whitespace_ character.
- `\w` Matches any **word** character (alphanumeric plus underscore); equivalent to `[a-zA-Z0-9_]`.
- `\W` Matches any _non-word_ character; equivalent to `[^a-zA-Z0-9_]`.

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^\w+@\w+\.edu$", email):
    print("Valid")
else:
    print("Invalid")
```

#### Flags

- `re.IGNORECASE` Makes the pattern case-insensitive.
- `re.MULTILINE` Makes the pattern match the start and end of each line.
- `re.DOTALL` Makes the `.` character match any character, including newlines.

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^\w+@\w+\.edu$", email, re.IGNORECASE):
    print("Valid")
else:
    print("Invalid")
```

#### Groups

- `A|B` Matches either the pattern before or the pattern after the pipe.
- `()` Groups patterns and captures the matched text.
- `(?:...)` Groups patterns without capturing the matched text.

```python
import re

email = input("Whats your email? ").strip()

if re.search(r"^(\w|\.)+@(\w+\.)?\w+\.edu$", email, re.IGNORECASE):
    print("Valid")
else:
    print("Invalid")
```

#### Email Address Validation

This is the regular expression pattern that the browsers uses to validate email addresses.

```text
^[a-zA-Z0-9.!#$%&'*+\/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$
```

#### match, fullmatch

- `re.match(pattern, string, flags=0)` Matches the pattern at the start of the string.
- `re.fullmatch(pattern, string, flags=0)` Matches the pattern against the whole string.

#### Capturing Groups

- When we use `()` we are creating a capturing group that allows us to extract the matched text.
- `:=` is the walrus operator that allows us to assign a value to a variable and use it in the same line.

```python
import re

name = input("Whats your name? ").strip()
if matches := re.search(r"^(.+), *(.+)$", name):
    name = matches.group(2) + " " + matches.group(1)

print(f"Hello, {name}")
```

#### Extracting from Strings

##### 1. `re.sub`

- `.re.sub(pattern, repl, string, count=0, flags=0)` Replaces the matched text with the replacement text.

```python
import re

url = input("URL: ").strip()

username = re.sub(r"^(https?://)?(www\.)?twitter\.com/", "", url)
print(f"Username: {username}")
```

##### 2. `re.search`

- `re.search(pattern, string, flags=0)` Searches for the pattern in the string.

```python
import re

url = input("URL: ").strip()

if matches := re.search(r"^https?://?(?:www\.)?twitter\.com/([a-z0-9_]+)", url, re.IGNORECASE)
    print(f"Username: {matches.group(1)}")
```

## Conclusion

There are other other functions

- `re.split(pattern, string, maxsplit=0, flags=0)` Splits the string at the matches of the pattern.
- `re.findall(pattern, string, flags=0)` Finds all the matches of the pattern in the string.
