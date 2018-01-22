# 2015-09-03

## Computing *e*

### Problem statement

Compute *e* using Python without use of a pre-defined function, e.g., `math.e`, `math.exp(1)`. Modules like `math` are fair game.

### Adding up numbers

Specifiying addition is trivial:

```python
print 0 + 1 + 2 + 3 + 4 + 5
# ==> 15 
```

But what we really want is to add all the integers from 0 to *n*, given an *arbitrary* value of *n*.

```python
n = 5
total = 0  
for i in range(0,n+1):
    total += i   # means the same thing as total = total + i
    
print total
# ==> 15
```

### Calculating factorial

```python
print math.factorial(4)
# ==> 24
print math.factorial(0)
# ==> 1
```

### Putting it together

```python
n = 5
total = 0
for i in range(0,n+1):
    total += 1 / math.factorial(i)
    
print total
# ==> 2
```

Try again:

```python
n = 5
total = 0
for i in range(0,n+1):
    total += 1.0 / math.factorial(i)
    
print total
# ==> 2.71666666667
```
