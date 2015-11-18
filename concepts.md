# Contents
1. [Generators](#generators)
2. [Map](#map)
3. [Filter](#filter)
4. [Lambda](#lambda)

-
###Generators

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
-
### Map

##### Key points
- Applies a function a to a list of elements
- Returns a list of the results

```python
items = [1, 2, 3, 4, 5]

"""
Refer to the lambda section to understand how it works, but know that we are saying that
each item in the list items is multiplied by itself and returned as a map object that
we are converting to a list and assigning to the variable squared
"""
squared = list(map(lambda x: x ** x, items))
```

Using map with a list of functions

```python
def multiply(x):
    return(x*x)
    
def add(x):
    return(x+x)
    
funcs = [multiply, add]

"""
Here we iterate over a range of numbers 0-5, reassigning a new list to the variable value 
each time we go through the numbers, and then printing the list.

Inside the map function we are iterating through a list of functions and send the value
i to that function, getting the returned value and returning the mapped object which is
then converted to a list.
"""
for i in range(5):
    value = list(map(lambda x: x(i), funcs))
    print(value)
```
-
### Filter

##### Key points
- Applies a function to a list of elements
- Only returns elements for which function returns true
- Resembles a for loop but is a built in function that performs faster

```python
items = [-4, -3, -2, -1, 0, 1, 2, 3, 4]

"""
Inside the filter function here we iterate through the items list and if the element
is less than zero, that qualifies as true and will be in the filter objected 
returned which is then converted to a list
"""
numbers_less_than_zero = list(filter(lambda x: x < 0, items))
print(numbers_less_than_zero)
```
-
### Lambda

##### Key points
- One line functions
- Used when you only need function to run once
- Great for quick operations, use a function for more controlled cases

```python
add = lambda x, y: x + y

print(add(3, 5))
```

Function vs. Lambda

```python
# Function
def square(x):
    return x**2
    
# Usage
square(2)

# Lambda
square = lambda x: x**2

# Usage
square(2)
```
