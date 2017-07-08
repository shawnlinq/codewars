# The records of codewars using python

### 1. Multiply

```python
def multiply(a, b):
  return a * b
```

>null

### 2. Mumbling

```python
def accum(s):
    # your code
    li = []
    for i in range(len(s)):
        li.append(s[i]*(i+1))
    li2 = [j.capitalize() for j in li] 
    return "-".join(li2)
```

> This time no story, no theory. The examples below show you how to write function `accum`:
>
> **Examples:**
>
> ```
> accum("abcd")    # "A-Bb-Ccc-Dddd"
> accum("RqaEzty") # "R-Qq-Aaa-Eeee-Zzzzz-Tttttt-Yyyyyyy"
> accum("cwAt")    # "C-Ww-Aaa-Tttt"
> ```
>
> The parameter of accum is a string which includes only letters from `a..z` and `A..Z`.

