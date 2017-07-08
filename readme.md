# The records of codewars using python

### 1. Multiply

```python
def multiply(a, b):
  return a * b
```

> null

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

### 3. Sum of two lowest positive integers

```python
def sum_two_smallest_numbers(numbers):
    li = []
    for i in range(len(numbers)):
        for j in range(i+1, len(numbers)):
            li.append(numbers[i]+numbers[j])
    return min(i for i in li)
```

> Create a function that returns the sum of the two lowest positive numbers given an array of minimum 4 integers. No floats or empty arrays will be passed.
>
> For example, when an array is passed like [19,5,42,2,77], the output should be 7.
>
> [10,343445353,3453445,3453545353453] should return 3453455.
>
> Hint: Do not modify the original array.

### 4. Remove the minimum

```python
def remove_smallest(numbers):
    if numbers:
        numbers.remove(min(numbers))
    return numbers
    raise NotImplementedError("TODO: remove_smallest")
```

> # The museum of incredible dull things
>
> The museum of incredible dull things wants to get rid of some exhibitions. Miriam, the interior architect, comes up with a plan to remove the most boring exhibitions. She gives them a rating, and then removes the one with the lowest rating.
>
> However, just as she finished rating all exhibitions, she's off to an important fair, so she asks you to write a program that tells her the ratings of the items after one removed the lowest one. Fair enough.
>
> # Task
>
> Given an array of integers, remove the smallest value. Do not mutate the original array/list. If there are multiple elements with the same value, remove the one with a lower index. If you get an empty array/list, return an empty array/list.
>
> Don't change the order of the elements that are left.
>
> ### Examples
>
> ```
> remove_smallest([1,2,3,4,5]) = [2,3,4,5]
> remove_smallest([5,3,2,1,4]) = [5,3,2,4]
> remove_smallest([2,2,1,2,1]) = [2,2,2,1]
> ```

### 5. Stop gninnipS My sdroW!

```python
def spin_words(sentence):
    li = sentence.split()
    li_re = []
    for i in li:
        if len(i)>=5:
            li_re.append(i[::-1])
        else:
            li_re.append(i)
    return " ".join(li_re)
```

> Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.
>
> Examples:
>
> `spinWords( "Hey fellow warriors" )` => returns "Hey wollef sroirraw" 
> `spinWords( "This is a test")` => returns "This is a test" 
> `spinWords( "This is another test" )`=> returns "This is rehtona test"

### 6. Descending Order

```python
def Descending_Order(num):
    b = list(str(num))
    b.sort()
    return int("".join(b[::-1]))
```

> Your task is to make a function that can take any non-negative integer as a argument and return it with it's digits in descending order. Essentially, rearrange the digits to create the highest possible number.
>
> ### Examples:
>
> Input: `21445` Output: `54421`
>
> Input: `145263` Output: `654321`
>
> Input: `1254859723` Output: `9875543221`

### 7.



