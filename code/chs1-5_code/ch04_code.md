[toc]
## 4.1 Indentation
```python

n = 9
r = 1
while n > 0:
    r = r * n
    n = n - 1


```
## 4.3 Variables
```python

>>> x = "Hello"
>>> print(x)
Hello
>>> x = 5
>>> print(x)
5

>>> x = 5
>>> print(x)
5
>>> del x
>>> print(x)
Traceback (most recent call last):
 File "<stdin>", line 1, in <module>
NameError: name 'x' is not defined
>>>

```
## 4.4 Expressions
```python

x = 3
y = 5
z = (x + y) / 2


```
## 4.5 Strings
```python

x = "Hello, World"
x = "\tThis string starts with a \"tab\"." 
x = "This string contains a single backslash(\\)."
x = "Hello, World"
x = 'Hello, World'
x = "Don't need a backslash"
x = 'Can\'t get by without a backslash'
x = "Backslash your \" character!"
x = 'You can leave the " alone'
x = """Starting and ending a string with triple " characters
permits embedded newlines, and the use of " and ' without
backslashes"""


```
## 4.6 Numbers
```python

>>> 5 + 2 - 3 * 2
1
>>> 5 / 2          # floating-point result with normal division
2.5
>> 5 / 2.0         # also a floating-point result
2.5
>>> 5 // 2         # integer result with truncation when divided using '//'
2
>>> 30000000000    # This would be too large to be an int in many languages
30000000000
>>> 30000000000 * 3
90000000000
>>> 30000000000 * 3.0
90000000000.0
>>> 2.0e-8            # Scientific notation gives back a float.
2e-08
>>> 3000000 * 3000000                    
9000000000000
>>> int(200.2)
200
>>> int(2e2)
200
>>> float(200)
200.0

```
### 4.6.4 Complex Numbers
```python

>>> (3+2j)
(3+2j)

>>> 3 + 2j - (4 + 4j)
(-1-2j)
>>> (1 + 2j) * (3 + 4j)
(-5+10j)
>>> 1j*1j
(-1+0j)

>>> z = 3+5j
>>> z.real
3.0
>>> z.imag
5.0

```
### 4.6.5 Advanced complex-number functions
```python

>>> import cmath
>>> cmath.sqrt(-1)
1j

```
## 4.8 Getting input
```python

>>> name = input("Name? ")
Name? Jane
>>> print(name)
Jane
>>> age = int(input("Age? "))
Age? 28
>>> print(age)
28
>>>


```