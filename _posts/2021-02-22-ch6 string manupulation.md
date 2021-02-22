-----------------------------
title: ch6 문자열 조작
tag: algorithm
-----------------------------

# 6장 문자열 조작

## 1. 유효한 팰린드롬

팰린드롬은 영문자 숫자만 취급, : ! 이런거 안취급

### 예제 1

[leetcode 125]("https://leetcode.com/problems/valid-palindrome/")



```python
input_str = "A man, a plan, a canal: Panama"
# for 문 풀이

def solution(input_str):
    t1 = datetime.datetime.now()
    wanted_list = []
    for char in input_str:
        if char.isalnum(): # 만약 문자나 숫자가 아니면
            wanted_list.append(char.lower()) # 다 소문자로

    for _ in range(len(wanted_list)//2): # len() 는  O(1)
        if wanted_list.pop() != wanted_list.pop(0):
            t2 = datetime.datetime.now()
            print(t2-t1)
            return False
    t2 = datetime.datetime.now()   
    print(t2 - t1)
    return True

solution(input_str) # 44ms
```

    0:00:00
    




    True




```python
# deque를 활용해 빠르게 해보자

import collections
#print(collections.__all__)

def solutions(s:str)->bool:
    filter_str = []
    for char in s:
        if char.isalnum():
            filter_str.append(char.lower())
    deque_str = collections.deque(filter_str)
    for _ in range(len(filter_str)//2):
        if deque_str.pop() != deque_str.popleft():
            return False
    return True

solutions(input_str) # 이게 5배 더 빠름
```




    True




```python
# 슬라이싱 사용해보자 []
import re

def solutionss(s:str)->bool:
    s = s.lower()
    s = re.sub("[^a-z0-9]","",s) # re.sub(바꾸길 원하는 문자, 바뀐후 문자, 대상 문자열)
    if s == s[::-1]:
        return False
    return True
solutionss(input_str) # 데큐보다 2배 빠름
```




    False




```python
deque.__dict__
```




    mappingproxy({'__repr__': <slot wrapper '__repr__' of 'collections.deque' objects>,
                  '__hash__': None,
                  '__getattribute__': <slot wrapper '__getattribute__' of 'collections.deque' objects>,
                  '__lt__': <slot wrapper '__lt__' of 'collections.deque' objects>,
                  '__le__': <slot wrapper '__le__' of 'collections.deque' objects>,
                  '__eq__': <slot wrapper '__eq__' of 'collections.deque' objects>,
                  '__ne__': <slot wrapper '__ne__' of 'collections.deque' objects>,
                  '__gt__': <slot wrapper '__gt__' of 'collections.deque' objects>,
                  '__ge__': <slot wrapper '__ge__' of 'collections.deque' objects>,
                  '__iter__': <slot wrapper '__iter__' of 'collections.deque' objects>,
                  '__init__': <slot wrapper '__init__' of 'collections.deque' objects>,
                  '__bool__': <slot wrapper '__bool__' of 'collections.deque' objects>,
                  '__len__': <slot wrapper '__len__' of 'collections.deque' objects>,
                  '__add__': <slot wrapper '__add__' of 'collections.deque' objects>,
                  '__mul__': <slot wrapper '__mul__' of 'collections.deque' objects>,
                  '__rmul__': <slot wrapper '__rmul__' of 'collections.deque' objects>,
                  '__getitem__': <slot wrapper '__getitem__' of 'collections.deque' objects>,
                  '__setitem__': <slot wrapper '__setitem__' of 'collections.deque' objects>,
                  '__delitem__': <slot wrapper '__delitem__' of 'collections.deque' objects>,
                  '__contains__': <slot wrapper '__contains__' of 'collections.deque' objects>,
                  '__iadd__': <slot wrapper '__iadd__' of 'collections.deque' objects>,
                  '__imul__': <slot wrapper '__imul__' of 'collections.deque' objects>,
                  '__new__': <function deque.__new__(*args, **kwargs)>,
                  'append': <method 'append' of 'collections.deque' objects>,
                  'appendleft': <method 'appendleft' of 'collections.deque' objects>,
                  'clear': <method 'clear' of 'collections.deque' objects>,
                  '__copy__': <method '__copy__' of 'collections.deque' objects>,
                  'copy': <method 'copy' of 'collections.deque' objects>,
                  'count': <method 'count' of 'collections.deque' objects>,
                  'extend': <method 'extend' of 'collections.deque' objects>,
                  'extendleft': <method 'extendleft' of 'collections.deque' objects>,
                  'index': <method 'index' of 'collections.deque' objects>,
                  'insert': <method 'insert' of 'collections.deque' objects>,
                  'pop': <method 'pop' of 'collections.deque' objects>,
                  'popleft': <method 'popleft' of 'collections.deque' objects>,
                  '__reduce__': <method '__reduce__' of 'collections.deque' objects>,
                  'remove': <method 'remove' of 'collections.deque' objects>,
                  '__reversed__': <method '__reversed__' of 'collections.deque' objects>,
                  'reverse': <method 'reverse' of 'collections.deque' objects>,
                  'rotate': <method 'rotate' of 'collections.deque' objects>,
                  '__sizeof__': <method '__sizeof__' of 'collections.deque' objects>,
                  'maxlen': <attribute 'maxlen' of 'collections.deque' objects>,
                  '__doc__': 'deque([iterable[, maxlen]]) --> deque object\n\nA list-like sequence optimized for data accesses near its endpoints.'})



