[toc]

## 18.3 A concrete example
### 18.3.2 Basic use of the mathproj package
```python

>>> import mathproj
Hello from mathproj init


>>> mathproj.version
1.03

```
### 18.3.3 Loading subpackages and submodules
```python

>>> import mathproj
Hello from mathproj init
>>> mathproj.comp.numeric.n1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'mathproj' has no attribute 'comp'


>>> import mathproj.comp.numeric.n1
Hello from mathproj.comp init
Hello from numeric init
>>> mathproj.comp.numeric.n1.g()
version is 1.03
Called function h in module n2


>>> mathproj.comp
<module 'mathproj.comp' from 'mathproj/comp/__init__.py'>
>>> mathproj.comp.numeric
<module 'mathproj.comp.numeric'  from 'mathproj/comp/numeric/__init__.py'>

```
### 18.3.4 import statements within packages
```python

from mathproj import version
from mathproj.comp import c1
from mathproj.comp.numeric.n2 import h
def g():
    print("version is", version)
    print(h())


from .n2 import h

from mathproj import version
from mathproj.comp import c1
from mathproj.comp.numeric.n2 import h


from ... import version
from ..  import c1
from . n2 import h

```
## 18.4 The __all__ attribute
```python

>>> from mathproj import *
Hello from mathproj init
Hello from mathproj.comp init


>>> comp
<module 'mathproj.comp' from 'mathproj/comp/__init__.py'>

>>> c1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'c1' is not defined


>>> from mathproj.comp import c1
>>> c1
<module 'mathproj.comp.c1' from 'mathproj/comp/c1.py'>


```