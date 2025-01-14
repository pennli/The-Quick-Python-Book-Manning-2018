[toc]

## 03.2 built-in data types

### 03.2.1 Numbers
```python

>>> x = 5 + 2 - 3 * 2    
>>> x
1
>>> 5 / 2
2.5               #1
>>> 5 // 2
2                  #2
>>> 5 % 2
1
>>> 2 ** 8
256
>>> 1000000001 ** 3
1000000003000000003000000001    #3

>>> x = 4.3 ** 2.4
>>> x
33.13784737771648
>>> 3.5e30 * 2.77e45   
9.695e+75
>>> 1000000001.0 ** 3 
1.000000003e+27

>>> (3+2j) ** (2+3j)
(0.6817665190890336-2.1207457766159625j)
>>> x = (3+2j) * (4+9j)
>>> x                               #1
(-6+35j)
>>> x.real 
-6.0
>>> x.imag 
35.0

>>> round(3.49)       #1
3
>>> import math
>>> math.ceil(3.49)  #2
4

>>> x = False
>>> x
False
>>> not x
True
>>> y = True * 2    #1
>>> y
2

```
### 03.2.2 Lists
```python

>>> x = ["first", "second", "third", "fourth"]
>>> x[0]                   #1 
'first'                    #1
>>> x[2]                   #1
'third'
>>> x[-1]               #2 
'fourth'                #2 
>>> x[-2]               #2
'third'                 #2
>>> x[1:-1]             #2
['second', 'third']           #3
>>> x[0:3]                    #3 
['first', 'second', 'third']  #3
>>> x[-2:-1]                  #3
['third']                     #3
>>> x[:3]                     #3
['first', 'second', 'third']  #4
>>> x[-2:]                    #4
['third', 'fourth']           #4

>>> x = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> x[1] = "two"
>>> x[8:9] = []
>>> x
[1, 'two', 3, 4, 5, 6, 7, 8]
>>> x[5:7] = [6.0, 6.5, 7.0]          #1
>>> x
[1, 'two', 3, 4, 5, 6.0, 6.5, 7.0, 8]
>>> x[5:] 
[6.0, 6.5, 7.0, 8]

>>> x = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> len(x)
9
>>> [-1, 0] + x                     #1
[-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> x.reverse()                    #2 
>>> x
[9, 8, 7, 6, 5, 4, 3, 2, 1]

```
### 03.2.3  Tuples
```python

>>> x = [1, 2, 3, 4]
>>> tuple(x)
(1, 2, 3, 4)


>>> x = (1, 2, 3, 4)
>>> list(x)
[1, 2, 3, 4]

```
### 03.2.4  Strings
```python

>>> x = "live and     let \t   \tlive"
>>> x.split()
['live', 'and', 'let', 'live']
>>> x.replace("    let \t   \tlive", "enjoy life")
'live and enjoy life'
>>> import re                         #1
>>> regexpr = re.compile(r"[\t ]+")
>>> regexpr.sub(" ", x)
'live and let live'


>>> e = 2.718
>>> x = [1, "two", 3, 4.0, ["a", "b"], (5, 6)]
>>> print("The constant e is:", e, "and the list x is:", x)   #1
The constant e is: 2.718 and the list x is: [1, 'two', 3, 4.0,
['a', 'b'], (5, 6)]
>>> print("the value of %s is: %.2f" % ("e", e))    #2
the value of e is: 2.72

```
### 03.2.5 Dictionaries
```python

>>> x = {1: "one", 2: "two"}
>>> x["first"] = "one"     #A
>>> x[("Delorme", "Ryan", 1995)] = (1, 2, 3)   #1
>>> list(x.keys())
['first', 2, 1, ('Delorme', 'Ryan', 1995)]
>>> x[1]
'one'
>>> x.get(1, "not available")
'one'
>>> x.get(4, "not available")         #2
'not available'

```
### 03.2.6 Sets
```python

>>> x = set([1, 2, 3, 1, 3, 5])   #1
>>> x
{1, 2, 3, 5}    #2
>>> 1 in x                 #3      
True
>>> 4 in x               #3 
False
>>>

```
### 03.2.7 File Objectss
```python

>>> f = open("myfile", "w")                      #1
>>> f.write("First line with necessary newline character\n")
44
>>> f.write("Second line to write to the file\n")
33
>>> f.close()
>>> f = open("myfile", "r")            #2
>>> line1 = f.readline()
>>> line2 = f.readline()
>>> f.close()
>>> print(line1, line2)
First line with necessary newline character
Second line to write to the file
>>> import os                                   #4
>>> print(os.getcwd())
c:\My Documents\test
>>> os.chdir(os.path.join("c:", "My Documents", "images"))    #4
>>> filename = os.path.join("c:", "My Documents",  #4
"test", "myfile")                                  #5
>>> print(filename)
c:\My Documents\test\myfile
>>> f = open(filename, "r")
>>> print(f.readline())
First line with necessary newline character
>>> f.close()

```

