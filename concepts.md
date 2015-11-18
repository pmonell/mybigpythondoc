### Generators

##### Key points
- Iterator that you can iterate only once
- Does not store values in memory
- Values are not stored, rather they are yielded
- Like a list, but values are not stored in memory

```python
def generator_function():
    """
    Function iterates through a range of numbers 0-30 and yields each number individually
    """
    for i in range(30):
        yield i

# Usage
for item in generator_function():
    print(item)
```

A better example:

```python
def fibon(n):
    """
    Sets values a and b equal 1.  Iterates through a range of numbers determined by the 
    function argument and yields value a.  Reassigns values to a and b based on the 
    principles of fibonacci numbers and moves to the next sequence.
    """
    a = b = 1
    for i in range(n):
        yield a
        a, b = b, a + b

# Usage
for x in fibon(1000):
    print(x)
```

### Map
