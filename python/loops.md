# Loops

## Basic loops

### `for`

This is a simple loop to iterate over a list of things:

```python
arr = [1, 3, 5, 7, 9, 2, 4, 6, 8]
for num in arr:
    print num
```
Output:
```
1
3
5
7
9
2
4
6
8
```

### `while`

The `while` loop repeats itself until a condition is met:

```python
count = 0
while count < 5:
    print 'Hello World!'
    count += 1
```
Output:
```
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
```

## List comprehensions

A list comprehension is shorter way to write some simple loops, which create an
array:

```python
arr = [ x for x in range(0, 10) ]
print arr
```
Output:
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

They can be used to iterate over a thing, like a `for` loop, and do something
with each element:

```python
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
arr_times_2 = [ x * 2 for x in arr ]
print arr_times_2
```
Output:
```
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

Let's break this down and look at each part of the list comprehension. We'll
work back to front:
* `for x in arr`: This is your basic `for` loop. It is taking the array called
  `arr` and looping over it.
* `x * 2`: This is taking each element from the loop, and multiplying it by 2.
The result of a list comprehension is, as the name implies, a list (or array).

## Loop counters

Sometimes while you loop over an array, you need to know where in the array you
are. `enumerate` helps with this:

```python
arr = ['A', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
for idx, elem in enumerate(arr):
    print '{}: {}'.format(idx, elem)
```
Output:
```
0 A
1 quick
2 brown
3 fox
4 jumps
5 over
6 the
7 lazy
8 dog
```

## Looping over dictionaries

A dictionary is an associative array: a set of key-value pairs. You can loop
over these too!

```python
d = { 'fox': 'brown',
      'dog': 'lazy',
      'act': 'jumping',
      'speed': 'quick' }
for subject, attribute in d.items():
    print '{}: {}'.format(subject, attribute)
```
Output:
```
speed: quick
fox: brown
dog: lazy
act: jumping
```

## Finding a number which occurs only once

If you have a list of numbers, find the number which occurs only once

```python
from collections import defaultdict
arr = [ 1, 3, 4, 2, 6, 3, 6, 5, 8, 2, 4, 1, 9, 0, 7, 1, 0 ]
d = defaultdict(int)
for i in arr:
    d[i] += 1
for k, v in d.items():
    if v == 1:
        print '%s occurred only once' % k
```

## Select all of the even numbers from a list

```python
arr = [ 1, 3, 4, 2, 6, 3, 6, 5, 8, 2, 4, 1, 9, 0, 7, 1, 0 ]
evens = [ x for x in arr if x%2 == 0 ]
```
