# Follow (tail) a file as it is updated

```python
import os
import time

file_name = 'app.log'
fh = open(file_name, 'r')

while True:
    for line in fh.xreadlines():
        print line
    # Now we should have hit EOF. Check every second to see if we have new
    # lines.
    while True:
        if fh.tell() == os.stat(file_name).st_size:
            sleep 1
        else:
            # Reset the cursor, so we can read more lines
            fh.seek(0, 1)
            break
```

Let's step through each part of the code:

```python
while True:
    for line in fh.xreadlines():
        print line
```

We start by initiating an infinte loop, because we want to keep retrying the
rest of the code to read the file.
Then we take our first pass are reading and printing each line of the file.
`xreadlines` is a generator which reads a line from the file as it is needed,
rather than reading the whole file into memory.

```python
    # Now we should have hit EOF. Check every second to see if we have new
    # lines.
    while True:
```

Once we've finished reading all the existing lines in a file, we need to wait
for more lines to be added. Another infinite loop will let us sit and wait.

```python
        if fh.tell() == os.stat(file_name).st_size:
            sleep 1
```

`fh.tell()` returns the current position of the file handle, in the file.
`os.stat(file_name).st_size` returns the size of the file.
If these two numbers are the same, we don't have any new lines and can sleep for
a second.
If we didn't sleep, our code would be rechecking for new lines as fast as
possible, consuming all available CPU time.

```python
        else:
            # Reset the cursor, so we can read more lines
            fh.seek(0, 1)
            break
```

Once new lines have come in, we reset the position of out file handle.
The two values are for `offset` and `whence`:

* `0` offset: Move the file handle to the position of `whence`.
* `1` whence: The current position of the file handle.

Together, these effectively reset the EOF and let us continue reading more
lines.
Finally, we issue a `break` out of the current loop, so we can go back to the
top of the first loop and read more lines.