## 03.3 control flow
### 03.3.2 If-elif-else
```python

x = 5
if x < 5:
    y = -1
    z = 5
elif x > 5:    #1
    y = 1      #1
    z = 11     #1
else:
    y = 0      #2
    z = 10     #2
print(x, y, z)

```
### 03.3.3 While
```python

u, v, x, y = 0, 0, 100, 30     #1
while x > y:            #2
    u = u + y           #2
    x = x - y           #2 
    if x < y + 2:       #2
        v = v + x       #2
        x = 0           #2
    else:               #2
        v = v + y + 2   #2
        x = x - y - 2   #2
print(u, v)

```
### 03.3.4 For
```python

item_list = [3, "string1", 23, 14.0, "string2", 49, 64, 70]
for x in item_list:                         #1
    if not isinstance(x, int):
        continue                 #2
    if not x % 7:
        print("found an integer divisible by seven: %d" % x)
        break

```
### 03.3.5 Functions
```python

>>> def funct1(x, y, z):          #1
...     value = x + 2*y + z**2
...     if value > 0:
...         return x + 2*y + z**2   #2 
...     else:
...         return 0 
...
>>> u, v = 3, 4
>>> funct1(u, v, 2)
15
>>> funct1(u, z=v, y=2)      #3
23
>>> def funct2(x, y=1, z=1):        #4
...     return x + 2 * y + z ** 2
...
>>> funct2(3, z=4)
21
>>> def funct3(x, y=1, z=1, *tup):     #5
...     print((x, y, z) + tup)
...
>>> funct3(2)
(2, 1, 1)
>>> funct3(1, 2, 3, 4, 5, 6, 7, 8, 9)
(1, 2, 3, 4, 5, 6, 7, 8, 9)
>>> def funct4(x, y=1, z=1, **kwargs):  #6
...     print(x, y, z, kwargs)
>>> funct4(1, 2, m=5, n=9, z=3)
1 2 3 {'n': 9, 'm': 5}

```
### 03.3.6 Exceptions
```python

class EmptyFileError(Exception):
    pass
filenames = ["myfile1", "nonExistent", "emptyFile", "myfile2"]
for file in filenames:
    try:
	f = open(file, 'r')
    	line = f.readline()
    	if line == "":
            f.close()
            raise EmptyFileError("%s: is empty" % file)
    except IOError as error:
    	print("%s: could not be opened: %s" % (file, error.strerror)
    except EmptyFileError as error:
    	 print(error)
    else:
        print("%s: %s" % (file, f.readline()))
    finally:
        print("Done processing", file)

```
### 03.3.7 Context handling using the with keyword
```python

filename = "myfile.txt"
with open(filename, "r") as f:
    for line in f:
        print(f)

filename = "myfile.txt"
try:
    f = open(filename, "r")
    for line in f:
        print(f)
except Exception as e:
    raise e
finally:
    f.close()

```
## 03.5 Object-oriented programming
```python

>>> import sh
>>> c1 = sh.Circle()           #1
>>> c2 = sh.Circle(5, 15, 20)
>>> print(c1)
Circle of radius 1 at coordinates (0, 0)
>>> print(c2)                           #2
Circle of radius 5 at coordinates (15, 20)
>>> c2.area()
78.539749999999998
>>> c2.move(5,6)                 #3
>>> print(c2)
Circle of radius 5 at coordinates (20, 26)

```