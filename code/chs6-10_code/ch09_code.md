[toc]
## 09.1 Basic function definitions
```python

>>> def fact(n): 
...     """Return the factorial of the given number."""            #1
...     r = 1
...     while n > 0:
...         r = r * n
...         n = n - 1
...     return r                                      #2
...

>>> fact(4)                            #1
24                                     #2 
>>> x = fact(4)                        #3
>>> x 
24
>>>

09.2. Positional parameters

>>> def power(x, y):
...     r = 1
...     while y > 0:
...         r = r * x
...         y = y - 1
...     return r
... 
>>> power(3, 3)
27


>>> power(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: power() missing 1 required positional argument: 'y'
>>>


>>> def power(x, y=2):
...     r = 1
...     while y > 0:
...         r = r * x
...         y = y - 1
...     return r
...


>>> power(3, 3)
27
>>> power(3)
9

```

## 09.2 Function parameter options
### 09.2.2 Passing arguments by parameter name
```python

def list_file_info(size=False, create_date=False, mod_date=False, ...):
    ...get file names...
    if size:
        # code to get file sizes goes here
    if create_date:
        # code to get create dates goes here
    # do any other stuff desired
    
    return fileinfostructure

fileinfo = list_file_info(size=True, mod_date=True)

>>> power(2, 3)
8
>>> power(3, 2)
9
>>> power(y=2, x=3)
9

```
### 09.2.3 Variable numbers of arguments
```python

>>> def maximum(*numbers):
...     if len(numbers) == 0:
...         return None
...     else:
...         maxnum = numbers[0]
...         for n in numbers[1:]:
...             if n > maxnum:
...                 maxnum = n
...         return maxnum
...

>>> maximum(3, 2, 8)
8
>>> maximum(1, 5, 9, -2, 2)
9


>>> def example_fun(x, y, **other):
...     print("x: {0}, y: {1}, keys in 'other': {2}".format(x, 
...           y, list(other.keys())))
...     other_total = 0
...     for k in other.keys():
...         other_total = other_total + other[k]
...     print("The total of values in 'other' is {0}".format(other_total))


>>> example_fun(2, y="1", foo=3, bar=4)
x: 2, y: 1, keys in 'other': ['foo', 'bar']
The total of values in 'other' is 7

```
## 09.3	Mutable objects as arguments
```python

>>> def f(n, list1, list2):
...    list1.append(3)
...    list2 = [4, 5, 6]
...    n = n + 1
...
>>> x = 5
>>> y = [1, 2]
>>> z = [4, 5]
>>> f(x, y, z)
>>> x, y, z
(5, [1, 2, 3], [4, 5])

```
## 09.4 Local, nonlocal, and global variables
```python

def fact(n):
    """Return the factorial of the given number."""
    r = 1
    while n > 0:
        r = r * n
        n = n - 1
    return r

>>> def fun():
...     global a
...     a = 1
...     b = 2
...

>>> a = "one"
>>> b = "two"

>>> fun()
>>> a
1
>>> b
'two'

top level-> g_var: 0 nl_var: 0
in test-> g_var: 0 nl_var: 2
in inner_test-> g_var: 1 nl_var: 4
in test-> g_var: 1 nl_var: 4
top level-> g_var: 1 nl_var: 0

```
## 09.5	Assigning functions to variables
```python

>>> def f_to_kelvin(degrees_f):                     #A
...     return 273.15 + (degrees_f - 32) * 5 / 9
...
>>> def c_to_kelvin(degrees_c):                      #B
...     return 273.15 + degrees_c
...
>>> abs_temperature = f_to_kelvin                    #C
>>> abs_temperature(32)
273.15
>>> abs_temperature = c_to_kelvin                      #D
>>> abs_temperature(0)
273.15


>>> t = {'FtoK': f_to_kelvin, 'CtoK': c_to_kelvin}      #1
>>> t['FtoK'](32)                                       #A
273.15
>>> t['CtoK'](0)                                        #B
273.15

```
## 09.6 lambda expressions
```python

>>> t2 = {'FtoK': lambda deg_f: 273.15 + (deg_f - 32) * 5 / 9, #1 
...       'CtoK': lambda deg_c: 273.15 + deg_c}                #1
>>> t2['FtoK'](32)
273.15

```
## 09.7 Generator functions
```python

>>> def four():
...     x = 0                                    #A
...     while x < 4:
...         print("in generator, x =", x)
...         yield x                               #B
...         x += 1                               #C
... 
>>> for i in four():
...     print(i)
...
in generator, x = 0
0
in generator, x = 1
1
in generator, x = 2
2
in generator, x = 3
3

>>> 2 in four()
in generator, x = 0
in generator, x = 1
in generator, x = 2
True
>>> 5 in four()
in generator, x = 0
in generator, x = 1
in generator, x = 2
in generator, x = 3
False


```
## 09.8 Decorators
```python

>>> def decorate(func):
...     print("in decorate function, decorating", func.__name__)
...     def wrapper_func(*args):
...         print("Executing", func.__name__)
...         return func(*args)
...     return wrapper_func
...
>>> def myfunction(parameter):
...     print(parameter)
...
>>> myfunction = decorate(myfunction)
in decorate function, decorating myfunction
>>> myfunction("hello")
Executing myfunction
hello


>>> def decorate(func):
...     print("in decorate function, decorating", func.__name__)  #1
...     def wrapper_func(*args):
...         print("Executing", func.__name__)
...         return func(*args)
...     return wrapper_func                                       #2
...
>>> @decorate                                                     #3
... def myfunction(parameter):
...     print(parameter)
...
in decorate function, decorating myfunction                      #4
>>> myfunction("hello")
Executing myfunction
hello


```