[toc]
## 06.1 Strings as sequences of characters
```python

>>> x = "Hello"
>>> x[0]
'H'
>>> x[-1]
'o'
>>> x[1:]
'ello'


>>> x = "Goodbye\n"
>>> x = x[:-1]
>>> x
'Goodbye'


>>> len("Goodbye")
7

```
## 06.2 Basic String operations
```python

>>> x = "Hello " + "World"
>>> x
'Hello World'


>>> 8 * "x"
'xxxxxxxx'

```

## 06.3 Special characters and escape sequences
### 06.3.2 Numeric and Unicode escapes
```python

>>> 'm'
'm'
>>> '\155'
'm'
>>> '\x6D'
'm'


>>> '\n'
'\n'
>>> '\012'
'\n'
>>> '\x0A'
'\n'


>>> unicode_a ='\N{LATIN SMALL LETTER A}'      #A
>>> unicode_a
'a'                                            #1
>>> unicode_a_with_acute = '\N{LATIN SMALL LETTER A WITH ACUTE}'      
>>> unicode_a_with_acute
'á'
>>> "\u00E1"                                   #B
'á'
>>>

```
### 06.3.3 Printing vs evaluating
```python

>>> 'a\n\tb'
'a\n\tb'
>>> print('a\n\tb')
a
    b


>>> print("abc\n")
abc

>>> print("abc\n", end="")           
abc
>>>

```

## 06.4 String methods
### 06.4.1 split and join string methods
```python

>>> " ".join(["join", "puts", "spaces", "between", "elements"])
'join puts spaces between elements'


>>> "::".join(["Separated", "with", "colons"])
'Separated::with::colons'


>>> "".join(["Separated", "by", "nothing"])
'Separatedbynothing'


>>> x = "You\t\t can have tabs\t\n \t and newlines \n\n mixed in"
>>> x.split()
['You', 'can', 'have', 'tabs', 'and', 'newlines', 'mixed', 'in']
>>> x = "Mississippi"
>>> x.split("ss")
['Mi', 'i', 'ippi']


>>> x = 'a b c d'
>>> x.split(' ', 1)
['a', 'b c d']
>>> x.split(' ', 2)
['a', 'b', 'c d']
>>> x.split(' ', 9)
['a', 'b', 'c', 'd']

```
### 06.4.2 Converting strings to numbers
```python

>>> float('123.456')
123.456
>>> float('xxyy') 
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: could not convert string to float: 'xxyy'
>>> int('3333')
3333
>>> int('123.456')                       #A
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: invalid literal for int() with base 10: '123.456'
>>> int('10000', 8)                   #B
4096
>>> int('101', 2)
5
>>> int('ff', 16)
255
>>> int('123456', 6)              #C
Traceback (innermost last):
 File "<stdin>", line 1, in ?
ValueError: invalid literal for int() with base 6: '123456'

```
### 06.4.3 Extra whitespace
```python

>>> x = "  Hello,    World\t\t "
>>> x.strip()
'Hello,    World'
>>> x.lstrip()
'Hello,    World\t\t '
>>> x.rstrip()
'  Hello,    World'


>>> import string
>>> string.whitespace
' \t\n\r\x0b\x0c'
>>> " \t\n\r\v\f"
' \t\n\r\x0b\x0c'


>>> x = "www.python.org"
>>> x.strip("w")                       #A
'.python.org'
>>> x.strip("gor")                     #1
'www.python.'
>>> x.strip(".gorw")                    #B
'python'

```
### 06.4.4 String searching
```python

>>> x = "Mississippi"
>>> x.find("ss")
2
>>> x.find("zz")
-1


>>> x = "Mississippi"
>>> x.find("ss", 3)
5
>>> x.find("ss", 0, 3)
-1


>>> x = "Mississippi"
>>> x.rfind("ss")
5


>>> x = "Mississippi"
>>> x.count("ss")
2


>>> x = "Mississippi"
>>> x.startswith("Miss")
True
>>> x.startswith("Mist")
False
>>> x.endswith("pi")
True
>>> x.endswith("p")
False


>>> x.endswith(("i", "u"))
True

```
### 06.4.5 Modifying strings
```python

>>> x = "Mississippi"
>>> x.replace("ss", "+++")
'Mi+++i+++ippi'


>>> x = "~x ^ (y % z)"
>>> table = x.maketrans("~^()", "!&[]")
>>> x.translate(table)
'!x & [y % z]'

```
### 06.4.6 Modifying strings with list manipulations
```python

>>> text = "Hello, World"
>>> wordList = list(text)
>>> wordList[6:] = []                    #A 
>>> wordList.reverse()
>>> text = "".join(wordList)      
>>> print(text)                          #B
,olleH

```
### 06.4.7 Userful methods
```python

>>> x = "123"
>>> x.isdigit()
True
>>> x.isalpha()
False
>>> x = "M"
>>> x.islower()
False
>>> x.isupper()
True

```
## 06.5 Objects to strings
```python

>>> repr([1, 2, 3])
'[1, 2, 3]'
>>> x = [1]
>>> x.append(2)
>>> x.append([3, 4])
>>> 'the list x is ' + repr(x)
'the list x is [1, 2, [3, 4]]'

```