### 예제 2 : 문자열 뒤집기

[leetcode 344]("https://leetcode.com/problems/reverse-string/")


```python
input_str = ["h","e","l","l","o"]

# 문자열 슬라이싱 & reverse()

def solution(s: list())->None:
    s.reverse()


def solution(s: list())->None:
    s=s[::-1] #변환 안됨(원래는 되는 디 leet code의 공간 복잡도 O(1)이어야되서 안됨)
    s[:]=s[::-1]

```

    None
    None
    

### 예제 3 : 로그 파일 재정렬

1. 로그의 가장 앞부분은 식별자 이다
2. 문자로 구성된 로그가 숫자 로그보다 앞에 온다
3. 식별자는 순서에 영향을 끼칮 않지만, 문자가 동일한 경우 식별자 순으로 한다
4. 숫자 로그는 입력순

[leetcode 937]("https://leetcode.com/problems/reorder-data-in-log-files/")


```python
logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]

def solution(logs):
    letter = []; digs = []

    for log in logs:
        if "let" in log.split(" ")[0]: 
            letter.append(log)
        else:
            digs.append(log)
    letter.sort(key = lambda x : (x.split()[1:], x.split()[0]))

    return letter + digs
solution(logs) # 위 풀이는 로그가 DIG, LET일때만 가능
```




    ['let1 art can',
     'let3 art zero',
     'let2 own kit dig',
     'dig1 8 1 5 1',
     'dig2 3 6']




```python
def solution(logs):
    letter = []; digs = []

    for log in logs:
        if log.split(" ")[1].isdigit(): 
            digs.append(log)
        else:
            letter.append(log)
    letter.sort(key = lambda x : (x.split()[1:], x.split()[0]))

    return letter + digs
solution(logs) # 이거는 그냥 뒷부분이 숫자인지 판별
```




    ['let1 art can',
     'let3 art zero',
     'let2 own kit dig',
     'dig1 8 1 5 1',
     'dig2 3 6']



### 4. 가장 흔한 단어
[leet code 819]("https://leetcode.com/problems/most-common-word/")

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

Note:

1 <= paragraph.length <= 1000.
0 <= banned.length <= 100.
1 <= banned[i].length <= 10.
* The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)
* paragraph only consists of letters, spaces, or the punctuation symbols !?',;.
* There are no hyphens or hyphenated words.
* Words only consist of letters, never apostrophes or other punctuation symbols.



```python
# Counter 가지고 풀기

from collections import Counter
import re

paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
para2 = "a, a, a, a, b,b,b,c, c"
banned = ["hit"]

def solution(para,banned):
        para = re.sub("[!?';.,]"," ",para.lower()) # 소문자로 & 저 값들을 " "로 바꿈
        para = para.split(" ") # 공백이 3개면 중간이 남음 그래서 ""로 카운터 생김
        c = Counter(para)
        c.__delitem__("")

        for i in banned:
            c.__delitem__(i)

        return c.most_common(1)[0][0]



solution(para2,banned)
```

    ['a', '', 'a', '', 'a', '', 'a', '', 'b', 'b', 'b', 'c', '', 'c']
    Counter({'a': 4, 'b': 3, 'c': 2})
    




    'a'




