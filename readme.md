# The records of codewars using python

### 25. Complementary DNA

```python
pairs = {'A':'T','T':'A','C':'G','G':'C'}
def DNA_strand(dna):
    return ''.join([pairs[x] for x in dna])
```

> Deoxyribonucleic acid (DNA) is a chemical found in the nucleus of cells and carries the "instructions" for the development and functioning of living organisms.
>
> If you want to know more [http://en.wikipedia.org/wiki/DNA](http://en.wikipedia.org/wiki/DNA)
>
> In DNA strings, symbols "A" and "T" are complements of each other, as "C" and "G". You have function with one side of the DNA (string, except for Haskell); you need to get the other complementary side. DNA strand is never empty or there is no DNA at all (again, except for Haskell).
>
> ```
> DNA_strand ("ATTGC") # return "TAACG"
> DNA_strand ("GTAT") # return "CATA"
> ```

### 24. Make a spiral

```python
def spiralize(size):
    spiral = [[0 for i in range(size)] for j in range(size)]
    if size == 1:
        return [[1]]
    if size == 0:
        return []
    for n in range(size):
        spiral[0][n] = 1
        spiral[size-1][n] =1
        spiral[n][size-1] =1
        spiral[n][0] = 1
    spiral[1][0] = 0
    if size < 5:
        return spiral
    spiral[2][1] = 1
    x, y = 2, 1
    while True:
        if spiral[x][y-1] == 1:
            if spiral[x][y+2] == 0:
                spiral[x][y+1] =1
                y += 1
            else:
                if spiral[x+2][y] ==0:
                    spiral[x+1][y] = 1
                    x += 1
                    if spiral[x+2][y] == 1:
                        break
                else:
                    break
        elif spiral[x-1][y] == 1:
            if spiral[x+2][y] == 0:
                spiral[x+1][y] = 1
                x += 1
            else:
                if spiral[x][y-2] == 0:
                    spiral[x][y-1] =1
                    y -= 1
                    if spiral[x][y-2] == 1:
                        break
                else:
                    break
        elif spiral[x][y+1] == 1:
            if spiral[x][y-2] == 0:
                spiral[x][y-1] = 1
                y-= 1
            else:
                if spiral[x-2][y] == 0:
                    spiral[x-1][y] =1
                    x -= 1
                    if spiral[x-2][y] ==1:
                        break
                else:
                    break
        elif spiral[x+1][y] == 1:
            if spiral[x-2][y] == 0:
                spiral[x-1][y] = 1
                x -= 1
            else:
                if spiral[x][y+2] == 0:
                    spiral[x][y+1] =1
                    y += 1
                    if spiral[x][y+2] ==1:
                        break
                else:
                    break

    return spira
```

**more clever solution:**

```python
def spiralize(size):
    spiral = [[1]*size for _ in xrange(size)]
    def ok(y, x):
        return y < size and x < size and y >= 0 and x >= 0 and spiral[y][x]
    y, x, dy, dx = 1, -1, 0, 1
    while ok(y + dy, x + dx):
        if ok(y + 2*dy, x + 2*dx):
            y += dy
            x += dx
        else:
            dx, dy = dy*(2*dx-1), dx
        spiral[y][x] = 0
    return spiral
```



> Your task, is to create a NxN spiral with a given `size`.
>
> For example, spiral with size 5 should look like this:
>
> ```
> 00000
> ....0
> 000.0
> 0...0
> 00000
> ```
>
> and with the size 10:
>
> ```
> 0000000000
> .........0
> 00000000.0
> 0......0.0
> 0.0000.0.0
> 0.0..0.0.0
> 0.0....0.0
> 0.000000.0
> 0........0
> 0000000000
> ```
>
> Return value should contain array of arrays, of `0` and `1`, for example for given size `5` result should be:
>
> ```
> [[1,1,1,1,1],[0,0,0,0,1],[1,1,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
>
> ```
>
> Because of the edge-cases for tiny spirals, the size will be at least 5.
>
> General rule-of-a-thumb is, that the snake made with '1' cannot touch to itself.

### 23. First non-repeating letter 

```python
def first_non_repeating_letter(string):
    str_lower = string.lower()
    for i, j in enumerate(str_lower):
        if str_lower.count(j) == 1:
            return string[i]
            
    return ""
```

> Write a function named `firstNonRepeatingCharacter` that takes a string input, and returns the first character that is not repeated anywhere in the string.
>
> For example, if given the input `'stress'`, the function should return `'t'`, since the letter *t* only occurs once in the string, and occurs first in the string.
>
> As an added challenge, upper- and lowercase letters are considered the **same character**, but the function should return the correct case for the initial letter. For example, the input`'sTreSS'` should return `'T'`.
>
> If a string contains *all repeating characters*, it should return the empty string (`""`).

### 22. Twice linear

**my solutions(time out when n is large):**

```python
def dbl_linear(n):
    u = set([1])
    for i in range(n):
        x = min(u)
        u.update([x*2 + 1, x*3 +1])
        u.remove(x)
    return min(u)
```

**or**

```python
def dbl_linear(n):
    u = [1]
    for i in range(n):
        u.append(u[0]*2 +1)
        u.append(u[0]*3 +1)
        del u[0]
        u.sort()
    return u[0]
```

**the author's solution:**

```python
from collections import deque
def dbl_linear(n):
    h = 1; cnt = 0; q2, q3 = deque([]), deque([])
    while True:
        if (cnt >= n):
            return h
        q2.append(2 * h + 1)
        q3.append(3 * h + 1)
        h = min(q2[0], q3[0])
        if h == q2[0]: h = q2.popleft()
        if h == q3[0]: h = q3.popleft()
        cnt += 1
```

> Consider a sequence `u` where u is defined as follows:
>
> 1. The number `u(0) = 1` is the first one in `u`.
> 2. For each `x` in `u`, then `y = 2 * x + 1` and `z = 3 * x + 1` must be in `u` too.
> 3. There are no other numbers in `u`.
>
> Ex: `u = [1, 3, 4, 7, 9, 10, 13, 15, 19, 21, 22, 27, ...]`
>
> 1 gives 3 and 4, then 3 gives 7 and 10, 4 gives 9 and 13, then 7 gives 15 and 22 and so on...
>
> \#Task: Given parameter `n` the function `dbl_linear` (or dblLinear...) returns the element `u(n)` of the ordered (with <) sequence `u`.
>
> \#Example: `dbl_linear(10) should return 22`
>
> \#Note: Focus attention on efficiency

### 21.Valid Braces 

```python
def validBraces(string):
    a = list(string)
    while len(a)>0:
        n = 0
        for i in range(len(a)-1):
            if (a[i] == "(" and a[i+1] == ")") or (a[i] == "[" and a[i+1] == "]") or (a[i] == "{" and a[i+1] == "}"):
                del a[i]
                del a[i]
                n += 1
                break
        if n == 0:
            return False
    if len(a) == 0:
        return True
```

**or**

```python
def validBraces(s):
  while '{}' in s or '()' in s or '[]' in s:
      s=s.replace('{}','')
      s=s.replace('[]','')
      s=s.replace('()','')
  return s==''
```

> Write a function called `validBraces` that takes a string of braces, and determines if the order of the braces is valid. `validBraces` should return true if the string is valid, and false if it's invalid.
>
> This Kata is similar to the Valid Parentheses Kata, but introduces four new characters. Open and closed brackets, and open and closed curly braces. Thanks to @arnedag for the idea!
>
> All input strings will be nonempty, and will only consist of open parentheses '(' , closed parentheses ')', open brackets '[', closed brackets ']', open curly braces '{' and closed curly braces '}'.
>
> **What is considered Valid?** A string of braces is considered valid if all braces are matched with the correct brace. 
> For example:
> '(){}[]' and '([{}])' would be considered valid, while '(}', '[(])', and '[({})](]' would be considered invalid.
>
> **Examples:** 
> `validBraces( "(){}[]" )` => returns true 
> `validBraces( "(}" )` => returns false 
> `validBraces( "[(])" )` => returns false 
> `validBraces( "([{}])" )` => returns true 

### 20. Convert string to camel case

```python
import re

def to_camel_case(text):
    li = re.split("-|_", text)
    return li[0] + "".join([x.title() for x in li[1:]])
```



> Complete the method/function so that it converts dash/underscore delimited words into camel casing. The first word within the output should be capitalized only if the original word was capitalized.
>
> Examples:
>
> ```
> # returns "theStealthWarrior"
> to_camel_case("the-stealth-warrior") 
>
> # returns "TheStealthWarrior"
> to_camel_case("The_Stealth_Warrior")
> ```

### 19. Two Joggers:

```python
def nbr_of_laps(x, y):
    for i in range(min(x,y),0,-1):
        if x%i == 0 and y%i ==0:
            return [y/i, x/i]
```



> ## Description
>
> Bob and Charles are meeting for their weekly jogging tour. They both start at the same spot called "Start" and they each run a different lap, which may (or may not) vary in length. Since they know each other for a long time already, they both run at the exact same speed.
>
> ## Illustration
>
> Example where Charles (dashed line) runs a shorter lap than Bob:
>
> ![Example laps](http://www.haan.lu/files/7713/8338/6140/jogging.png)
>
> ## Task
>
> Your job is to complete the function **nbrOfLaps(x, y)** that, given the length of the laps for Bob and Charles, finds the number of laps that each jogger has to complete before they meet each other again, at the same time, at the start.
>
> The function takes two arguments:
>
> 1. The length of Bob's lap (larger than 0)
> 2. The length of Charles' lap (larger than 0)
>
> The function should return an array containing exactly two numbers:
>
> 1. The first number is the number of laps that Bob has to run
> 2. The second number is the number of laps that Charles has to run
>
> Examples
>
> ```
> nbr_of_laps(5, 3) # returns [3,5]
> nbr_of_laps(4, 6); # returns [3, 2]
> ```

### 18. Primes in numbers

```python
def primeFactors(n):
    ret = ''
    for i in xrange(2, n + 1):
        num = 0
        while(n % i == 0):
            num += 1
            n /= i
        if num > 0:
            ret += '({}{})'.format(i, '**%d' % num if num > 1 else '')
        if n == 1:
            return ret
```

> Given a positive number n > 1 find the prime factor decomposition of n. The result will be a string with the following form :
>
> ```
>  "(p1**n1)(p2**n2)...(pk**nk)"
>
> ```
>
> with the p(i) in increasing order and n(i) empty if n(i) is 1.
>
> ```
> Example: n = 86240 should return "(2**5)(5)(7**2)(11)"
> ```

### 17. Vector class

```python
from math import sqrt
import operator as op
from itertools import imap

class Vector:
  # TODO: Finish the Vector class.
  def __init__(self, array=[]):
    self.__data = array
  
  def __len__(self):
    return len(self.__data)
    
  def __iter__(self):
    return iter(self.__data)
    
  def __getitem__(self, i):
    return self.__data[i]
    
  def check_length(f):
    def wrapper(self, other):
      if len(self) != len(other):
        raise ValueError()
      return f(self, other)
    return wrapper
  
  @check_length
  def add(self, other):
    res = Vector(map(op.add, self, other))
    return res
  
  @check_length
  def subtract(self, other):
    res = Vector(map(op.sub, self, other))
    return res
    
  @check_length  
  def dot(self, other):
    res = reduce(op.add, imap(op.mul, self, other))
    return res
    
  def norm(self):
    return sqrt(self.dot(self))
    
  def equals(self, other):
    if len(self) != len(other):
      return False
    return all(map(op.eq, self, other))
    
  def __str__(self):
    return '(%s)' % ','.join(str(x) for x in self.__data)
```

> Create a Vector object that supports addition, subtraction, dot products, and norms. So, for example:
>
> ```
> a = Vector([1,2,3])
> b = Vector([3,4,5])
> c = Vector([5,6,7,8])
> a.add(b) # should return Vector([4,6,8])
> a.subtract(b) # should return Vector([-2,-2,-2])
> a.dot(b) # should return 1*3+2*4+3*5 = 26
> a.norm() # should return sqrt(1^2+2^2+3^2)=sqrt(14)
> a.add(c) # raises an exception
>
> ```
>
> If you try to add, subtract, or dot two vectors with different lengths, **you must throw an error**!
>
> Also provide:
>
> - a toString function, so that using the vectors from above, `a.toString() === '(1,2,3)'` (in Python, this is a `__str__` method, so that `str(a) == '(1,2,3)'`)
> - an equals function, so that two vectors who have the same components are equal
>
> The test cases will utilize the user-provided `equals` method.

### 16. Regex Password Validation

```python
regex="^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])[a-zA-Z0-9]{6,}$"
```

**or**

```python
from re import compile, VERBOSE

regex = compile("""
^              # begin word
(?=.*?[a-z])   # at least one lowercase letter
(?=.*?[A-Z])   # at least one uppercase letter
(?=.*?[0-9])   # at least one number
[A-Za-z\d]     # only alphanumeric
{6,}           # at least 6 characters long
$              # end word
""", VERBOSE)
```

> You need to write regex that will validate a password to make sure it meets the following criteria:
>
> - At least six characters long
> - contains a lowercase letter
> - contains an uppercase letter
> - contains a number
>
> Valid passwords will only be alphanumeric characters.

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

> **The museum of incredible dull things**
>
> The museum of incredible dull things wants to get rid of some exhibitions. Miriam, the interior architect, comes up with a plan to remove the most boring exhibitions. She gives them a rating, and then removes the one with the lowest rating.
>
> However, just as she finished rating all exhibitions, she's off to an important fair, so she asks you to write a program that tells her the ratings of the items after one removed the lowest one. Fair enough.
>
> **Task**
>
> Given an array of integers, remove the smallest value. Do not mutate the original array/list. If there are multiple elements with the same value, remove the one with a lower index. If you get an empty array/list, return an empty array/list.
>
> Don't change the order of the elements that are left.
>
> **Examples**
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

### 13. Peter, the baker

```python
def cakes(recipe, available):
    return min([available.get(x,0)//y for x,y in recipe.items()])
```



> Pete likes to bake some cakes. He has some recipes and ingredients. Unfortunately he is not good in maths. Can you help him to find out, how many cakes he could bake considering his recipes?
>
> Write a function `cakes()`, which takes the recipe (object) and the available ingredients (also an object) and returns the maximum number of cakes Pete can bake (integer). For simplicity there are no units for the amounts (e.g. 1 lb of flour or 200 g of sugar are simply 1 or 200). Ingredients that are not present in the objects, can be considered as 0.
>
> Examples:
>
> ```
> # must return 2
> cakes({flour: 500, sugar: 200, eggs: 1}, {flour: 1200, sugar: 1200, eggs: 5, milk: 200})
> # must return 0
> cakes({apples: 3, flour: 300, sugar: 150, milk: 100, oil: 100}, {sugar: 500, flour: 2000, milk: 2000})
> ```

### 14. Is a number prime?

```python
def is_prime(num):
    if num <2:
        return False
    else:
        for i in range(2,num):
            if num%i ==0:
                return False
        else:
            return True
```

> **Is Prime**
>
> Define a function `isPrime` that takes one integer argument and returns `true` or `false` depending on if the integer is a prime.
>
> Per Wikipedia, a prime number (or a prime) is a natural number greater than 1 that has no positive divisors other than 1 and itself.
>
> **Example**
>
> ```
> isPrime(5)
> => true
> ```
>
> **Assumptions**
>
> - You can assume you will be given an integer input.
> - You can not assume that the integer will be only positive. You may be given negative numbers.

### 15. Next bigger number with the same digits

```python
def next_bigger(n):
    for i in range(len(str(n))-1):
        if str(n)[i] < str(n)[i+1] and int(str(n)[i])*int(str(n)[i+1]) != 0:
            m = list(str(n))
            m[i+1], m[i] = m[i], m[i+1]
            return int("".join(m))
    else:
        return -1
```

> You have to create a function that takes a positive integer number and returns the next bigger number formed by the same digits:
>
> ```
> next_bigger(12)==21
> next_bigger(513)==531
> next_bigger(2017)==2071
>
> ```
>
> If no bigger number can be composed using those digits, return -1:
>
> ```
> next_bigger(9)==-1
> next_bigger(111)==-1
> next_bigger(531)==-1
> ```