## 06.6 Using the format method
### 06.6.1 format method
```python

>>> "{0} is the {1} of {2}".format("Ambrosia", "food", "the gods") #1
'Ambrosia is the food of the gods'
>>> "{{Ambrosia}} is the {0} of {1}".format("food", "the gods")    #2
'{Ambrosia} is the food of the gods'

```
### 06.6.2 format method, named params
```python

>>> "{food} is the food of {user}".format(food="Ambrosia", 
...       user="the gods") 
'Ambrosia is the food of the gods'


>>> "{0} is the food of {user[1]}".format("Ambrosia", 
...          user=["men", "the gods", "others"]) 
'Ambrosia is the food of the gods'

```
### 06.6.3 format specifiers
```python

>>> "{0:10} is the food of gods".format("Ambrosia")      #1
'Ambrosia   is the food of gods'
>>> "{0:{1}} is the food of gods".format("Ambrosia", 10)   #2
'Ambrosia   is the food of gods'
>>> "{food:{width}} is the food of gods".format(food="Ambrosia", width=10)
'Ambrosia   is the food of gods'
>>> "{0:>10} is the food of gods".format("Ambrosia")         #3 
'  Ambrosia is the food of gods'
>>> "{0:&>10} is the food of gods".format("Ambrosia")           #4
'&&Ambrosia is the food of gods'

```
## 06.7 Formatting strings with %
```python

>>> "%s is the %s of %s" % ("Ambrosia", "food", "the gods")
'Ambrosia is the food of the gods'


>>> "%s is the %s of %s" % ("Nectar", "drink", "gods")
'Nectar is the drink of gods'
>>> "%s is the %s of the %s" % ("Brussels Sprouts", "food", 
...        "foolish")
'Brussels Sprouts is the food of the foolish'


>>> x = [1, 2, "three"]
>>> "The %s contains: %s" % ("list", x)
"The list contains: [1, 2, 'three']"

```
### 06.7.1 Formatting sequences
```python

>>> "Pi is <%-6.2f>" % 3.14159 # use of the formatting sequence: %–6.2f
'Pi is <3.14  >'

```
### 06.7.2 Named params and Formatting sequences
```python

>>> num_dict = {'e': 2.718, 'pi': 3.14159}
>>> print("%(pi).2f - %(pi).4f - %(e).2f" % num_dict)
3.14 - 3.1416 - 2.72

```
## 06.8 String interpolation
```python

>>> value = 42
>>> message = f"The answer is {value}"
>>> print(message)
The answer is 42

>>> pi = 3.1415
>>> print(f"pi is {pi:{10}.{2}}")
pi is        3.1

```
## 06.9 Bytes
```python

>>> unicode_a_with_acute = '\N{LATIN SMALL LETTER A WITH ACUTE}'
>>> unicode_a_with_acute
'á'
>>> xb = unicode_a_with_acute.encode()    #1
>>> xb
b'\xc3\xa1'                               #2 
>>> xb += 'A'                              #3
Traceback (most recent call last):
  File "<pyshell#35>", line 1, in <module>
    xb += 'A'
TypeError: can't concat str to bytes
>>> xb.decode()                           #4
'á'


```