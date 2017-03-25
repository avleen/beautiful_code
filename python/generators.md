# Generators

Generators are an efficient way to iterate over large lists of things.

## `xrange`

```python
def make_list():
    count = 0
    while count < 100000000:
        yield count
        count += 1

for i in make_list():
    print i
```

This is efficient because it doesn't require generating a huge list in memory
first, and then returning it and iterating through it.
If you've used the `xrange` function, this is how it works.

## From list comprehensions to generators

We can also turn a list comprehension into a generator.
Suppose we want to get all of the powers of two from 1 to 16:

```python
powers = ( 2 ** i for i in xrange(50) )
for i in powers:
    print powers
```
