[toc]

## 13.1 Opening files
```python

with open('myfile', 'r') as file_object:
    line = file_object.readline()


import os
file_name = os.path.join("c:", "My Documents", "test", "myfile")
file_object = open(file_name, 'r')

```
## 13.2 Closing files
```python

file_object = open("myfile", 'r')
line = file_object.readline()
# . . . any further reading on the file_object . . .
file_object.close()


with open("myfile", 'r') as file_object:
    line = file_object.readline()
    # . . . any further reading on the file_object . .

```
## 13.3 Opening files in writer or other modes
```python

file_object = open("myfile", 'w')
file_object.write(“Hello, World\n”)
file_object.close()

```
## 13.4 Functions to read and write text or binary data
```python

file_object = open("myfile", 'r')
count = 0
while file_object.readline() != "":
    count = count + 1
print(count)
file_object.close()


file_object = open("myfile", 'r')
print(len(file_object.readlines()))
file_object.close()


file_object = open("myfile", 'r')
count = 0
for line in file_object:
    count = count + 1
print(count)
file_object.close()

input_file = open("myfile", 'rb') 
header = input_file.read(4)       
data = input_file.read()          
input_file.close()


input_file = open("myfile.txt", 'r')
lines = input_file.readlines()
input_file.close()
output = open("myfile2.txt", 'w')
output.writelines(lines)
output.close()

```
### 13.4.1 Using binary mode
```python

input_file = open("myfile", 'rb')
header = input_file.read(4)
data = input_file.read()
input_file.close()

```
## 13.5 Reading and writing with pathlib
```python

>>> from pathlib import Path
>>> p_text = Path('my_text_file')
>>> p_text.write_text('Text file contents')
18
>>> p_text.read_text()
'Text file contents'
>>> p_binary = Path('my_binary_file')
>>> p_binary.write_bytes(b'Binary file contents')
20
>>> p_binary.read_bytes()
b'Binary file contents'

```
## 13.6 Screen input/output and redirection
```python

>>> x = input("enter file name to use: ")
enter file name to use: myfile
>>> x
'myfile'


>>> x = int(input("enter your number: "))
enter your number: 39
>>> x
39


>>> import sys
>>> print("Write to the standard output.")
Write to the standard output.
>>> sys.stdout.write("Write to the standard output.\n")
Write to the standard output.
30                                                   #A
>>> s = sys.stdin.readline()
An input line
>>> s
'An input line\n'


>>> import sys
>>> f= open("outfile.txt", 'w')
>>> sys.stdout = f
>>> sys.stdout.writelines(["A first line.\n", "A second line.\n"]) #A
>>> print("A line from the print function")
>>> 3 + 4                                           #B
>>> sys.stdout = sys.__stdout__
>>> f.close()
>>> 3 + 4
7


>>> import sys
>>> f = open("outfile.txt", 'w')
>>> print("A first line.\n", "A second line.\n", file=f)   #A
>>> 3 + 4
7
>>> f.close()
>>> 3 + 4
7

```
## 13.7 Reading structured binary data with the struct module
```python

import struct
record_format = 'hd4s'
record_size = struct.calcsize(record_format)
result_list = []
input = open("data", 'rb')
while 1:
    record = input.read(record_size)                    #A
    if record == '':                                    #1
        input.close()
        break
    result_list.append(struct.unpack(record_format, record))    #B

>>> import struct
>>> record_format = 'hd4s'
>>> struct.pack(record_format, 7, 3.14, b'gbye')
b'\x07\x00\x00\x00\x00\x00\x00\x00\x1f\x85\xebQ\xb8\x1e\t@gbye'

```
## 13.8 Pickling objects into files
```python

import pickle
.
.
.
file = open("state", 'wb')
pickle.dump(a, file)
pickle.dump(b, file)
pickle.dump(c, file)
file.close()

import pickle
file = open("state", 'rb')
a = pickle.load(file)
b = pickle.load(file)
c = pickle.load(file)
file.close()


import pickle
.
.
.
def save_data():
    global a, b, c
    file = open("state", 'w')
    data = {'a': a, 'b': b, 'c': c}
    pickle.dump(data, file)
    file.close()

def restore_data():
    global a, b, c
    file = open("state", 'r')
    data = pickle.load(file)
    file.close()
    a = data['a']
    b = data['b']
    c = data['c']
    .
    .

>>> import pickle
>>> file = open("solecache",'wb')
>>> pickle.dump({}, file)
>>> file.close()

```
## 13.9 Shelving objects
```python

>>> import shelve
>>> book = shelve.open("addresses")

>>> book['flintstone'] = ('fred', '555-1234', '1233 Bedrock Place')
>>> book['rubble'] = ('barney', '555-4321', '1235 Bedrock Place') 


>>> book.close()

>>> import shelve
>>> book = shelve.open("addresses")

>>> book['flintstone']
('fred', '555-1234', '1233 Bedrock Place')

```