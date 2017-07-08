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

### 7.Sum of the first nth term of Series

```python
def series_sum(n):
    return "%.2f" % sum([1/(i*3+1) for i in range(n)])
```

> **Task:**
>
> Your task is to write a function which returns the sum of following series upto nth term(parameter).
>
> ```
> Series: 1 + 1/4 + 1/7 + 1/10 + 1/13 + 1/16 +...
> ```
>
> **Rules:**
>
> - You need to round the answer up to 2 decimal places and return it as String.
> - If the given value is 0 then it should return 0.00
> - You will only be given Natural Numbers as arguments.
>
> **Examples:**
>
> ```
> SeriesSum(1) => 1 = "1"
> SeriesSum(2) => 1 + 1/4 = "1.25"
> SeriesSum(5) => 1 + 1/4 + 1/7 + 1/10 + 1/13 = "1.57"
> ```
>
> **NOTE**: In PHP the function is called `series_sum()`.

### 8. Breaking chocolate problem

```python
def breakChocolate(n, m):
    return n*m-1 if n>0 and m>0 else 0
```

> Your task is to split the chocolate bar of given dimension `n` x `m` into small squares. Each square is of size 1x1 and unbreakable. Implement a function that will return minimum number of breaks needed.
>
> For example if you are given a chocolate bar of size `2` x `1` you can split it to single squares in just one break, but for size `3` x `1` you must do two breaks.
>
> If input data is invalid you should return 0 (as in no breaks are needed if we do not have any chocolate to split). Input will always be a non-negative integer.

### 9. Human Readable Time

```python
def make_readable(seconds):
    # Do something
    hours = seconds//3600
    rests = seconds % 3600
    mins = rests // 60
    secs = rests % 60
    return "{}:{}:{}".format(str(hours).rjust(2,"0"), str(mins).rjust(2,"0"), str(secs).rjust(2,"0"))
```

> Write a function, which takes a non-negative integer (seconds) as input and returns the time in a human-readable format (`HH:MM:SS`)
>
> - `HH` = hours, padded to 2 digits, range: 00 - 99
> - `MM` = minutes, padded to 2 digits, range: 00 - 59
> - `SS` = seconds, padded to 2 digits, range: 00 - 59
>
> The maximum time never exceeds 359999 (`99:59:59`)
>
> You can find some examples in the test fixtures.

### 10. Does my number look big in this? 

```python
def narcissistic( value ):
    v = list(str(value))
    if sum([int(i)**len(v) for i in v]) == value:
        return True
    else:
        return False
```

> A [Narcissistic Number](https://en.wikipedia.org/wiki/Narcissistic_number) is a number which is the sum of its own digits, each raised to the power of the number of digits.
>
> For example, take 153 (3 digits):
>
> ```
>     1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153
> ```
>
> and 1634 (4 digits):
>
> ```
>     1^4 + 6^4 + 3^4 + 4^4 = 1 + 1296 + 81 + 256 = 1634
>
> ```
>
> The Challenge:
>
> Your code must return **true or false** depending upon whether the given number is a Narcissistic number.
>
> Error checking for text strings or other invalid inputs is not required, only valid integers will be passed into the function.

### 11. Moving Zeros To the End

```python
def move_zeros(array):
    return [i for i in array if i != 0 or str(i) == "False"] + [i for i in array if i == 0 and str(i) != "False"]
```

> Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.
>
> ```
> move_zeros([false,1,0,1,2,0,1,3,"a"]) # returns[false,1,1,2,1,3,"a",0,0]
> ```

### 12. 

``` python
def sum_dig_pow(a, b): # range(a, b + 1) will be studied by the function
    return [i for i in range(a, b+1) if sum(int(x)**(y+1) for y, x in enumerate(str(i))) == i]
```

> The number `89` is the first integer with more than one digit that fulfills the property partially introduced in the title of this kata. What's the use of saying "Eureka"? Because this sum gives the same number.
>
> In effect: `89 = 8^1 + 9^2`
>
> The next number in having this property is `135`.
>
> See this property again: `135 = 1^1 + 3^2 + 5^3`
>
> We need a function to collect these numbers, that may receive two integers `a`, `b` that defines the range `[a, b]` (inclusive) and outputs a list of the sorted numbers in the range that fulfills the property described above.
>
> Let's see some cases:
>
> ```
> sum_dig_pow(1, 10) == [1, 2, 3, 4, 5, 6, 7, 8, 9]
>
> sum_dig_pow(1, 100) == [1, 2, 3, 4, 5, 6, 7, 8, 9, 89]
>
> ```
>
> If there are no numbers of this kind in the range [a, b] the function should output an empty list.
>
> ```
> sum_dig_pow(90, 100) == []
> ```