```python
Counter.__dict__
```




    mappingproxy({'__module__': 'collections',
                  '__doc__': "Dict subclass for counting hashable items.  Sometimes called a bag\n    or multiset.  Elements are stored as dictionary keys and their counts\n    are stored as dictionary values.\n\n    >>> c = Counter('abcdeabcdabcaba')  # count elements from a string\n\n    >>> c.most_common(3)                # three most common elements\n    [('a', 5), ('b', 4), ('c', 3)]\n    >>> sorted(c)                       # list all unique elements\n    ['a', 'b', 'c', 'd', 'e']\n    >>> ''.join(sorted(c.elements()))   # list elements with repetitions\n    'aaaaabbbbcccdde'\n    >>> sum(c.values())                 # total of all counts\n    15\n\n    >>> c['a']                          # count of letter 'a'\n    5\n    >>> for elem in 'shazam':           # update counts from an iterable\n    ...     c[elem] += 1                # by adding 1 to each element's count\n    >>> c['a']                          # now there are seven 'a'\n    7\n    >>> del c['b']                      # remove all 'b'\n    >>> c['b']                          # now there are zero 'b'\n    0\n\n    >>> d = Counter('simsalabim')       # make another counter\n    >>> c.update(d)                     # add in the second counter\n    >>> c['a']                          # now there are nine 'a'\n    9\n\n    >>> c.clear()                       # empty the counter\n    >>> c\n    Counter()\n\n    Note:  If a count is set to zero or reduced to zero, it will remain\n    in the counter until the entry is deleted or the counter is cleared:\n\n    >>> c = Counter('aaabbc')\n    >>> c['b'] -= 2                     # reduce the count of 'b' by two\n    >>> c.most_common()                 # 'b' is still in, but its count is zero\n    [('a', 3), ('c', 1), ('b', 0)]\n\n    ",
                  '__init__': <function collections.Counter.__init__(self, iterable=None, /, **kwds)>,
                  '__missing__': <function collections.Counter.__missing__(self, key)>,
                  'most_common': <function collections.Counter.most_common(self, n=None)>,
                  'elements': <function collections.Counter.elements(self)>,
                  'fromkeys': <classmethod at 0x2a21c316eb0>,
                  'update': <function collections.Counter.update(self, iterable=None, /, **kwds)>,
                  'subtract': <function collections.Counter.subtract(self, iterable=None, /, **kwds)>,
                  'copy': <function collections.Counter.copy(self)>,
                  '__reduce__': <function collections.Counter.__reduce__(self)>,
                  '__delitem__': <function collections.Counter.__delitem__(self, elem)>,
                  '__repr__': <function collections.Counter.__repr__(self)>,
                  '__add__': <function collections.Counter.__add__(self, other)>,
                  '__sub__': <function collections.Counter.__sub__(self, other)>,
                  '__or__': <function collections.Counter.__or__(self, other)>,
                  '__and__': <function collections.Counter.__and__(self, other)>,
                  '__pos__': <function collections.Counter.__pos__(self)>,
                  '__neg__': <function collections.Counter.__neg__(self)>,
                  '_keep_positive': <function collections.Counter._keep_positive(self)>,
                  '__iadd__': <function collections.Counter.__iadd__(self, other)>,
                  '__isub__': <function collections.Counter.__isub__(self, other)>,
                  '__ior__': <function collections.Counter.__ior__(self, other)>,
                  '__iand__': <function collections.Counter.__iand__(self, other)>,
                  '__dict__': <attribute '__dict__' of 'Counter' objects>,
                  '__weakref__': <attribute '__weakref__' of 'Counter' objects>})




```python
# list comprehension & counter

def solution(para,banned):
     
    words = [word for word in re.sub(r'[^\w]'," ",para).lower().split() if word not in banned] 
    # ^ : not
    # \w : 단어 문자
    c = Counter(words)
    return c.most_common(1)[0][0]



solution(para2,banned) # 차이는 없음
```




    'a'




```python
# list comprehension & default dict

from collections import defaultdict

def solution(para,banned):
     
    words = [word for word in re.sub(r'[^\w]'," ",para).lower().split() if word not in banned] 
    # ^ : not
    # \w : 단어 문자
    count = defaultdict(int)
    for word in words:
        count[word] += 1
    return max(count, key = count.get)



solution(para2,banned) # 이게 더 빠름 / 메모리 동일

```




    'a'



### 5. 그룹 애너그램

