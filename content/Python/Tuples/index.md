---
title: "Tuples"
subtitle: ""
excerpt: "Covers tuples as a fixed, unchangeable alternative to lists useful for data that shouldn't be modified, such as coordinates or fixed groupings of values."
date: 2026-09-01
author: "Kelvin Kiprono"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- Python
---
**What Is a Tuple?**

The word tuple comes from mathematics, where it’s used to describe a finite ordered sequence of values.For example , (1,2,3) is a tuple containing three integers.

Tuples are **ordered** because their elements appear in an ordered fashion.

*How to Create a Tuple*

There are a few ways to create a tuple in Python. We’ll cover two of
them:
1. Tuple literals
2. The built-in tuple()

*Tuple Literals*

Just like a string literal is a string that is explicitly created by surrounding some text with quotes, a tuple literal is a tuple that is written out explicitly as a comma-separated list of values surrounded by parentheses.
Here’s an example of a tuple literal:

``` python
my_first_tuple = (1, 2, 3)
```
Unlike strings, which are sequences of characters, tuples may contain any type of value, including values of different types. The tuple (1,
2.0, "three") is perfectly valid.


``` python
my_next_tuple=(1,2,'three','Kelvin')
```
To create a tuple containing the single value 1, you need to include a comma after the 1:

``` python
x=(1,)
type(x)
```

```
## <class 'tuple'>
```

**The Built-In tuple()**

You can also use the built-in tuple() to create a tuple from another sequence type, such as a string:

``` python
tuple("Python")
```

```
## ('P', 'y', 't', 'h', 'o', 'n')
```
**Similarities Between Tuples and Strings**

Tuples and strings have a lot in common. Both are sequence types with finite lengths, both support indexing and slicing, both are immutable, and both can be iterated over in a loop.

The main difference between strings and tuples is that the elements of tuples can be any kind of value you like, whereas strings can only contain characters.

``` python
name =("David")
name[1]
```

```
## 'a'
```
The index notation [1] after the variable name tells Python to get the character at index 1 in the string "David". Since counting starts at zero,the character at index 1 is the letter "a".

Tuples also support index notation:

``` python
values =[1,3,4,7,9,0]
values[3]
```

```
## 7
```
Another feature that strings and tuples have in common is slicing.

``` python
values =[1,3,4,7,9,0]
values[2:4]
```

```
## [4, 7]
```
The slice values[2:4] creates a new tuple containing all the integers in values starting from position 2 and going up to but not including position 4.

**Tuples are immutable**

This means you cannot change the value of an element in a tuple once it has been created.If you do try  to change the values then you'll raise a TypeError.

**Tuples are iterable**

You can loop over them

``` python
name = ("LEONARD")
for i in name:
  print(i)
```

```
## L
## E
## O
## N
## A
## R
## D
```
***Checking for Existence of Values With (in)***

You can check whether a value is contained in a tuple with the in keyword.

``` python
name
```

```
## 'LEONARD'
```

``` python
"O" in name
```

```
## True
```
