[toc]
## 05.1 Lists like arrays
```python

>>> x = [2, "two", [1, 2, 3]]
>>> len(x)
3

```
## 05.2 List indices
```python

>>> x = ["first", "second", "third", "fourth"]
>>> x[0]
'first'
>>> x[2]
'third'


>>> a = x[-1]
>>> a
'fourth'
>>> x[-2]
'third'


>>> x = ["first", "second", "third", "fourth"]    
>>> x[1:-1]
['second', 'third']
>>> x[0:3]
['first', 'second', 'third']
>>> x[-2:-1]
['third']


>>> x[-1:2]
[]


>>> x[:3]
['first', 'second', 'third']
>>> x[2:]
['third', 'fourth']


>>> y = x[:]
>>> y[0] = '1 st'
>>> y
['1 st', 'second', 'third', 'fourth']
>>> x
['first', 'second', 'third', 'fourth']

```
## 05.3 Modifying Lists
```python

>>> x = [1, 2, 3, 4]
>>> x[1] = "two"
>>> x
[1, 'two', 3, 4]


>>> x = [1, 2, 3, 4]
>>> x[len(x):] = [5, 6, 7]                #A
>>> x
[1, 2, 3, 4, 5, 6, 7]
>>> x[:0] = [-1, 0]                       #B
>>> x
[-1, 0, 1, 2, 3, 4, 5, 6, 7]
>>> x[1:-1] = []                          #C 
>>> x
[-1, 7]


>>> x = [1, 2, 3]
>>> x.append("four")
>>> x
[1, 2, 3, 'four']


>>> x = [1, 2, 3, 4]
>>> y = [5, 6, 7]
>>> x.append(y)  
>>> x
[1, 2, 3, 4, [5, 6, 7]]


>>> x = [1, 2, 3, 4]
>>> y = [5, 6, 7]
>>> x.extend(y)  
>>> x
[1, 2, 3, 4, 5, 6, 7]  


>>> x = [1, 2, 3]
>>> x.insert(2, "hello")
>>> print(x)
[1, 2, 'hello', 3]
>>> x.insert(0, "start")
>>> print(x)
['start', 1, 2, 'hello', 3]


>>> x = [1, 2, 3]
>>> x.insert(-1, "hello")
>>> print(x)
[1, 2, 'hello', 3]


>>> x = ['a', 2, 'c', 7, 9, 11]
>>> del x[1]
>>> x
['a', 'c', 7, 9, 11]
>>> del x[:2]
>>> x
[7, 9, 11]


>>> x = [1, 2, 3, 4, 3, 5]
>>> x.remove(3)
>>> x
[1, 2, 4, 3, 5]
>>> x.remove(3)
>>> x
[1, 2, 4, 5]
>>> x.remove(3)
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: list.remove(x): x not in list


>>> x = [1, 3, 5, 6, 7]
>>> x.reverse()
>>> x
[7, 6, 5, 3, 1]

```
## 05.4 Sorting Lists
```python

>>> x = [3, 8, 4, 0, 2, 1]
>>> x.sort()
>>> x
[0, 1, 2, 3, 4, 8]


>>> x = [2, 4, 1, 3]
>>> y = x[:]
>>> y.sort()
>>> y
[1, 2, 3, 4]
>>> x
[2, 4, 1, 3]


>>> x = ["Life", "Is", "Enchanting"]
>>> x.sort()
>>> x
['Enchanting', 'Is', 'Life']


>>> x = [1, 2, 'hello', 3]
>>> x.sort()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '<' not supported between instances of 'str' and 'int'


>>> x = [[3, 5], [2, 9], [2, 3], [4, 1], [3, 2]]
>>> x.sort()
>>> x
[[2, 3], [2, 9], [3, 2], [3, 5], [4, 1]]


>>> x = [[3, 5], [2, 9], [2, 3], [4, 1], [3, 2]]
>>> x.sort()
>>> x
[[2, 3], [2, 9], [3, 2], [3, 5], [4, 1]]

```
### 05.4.1 Custom sorting
```python

def compare_num_of_chars(string1):
    return len(string1)

>>> def compare_num_of_chars(string1):
...     return len(string1)
>>> word_list = ['Python', 'is', 'better', 'than', 'C']
>>> word_list.sort()
>>> print(word_list)
['C', 'Python', 'better', 'is', 'than']
>>> word_list = ['Python', 'is', 'better', 'than', 'C']
>>> word_list.sort(key=compare_num_of_chars)
>>> print(word_list)
['C', 'is', 'than', 'Python', 'better']

```
### 05.4.2 sorted() function
```python

>>> x = (4, 3, 1, 2)
>>> y = sorted(x)
>>> y
[1, 2, 3, 4] 
>>> z = sorted(x, reverse=True)
>>> z
[4, 3, 2, 1]

```
## 05.5 list operator
```python
```
### 05.5.1 in operator
```python

>>> 3 in [1, 3, 4, 5]
True
>>> 3 not in [1, 3, 4, 5]
False
>>> 3 in ["one", "two", "three"]
False
>>> 3 not in ["one", "two", "three"]
True

```
### 05.5.2 + operator
```python

>>> z = [1, 2, 3] + [4, 5]
>>> z
[1, 2, 3, 4, 5]

```
### 05.5.3 * operator
```python

>>> z = [None] * 4
>>> z
[None, None, None, None]

>>> z = [3, 1] * 2
>>> z
[3, 1, 3, 1]

```
### 05.5.4 min and max
```python

>>> min([3, 7, 0, -2, 11])
-2
>>> max([4, "Hello", [1, 2]])
Traceback (most recent call last):
  File "<pyshell#58>", line 1, in <module>
    max([4, "Hello",[1, 2]])
TypeError: '>' not supported between instances of 'str' and 'int'

```
### 05.5.5 search with index()
```python

>>> x = [1, 3, "five", 7, -2]
>>> x.index(7)
3
>>> x.index(5)
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: 5 is not in list

```
### 05.5.6 matches with count
```python

>>> x = [1, 2, 2, 3, 5, 2, 5]
>>> x.count(2)
3
>>> x.count(5)
2
>>> x.count(4)
0

```
## 05.6 Nested lists and deep copies
```python

>>> m = [[0, 1, 2], [10, 11, 12], [20, 21, 22]]
>>> m[0]
[0, 1, 2]
>>> m[0][1]
1
>>> m[2]
[20, 21, 22]
>>> m[2][2]
22

>>> nested = [0]
>>> original = [nested, 1]
>>> original 
[[0], 1]


>>> nested[0] = 'zero'
>>> original
[['zero'], 1]
>>> original[0][0] = 0
>>> nested
[0]
>>> original
[[0], 1]


>>> nested = [2]
>>> original
[[0], 1]


>>> original = [[0], 1]
>>> shallow = original[:]
>>> import copy
>>> deep = copy.deepcopy(original)


>>> shallow[1] = 2
>>> shallow
[[0], 2]
>>> original
[[0], 1]
>>> shallow[0][0] = 'zero'
>>> original
[['zero'], 1]


>>> deep[0][0] = 5
>>> deep
[[5], 1]
>>> original
[['zero'], 1]

```
## 05.7 tuples
```python
```
### 05.7.1 Tuple basics
```python

>>> x = ('a', 'b', 'c')   

>>> x[2]
'c'
>>> x[1:]
('b', 'c')
>>> len(x)
3
>>> max(x)
'c'
>>> min(x)
'a'
>>> 5 in x
False
>>> 5 not in x
True


>>> x[2] = 'd'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment


>>> x + x
('a', 'b', 'c', 'a', 'b', 'c')
>>> 2 * x
('a', 'b', 'c', 'a', 'b', 'c')


>>> x[:]
('a', 'b', 'c')
>>> x * 1
('a', 'b', 'c')
>>> x + ()
('a', 'b', 'c')

```
### 05.7.2 One-element tuples
```python

>>> x = 3
>>> y = 4
>>> (x + y)   # This adds x and y.
7
>>> (x + y,)  # Including a comma indicates the parentheses denote a tuple.
(7,)
>>> ()        # To create an empty tuple, use an empty pair of parentheses.
()

```
### 05.7.3 Tuple packing
```python

>>> (one, two, three, four) =  (1, 2, 3, 4)
>>> one
1
>>> two
2

one, two, three, four = 1, 2, 3, 4

>>> x = (1, 2, 3, 4)
>>> a, b, *c = x
>>> a, b, c
(1, 2, [3, 4])
>>> a, *b, c = x
>>> a, b, c
(1, [2, 3], 4)
>>> *a, b, c = x
>>> a, b, c
([1, 2], 3, 4)
>>> a, b, c, d, *e = x
>>> a, b, c, d, e
(1, 2, 3, 4, [])


>>> [a, b] = [1, 2]
>>> [c, d] = 3, 4
>>> [e, f] = (5, 6)
>>> (g, h) = 7, 8
>>> i, j = [9, 10]
>>> k, l = (11, 12)
>>> a
1
>>> [b, c, d]
[2, 3, 4]
>>> (e, f, g)
(5, 6, 7)
>>> h, i, j, k, l
(8, 9, 10, 11, 12)

```
### 05.7.4 Lists and Tuples
```python

>>> list((1, 2, 3, 4))
[1, 2, 3, 4]
>>> tuple([1, 2, 3, 4])
(1, 2, 3, 4)


>>> list("Hello")
['H', 'e', 'l', 'l', 'o']

```
## 05.8 sets
```python
```
### 05.8.1 Set operations
```python

>>> x = set([1, 2, 3, 1, 3, 5])     #1
>>> x
{1, 2, 3, 5}                       #2
>>> x.add(6)     #3 
>>> x
{1, 2, 3, 5, 6}    #2
>>> x.remove(5)               #4
>>> x
{1, 2, 3, 6}   #2
>>> 1 in x       #5
True
>>> 4 in x                     #5
False
>>> y = set([1, 7, 8, 9])
>>> x | y                 #6
{1, 2, 3, 6, 7, 8, 9}
>>> x & y                  #7
{1}
>>> x ^ y              #8
{2, 3, 6, 7, 8, 9}

```
### 05.8.2 Frozensets
```python

>>> x = set([1, 2, 3, 1, 3, 5]) 
>>> z = frozenset(x)
>>> z
frozenset({1, 2, 3, 5})
>>> z.add(6)
Traceback (most recent call last):
  File "<pyshell#79>", line 1, in <module>
    z.add(6)
AttributeError: 'frozenset' object has no attribute 'add'
>>> x.add(z)
>>> x
{1, 2, 3, 5, frozenset({1, 2, 3, 5})}


```