[leet code 49]("https://leetcode.com/problems/group-anagrams/")

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:

Input: strs = [""]
Output: [[""]]

Example 3:

Input: strs = ["a"]
Output: [["a"]]
 

Constraints:

1 <= strs.length <= 104
0 <= strs[i].length <= 100
strs[i] consists of lower-case English letters.


```python
# 내 풀이

strs = ["eat","tea","tan","ate","nat","bat"]
#strs = ["a"]
strs = ["","","b"]
import collections

def solution(strs):
    arr = collections.defaultdict(list)
    for word in strs:
        a ="".join(sorted(list(word)))
        arr[a].append(word)l,
    return arr.values()

solution(strs)
```




    dict_values([['', ''], ['b']])




```python
# 책 풀이
strs = ["eat","tea","tan","ate","nat","bat"]
def solution(strs):
    anagrams = collections.defaultdict(list)
    for word in strs:
        anagrams[''.join(sorted(word))].append(word)
    return anagrams.values()

solution(strs)
```




    dict_values([['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']])



### 6. 가장 긴 팰린드롬 부분 문자열

[leet code 5]("https://leetcode.com/problems/longest-palindromic-substring/")

Given a string s, return the longest palindromic substring in s.

 

Example 1:

Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Example 2:

Input: s = "cbbd"
Output: "bb"

Example 3:

Input: s = "a"
Output: "a"

Example 4:

Input: s = "ac"
Output: "a"
 

Constraints:

1 <= s.length <= 1000
s consist of only digits and English letters (lower-case and/or upper-case),


```python
# idea 1 : 그냥 정의 대로
s = "babad"
#s = "cbbd"
s = "aacabdkacaa"
def solution(s):
        answer = []

        def find_pelindrome(words):
            if words != words[::-1]:
                    return False
            return True

        for i in range(len(s)):

            for j in range(len(s)-1,i,-1):

                if s[j] == s[i] :
                    #print(s[i:j+1])

                    if find_pelindrome(s[i:j+1]) == True: 
                        answer.append(s[i:j+1])
                        break

        if len(answer) == 0:
            return s[0]
        else:
            return sorted(answer, key=len, reverse = True)[0]
        
solution(s)                
```




    'aca'




```python
# 조금 바꿔보자

s = "babad"
#s = "cbbd"
s = "aacabdkacaa"

def solution(s):

answer = [""]
        
        if  s == s[::-1] :
            return s
        if len(s) <= 2:
            return s[0]
        
        for i in range(len(s)):
            for j in range(len(s)-1,i,-1):
                if s[j] == s[i] :
                    test = s[i:j+1]
                    if test == test[::-1]: 
                        answer.append(test)
                        break
        if answer == [""]:
            return s[0]
        
        return max(answer, key=len)
    
solution(s) # 첫 답안 보다는 좋음 그래도 2개의 포인터로 하는게 10배나 좋음 
```




    'aca'




```python
# 몇개의 장소에서 시작............... 좀더 생각해야됨
# 코딩테스트의 잘못된 ㅇ예시로 보자
s = "babad"
#s = "cbbd"
s = "aacabdkacaa"
def solution(s):

    answer = []
    two = False; three = False;
    two_list = []
    three_list = []
    
    def find_pelindrome(words):
        if words != words[::-1]:
                return False
        return True
    
    for i in range(len(s)-2):
        if find_pelindrome(s[i:i+2]) == True:
            two = True
            two_list.append(i)
            
    for i in range(len(s)-3):
        if find_pelindrome(s[i:i+3]) == True:
            three = True
            three_list.append(i)
    
    if two == False:
        if three = False:
            return s[0]

    for num in two_list:
        if (num
        if len(answer) == 0:
            return s[0]
        else:
            return sorted(answer, key=len, reverse = True)[0]
        
solution(s)                
```


      File "<ipython-input-254-d61611fa4c4f>", line 28
        if three = False:
                 ^
    SyntaxError: invalid syntax
    



```python
def solution(s):
    result = ""
    def expand(left,right):
        while left >=0 and right <= len(s) and s[left] == s[right-1]:
            left -=1
            right +=1
        return s[left+1:right-1]
    
    if len(s)<2 or s == s[::-1]:
        return s
    
    for i in range(len(s)-1):
        result = max(result,expand(i,i+1), expand(i,i+2), key = len)
    return result
solution(s)
```




    'bb'




```python

```
