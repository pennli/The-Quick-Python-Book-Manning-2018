[toc]
## 17.1 Types are objects, too
```python

>>> type(5)
<class 'int'>
>>> type(['hello', 'goodbye'])
<class 'list'>


>>> type_result = type(5)
>>> type(type_result)
<class 'type'>

```
## 17.2 Using types
```python

>>> type("Hello") == type("Goodbye")
True
>>> type("Hello") == type(5)
False

```
## 17.3 Types and user-defined classes
```python

>>> class A:
...     pass
...
>>> class B(A):
...     pass
...

>>> b = B()

>>> type(b)
<class '__main__.B'>

>>> b.__class__
<class '__main__.B'>

>>> b_class = b.__class__

>>> b_class == B
True

>>> b_class.__name__
'B'

>>> b_class.__bases__
(<class '__main__.A'>,)


>>> class C:
...     pass
...
>>> class D:
...     pass
...
>>> class E(D):
...     pass
...
>>> x = 12
>>> c = C()
>>> d = D()
>>> e = E()
>>> isinstance(x, E)
False
>>> isinstance(c, E)                                #1
False
>>> isinstance(e, E)
True
>>> isinstance(e, D)      #2
True
>>> isinstance(d, E)                                #3
False
>>> y = 12
>>> isinstance(y, type(5))                          #4
True

>>> issubclass(C, D)
False
>>> issubclass(E, D)
True
>>> issubclass(D, D)                                 #5
True
>>> issubclass(e.__class__, D)
True

```
## 17.5 What is a special method attribute?
```python

>>> from color_module import Color
>>> c = Color(15, 35, 3)

>>> print(c)
Color: R=15, G=35, B=3

```
## 17.6 Making an object behave like a list
```python

fileobject = open(filename, 'r')
lines = fileobject.readlines()
fileobject.close()
for line in lines:
    . . . do whatever . . .


fileobject = open(filename, 'r')
for line in fileobject:
    . . . do whatever . . .
fileobject.close()

```
## 17.7 The __getitem__ special method attribute
```python

class LineReader:
    def __init__(self, filename):
        self.fileobject = open(filename, 'r')                #A
    def __getitem__(self, index):
        line = self.fileobject.readline()                    #B
        if line == "":                                       #C
            	self.fileobject.close()                          #D
            raise IndexError                                 #E
            
        else:
            return line.split("::")[:2]                      #F

for name, age in LineReader("filename"):
    . . . do whatever . . .

import myutils
for name, age in myutils.LineReader("filename"):
    . . . do whatever . . .

```
## 17.8 Giving an object full list capability
```python

class TypedList:
    def __init__(self, example_element, initial_list=[]):
        self.type = type(example_element)                            #1
        if not isinstance(initial_list, list):
            raise TypeError("Second argument of TypedList must " 
                          "be a list.")
        for element in initial_list:
                if not isinstance(element, self.type):
                    raise TypeError("Attempted to add an element of " 
                                  "incorrect type to a typed list.")
        self.elements = initial_list[:]


class TypedList:
    def __init__(self, example_element, initial_list=[]):
        self.type = type(example_element)
        if not isinstance(initial_list, list):
            raise TypeError("Second argument of TypedList must " 
                            "be a list.")
        for element in initial_list: 
            self.__check(element)
        self.elements = initial_list[:]
    def __check(self, element):
        if type(element) != self.type:
            raise TypeError("Attempted to add an element of " 
                            "incorrect type to a typed list.")
    def __setitem__(self, i, element):
        self.__check(element)
        self.elements[i] = element
    def __getitem__(self, i):
        return self.elements[i]

>>> x = TypedList("", 5 * [""])
>>> x[2] = "Hello"
>>> x[3] = "There"
>>> print(x[2] + ' ' + x[3])
Hello There
>>> a, b, c, d, e = x
>>> a, b, c, d
('', '', 'Hello', 'There')

```
## 17.9 Subclassing from built-in types
### 17.9.1 Subclassing list
```python

class TypedListList(list):
    def __init__(self, example_element, initial_list=[]):
        self.type = type(example_element)
        if not isinstance(initial_list, list):
            raise TypeError("Second argument of TypedList must " 
                            "be a list.")
        for element in initial_list: 
            self.__check(element)
        super().__init__(initial_list)

    def __check(self, element):
        if type(element) != self.type:
            raise TypeError("Attempted to add an element of " 
                            "incorrect type to a typed list.")

    def __setitem__(self, i, element):
        self.__check(element)
        super().__setitem__(i, element)

>>> x = TypedListList("", 5 * [""])
>>> x[2] = "Hello"
>>> x[3] = "There"
>>> print(x[2] + ' ' + x[3])
Hello There
>>> a, b, c, d, e = x
>>> a, b, c, d
('', '', 'Hello', 'There')
>>> x[:]
['', '', 'Hello', 'There', '']
>>> del x[2]
>>> x[:]
['', '', 'There', '']
>>> x.sort()
>>> x[:]
['', '', '', 'There']

```
### 17.9.2 Subclassing UserList
```python

from collections import UserList
class TypedUserList(UserList):
    def __init__(self, example_element, initial_list=[]):
        self.type = type(example_element)
        if not isinstance(initial_list, list):
            raise TypeError("Second argument of TypedList must " 
                            "be a list.")
        for element in initial_list: 
            self.__check(element)
        super().__init__(initial_list)
    def __check(self, element):
        if type(element) != self.type:
            raise TypeError("Attempted to add an element of " 
                            "incorrect type to a typed list.")
    def __setitem__(self, i, element):
        self.__check(element)
        self.data[i] = element
    def __getitem__(self, i):
        return self.data[i]

>>> x = TypedUserList("", 5 * [""])
>>> x[2] = "Hello"
>>> x[3] = "There"
>>> print(x[2] + ' ' + x[3])
Hello There
>>> a, b, c, d, e = x
>>> a, b, c, d
('', '', 'Hello', 'There')
>>> x[:]
['', '', 'Hello', 'There', '']
>>> del x[2]
>>> x[:]
['', '', 'There', '']
>>> x.sort()
>>> x[:]
['', '', '', 'There']


```