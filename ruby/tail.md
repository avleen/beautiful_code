# Follow (tail) a file as it is updated

```ruby
file_name = 'app.log'
fh = open(file_name, 'r')

loop do
    fh.each_line do |line|
        print line
    end
    loop do
        if fh.tell == File.stat(file_name).size
            sleep 1
        else
            fh.seek(0, 1)
            break
        end
    end
end
```

Let's step through each part of the code:

```ruby
file_name = 'app.log'
fh = open(file_name, 'r')

loop do
```

We start by defining the name of the file, and opening it.
Next we start an infinite loop, which will be the main body of our code. It will
allow is to keep interating on the file as new lines come in.

```ruby
    fh.each_line do |line|
        print line
    end
```

With the file open, we start by reading in all of the current lines.
If you don't want to read in all of the current lines you can add the following
code just before this loop, which will jump the file handle to the end of the
file:

```ruby
    fh.seek(0, 2)
```

```ruby
    loop do
```

Once we've finished reading all the existing lines in a file, we need to wait
for more lines to be added. Another infinite loop will let us sit and wait.

```ruby
        if fh.tell == File.stat(file_name).size
            sleep 1
```

`fh.tell` returns the current position of the file handle, in the file.
`File.stat(file_name).size` returns the size of the file.
If these two numbers are the same, we don't have any new lines and can sleep for
a second.
If we didn't sleep, our code would be rechecking for new lines as fast as
possible, consuming all available CPU time.

```ruby
        else
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
