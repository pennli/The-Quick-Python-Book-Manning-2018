[toc]

## 01.1 why should use python?
#### 01.1.2.3  
```python

# Perl version.
sub pairwise_sum {
    my($arg1, $arg2) = @_;
    my @result;
    for(0 .. $#$arg1) {
        push(@result, $arg1->[$_] + $arg2->[$_]);
    }
    return(\@result);
}

# Python version.
def pairwise_sum(list1, list2): 
    result = [] 
    for i in range(len(list1)): 
        result.append(list1[i] + list2[i]) 
    return result

```
#### 01.1.2.4  
```python

import http.server
http.server.test(HandlerClass=http.server.SimpleHTTPRequestHandler)

```
#### 01.1.3.3  
```python

>>> x = "2"
>>> x
'2'              #A
>>> x = int(x)
>>> x
2                #B


```