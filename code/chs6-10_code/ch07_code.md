[toc]
## 07.1 What's a dictionary?
```python

>>> x = []        
>>> y = {}        


>>> y[0] = 'Hello'
>>> y[1] = 'Goodbye'


>>> x[0] = 'Hello'
Traceback (innermost last):
  File "<stdin>", line 1, in ?
IndexError: list assignment index out of range


>>> print(y[0])
Hello
>>> y[1] + ", Friend."
'Goodbye, Friend.'


>>> y["two"] = 2
>>> y["pi"] = 3.14
>>> y["two"] * y["pi"]
6.28

>>> english_to_french = {}                    #A
>>> english_to_french['red'] = 'rouge'          #B
>>> english_to_french['blue'] = 'bleu'
>>> english_to_french['green'] = 'vert'
>>> print("red is", english_to_french['red'])   #C
red is rouge

```
## 07.2	Other dictionary operations
```python

>>> english_to_french = {'red': 'rouge', 'blue': 'bleu', 'green': 'vert'}

>>> len(english_to_french)
3


>>> list(english_to_french.keys())
['green', 'blue', 'red']


>>> list(english_to_french.values())
 ['vert', 'bleu', 'rouge']


>>> list(english_to_french.items())
[('green', 'vert'), ('blue', 'bleu'), ('red', 'rouge')]


>>> list(english_to_french.items())
[('green', 'vert'), ('blue', 'bleu'), ('red', 'rouge')]
>>> del english_to_french['green']
>>> list(english_to_french.items())
 [('blue', 'bleu'), ('red', 'rouge')]


>>> 'red' in english_to_french
True
>>> 'orange' in english_to_french
False


>>> print(english_to_french.get('blue', 'No translation'))
bleu
>>> print(english_to_french.get('chartreuse', 'No translation'))
No translation


>>> print(english_to_french.setdefault('chartreuse', 'No translation'))
No translation


>>> x = {0: 'zero', 1: 'one'}
>>> y = x.copy()
>>> y
{0: 'zero', 1: 'one'}


>>> z = {1: 'One', 2: 'Two'}
>>> x = {0: 'zero', 1: 'one'}
>>> x.update(z)
>>> x
{0: 'zero', 1: 'One', 2: 'Two'}

```
## 07.3 Word counting
```python

>>> sample_string = "To be or not to be"
>>> occurrences = {}
>>> for word in sample_string.split():
...     occurrences[word] = occurrences.get(word, 0) + 1   #1
...
>>> for word in occurrences:
...     print("The word", word, "occurs", occurrences[word], \
...            "times in the string")
...
The word To occurs 1 times in the string
The word be occurs 2 times in the string
The word or occurs 1 times in the string
The word not occurs 1 times in the string
The word to occurs 1 times in the string

```
## 07.5 Sparse matrices
```python

matrix = [[3, 0, -2, 11], [0, 9, 0, 0], [0, 7, 0, 0], [0, 0, 0, -5]]

matrix = {(0, 0): 3, (0, 2): -2, (0, 3): 11, 
          (1, 1): 9, (2, 1): 7, (3, 3): -5}

if (rownum, colnum) in matrix:
    element = matrix[(rownum, colnum)]
else:
    element = 0

```
## 07.6 Dictionaries as caches
```python

def sole(m, n, t):
    # . . . do some time-consuming calculations . . .
    return(result)


sole_cache = {}
def sole(m, n, t):
    if (m, n, t) in sole_cache:
        return sole_cache[(m, n, t)]
    else:
        # . . . do some time-consuming calculations . . .
        sole_cache[(m, n, t)] = result
        return result


```