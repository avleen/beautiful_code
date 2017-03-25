# Sort an array of arrays, on a specific key in the sub-arrays

You have an array of arrays, and you need to sort it on the second value in each
sub-array.
The array looks like:

```python
arr = [ [3, 12, 4], [6, 9, 14], [5, 8, 2] ]
```

You can solve this with `lambda`:

```python
arr = [ [3, 12, 4], [6, 9, 14], [5, 8, 2] ]
arr.sort(key=lambda x: x[1])
print arr
```

Output:

```
[[5, 8, 2], [6, 9, 14], [3, 12, 4]]
```

## How does this work?

The `Array` type can take an optional `key` argument, which is a function to run
on each element in the array prior to doing the comparison.

`lambda` is an anonymous function in Python - that just means it doesn't have a
name. If it had a name, it might look like this:

```python
def function_with_a_name(x):
    return x[1]
```

It takes the array element as argument `x`, and returns `x[1]`.
From that, the array knows to sort based on the numbers `8`, `9`, and `12`.
