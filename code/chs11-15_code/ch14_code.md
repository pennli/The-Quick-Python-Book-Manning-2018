[toc]
## 14.1 intro to exceptions
### 14.1.1 General philosophy of errors and exception handling
```python

const ERROR = 1;
const OK = 0;
int save_to_file(filename) {
    int status;
    status = save_prefs_to_file(filename);
    if (status == ERROR) {
        ...handle the error...
    }
    status = save_text_to_file(filename);
    if (status == ERROR) {
        ...handle the error...
    }
    status = save_formats_to_file(filename);
    if (status == ERROR) {
        ...handle the error...
    }
    .
    .
    .
}
int save_text_to_file(filename) {
    int status;
    status = ...lower-level call to write size of text...
    if (status == ERROR) {
        return(ERROR);
    }
    status = ...lower-level call to write actual text data...
    if (status == ERROR) {
        return(ERROR);
    }
    .
    .
    .
}


def save_to_file(filename)
    try to execute the following block 
        save_text_to_file(filename)
        save_formats_to_file(filename)
        save_prefs_to_file(filename)
        .
        .
        .
    except that, if the disk runs out of space while 
        executing the above block, do this
        ...handle the error...
    
def save_text_to_file(filename) 
    ...lower-level call to write size of text...
    ...lower-level call to write actual text data...
    .
    .
    .

```

## 14.2 Exceptions in Python
### 14.2.2 Raising exceptions
```python

>>> alist = [1, 2, 3]
>>> element = alist[7] 
Traceback (innermost last):
  File "<stdin>", line 1, in ?
IndexError: list index out of range


>>> raise IndexError("Just kidding")
Traceback (innermost last):
  File "<stdin>", line 1, in ?
IndexError: Just kidding

```
### 14.2.3 Catching and handling exceptions
```python

try:
    body
except exception_type1 as var1:
    exception_code1
except exception_type2 as var2:
    exception_code2
    .
    .
    .
except:
    default_exception_code
else:
    else_body
finally:
    finally_body

```
### 14.2.4 Defining new exceptions
```python

class MyError(Exception):
    pass


try:
    raise MyError("Some information about what went wrong")
except MyError as error:
    print("Situation:", error)


try:
    raise MyError("Some information", "my_filename", 3)
except MyError as error:
    print("Situation: {0} with file {1}\n error code: {2}".format( 
        error.args[0],
 error.args[1], error.args[2]))

>>> raise MyError("Some information about what went wrong")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
__main__.MyError: Some information about what went wrong

Situation: Some information with file my_filename
error code: 3 

```
### 14.2.5 Debugging programs with the assert statement
```python

>>> x = (1, 2, 3)
>>> assert len(x) > 5
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError: len(x) not > 5

```
### 14.2.6 Exception inheritance hierarchy
```python

try:
    body
except LookupError as error:
    exception code
except IndexError as error:
    exception code

```
### 14.2.8 Example: exceptions in normal evaluation
```python

def cell_value(string):
    try:
        return float(string)
    except ValueError:
        if string == "":
            return 0
        else:
            return None


def safe_apply(function, x, y, spreadsheet):
    try:
        return function, (x, y, spreadsheet)
    except TypeError:
        return None

```
## 14.3 Context managers
```python

try:
    infile = open(filename)
    data = infile.read()
finally:
    infile.close()



with open(filename) as infile:
    data = infile.read()


```