[toc]
## 16.1 What is a regular expression?
```python

import re
regexp = re.compile("hello")
count = 0
file = open("textfile", 'r')
for line in file.readlines():
    if regexp.search(line):
        count = count + 1
file.close()
print(count)

```

## 16.3 Regular expressions and raw strings
### 16.3.1 Raw strings to the rescue
```python

r"Hello"
r"""\tTo be\n\tor not to be"""
r'Goodbye'
r'''12345'''

>>> r"Hello" == "Hello"
True
>>> r"\the" == "\\the"
True
>>> r"\the" == "\the"
False
>>> print(r"\the")
\the
>>> print("\the")
        he

```
## 16.4 Extracting matched text from strings
```python

import re
regexp = re.compile(r"[-a-zA-Z]+,"                             #A
                    r" [-a-zA-Z]+"                             #B
                    r"( [-a-zA-Z]+)?"                          #C
                    r": (\d\d\d-)?\d\d\d-\d\d\d\d"             #D
                   )
file = open("textfile", 'r')
for line in file.readlines():
    if regexp.search(line):
        print("Yeah, I found a line with a name and number. So what?")
file.close()


import re
regexp = re.compile(r"(?P<last>[-a-zA-Z]+),"                      #A
                    r" (?P<first>[-a-zA-Z]+)"                     #B
                    r"( (?P<middle>([-a-zA-Z]+)))?"               #C
                    r": (?P<phone>(\d\d\d-)?\d\d\d-\d\d\d\d)"     #D
                   )
file = open("textfile", 'r')
for line in file.readlines():
    result = regexp.search(line)
    if result == None:
        print("Oops, I don't think this is a record")
    else:
        lastname = result.group('last')
        firstname = result.group('first')
        middlename = result.group('middle')
        if middlename == None:
            	middlename = ""
        phonenumber = result.group('phone')
    print('Name:', firstname, middlename, lastname,' Number:', phonenumber)
file.close()

```
## 16.5 Substituting text with regular expressions
```python

>>> import re
>>> string = "If the the problem is textual, use the the re module"
>>> pattern = r"the the"
>>> regexp = re.compile(pattern)
>>> regexp.sub("the", string)
'If the problem is textual, use the re module'


>>> import re
>>> int_string = "1 2 3 4 5"
>>> def int_match_to_float(match_obj):
...     return(match_obj.group('num') + ".0")
...
>>> pattern = r"(?P<num>[0-9]+)"
>>> regexp = re.compile(pattern)
>>> regexp.sub(int_match_to_float, int_string)
'1.0 2.0 3.0 4.0 5.0'

```
