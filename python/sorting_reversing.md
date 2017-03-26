# Sorting and Reversing

This page deals with reversing things.

## Reverse a string of characters

```python
str = 'a quick fox jumps over the lazy brown dog'
rstr = ''
for letter in str:
    rstr = letter + rstr
print rstr
```

Output:

```
god nworb yzal eht revo spmuj xof kciuq a
```

## Reverse the words in a sentence

```python
str = 'a quick fox jumps over the lazy brown dog'
str_array = str.split()
print ' '.join(str.reverse())
```

Output:

```
'dog brown lazy the over jumps fox quick a'
```

## Move positive integers to the front of a list

```python
arr = [ 1, 3, 4, 2, 6, 3, 6, 5, 8, 2, 4, 1, 9, 0, 7, 1, 0 ]

for idx, num in enumerate(arr):
    if num % 2 == 0:
        # We found a positive number
        del arr[idx]
        arr.insert(0, num)
print arr
```

Output:

```
[0, 0, 4, 2, 8, 6, 6, 2, 4, 1, 3, 3, 5, 1, 9, 7, 1]
```
