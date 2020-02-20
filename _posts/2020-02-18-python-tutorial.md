---
category: tutorial
order: 6
tags: python
---
## Python Tutorial
### Input and Print
```
name = input('Please enter')
print("10*10=", 10*10, 'Your name is', name)
```

### Data Types
#### String
Use r'' to avoid Escape Letter and show raw string
```
>>> print('\\\t\\')
\      \
>>> print(r'\\\t\\')
\\\t\\
>>> len('ABC')
3
```
#### True, False, and, or, not, None

### Division
/ float division            
// floor division              
% mod      

### Unicode
```
>>> ord('A')
65
>>> char(66)
'B'
```      

### Formative Sentence
Use % (Escape letter %%)
```
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```
%d: Integer    
%f: Float        
%s: String         
%x: Hex Number

### List
```
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']
>>> len(classmates)
3
>>> classmates[0]
'Michael'
>>> classmates[-1]
'Tracy'
>>> classmates.append('Adam')
>>> classmates
['Michael', 'Bob', 'Tracy', 'Adam']
>>> classmates.insert(1, 'Jack')
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
>>> classmates.pop()
'Adam'
>>> classmates
['Michael', 'Jack', 'Bob', 'Tracy']
>>> classmates.pop(1)
'Jack'
>>> classmates
['Michael', 'Bob', 'Tracy']
>>> classmates[1] = 'Sarah'
>>> classmates
['Michael', 'Sarah', 'Tracy']
>>> L = ['Apple', 123, True]
s = ['python', 'java', ['asp', 'php'], 'scheme']
```
### Tuple
Tuple can't be changed.
```
>>> t = (1, 2)
>>> t
(1, 2)
```
When there is only one element, comma is needed.
```
>>> t = (1,)
>>> t
(1,)
```
Following case, tuple is not changed, but list changed.
```
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])
```
### Condition
```
age = 3
if age >= 18:
    print('your age is', age)
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```
### Loop
```
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```
```
sum = 0
for x in range(101):
    sum = sum + x
print(sum)
```
```
n = 1
while n <= 100:
    if n > 10: 
        break
    print(n)
    n = n + 1
print('END')
```
continue also can be used.    
### Dictionary
```
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```
Check if the element exists
```
>>> 'Thomas' in d
False
>>> d.get('Thomas') //The return value is none.
>>> d.get('Thomas', -1)
-1
```
```
>>> d.pop('Bob')
75
>>> d
{'Michael': 95, 'Tracy': 85}
```
Key is unchangable, so a list cannot be a key.      
### Set
```
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.add(4)
>>> s
{1, 2, 3, 4}
>>> s.remove(4)
>>> s
{1, 2, 3}
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```
### Collection.Counter
#### Definition
```
>>> c = Counter()  
>>> c = Counter('gallahad') 
>>> c = Counter({'a': 4, 'b': 2})
>>> c = Counter(a=4, b=2) 
```
#### Update and Substract
```
>>> c = Counter('which')
>>> c.update('witch')  # 使用另一个iterable对象更新
>>> c['h']
3
>>> d = Counter('watch')
>>> c.update(d)  # 使用另一个Counter对象更新
>>> c['h']
4
>>> c = Counter('which')
>>> c.subtract('witch')  # 使用另一个iterable对象更新
>>> c['h']
1
>>> d = Counter('watch')
>>> c.subtract(d)  # 使用另一个Counter对象更新
>>> c['a']
-1
```
#### del
```
>>> c = Counter("abcdcba")
>>> c
Counter({'a': 2, 'c': 2, 'b': 2, 'd': 1})
>>> c["b"] = 0
>>> c
Counter({'a': 2, 'c': 2, 'd': 1, 'b': 0})
>>> del c["a"]
>>> c
Counter({'c': 2, 'b': 2, 'd': 1})
```
#### elements()
```
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> list(c.elements())
['a', 'a', 'a', 'a', 'b', 'b'] #no order
```
#### most_common([])
```
>>> c = Counter('abracadabra')
>>> c.most_common()
[('a', 5), ('r', 2), ('b', 2), ('c', 1), ('d', 1)]
>>> c.most_common(3)
[('a', 5), ('r', 2), ('b', 2)]
```
#### copy
```
>>> c = Counter("abcdcba")
>>> c
Counter({'a': 2, 'c': 2, 'b': 2, 'd': 1})
>>> d = c.copy()
>>> d
Counter({'a': 2, 'c': 2, 'b': 2, 'd': 1})
```
#### Calculations
```
>>> c = Counter(a=3, b=1)
>>> d = Counter(a=1, b=2)
>>> c + d  # c[x] + d[x]
Counter({'a': 4, 'b': 3})
>>> c - d  # subtract
Counter({'a': 2})
>>> c & d  # intersection:  min(c[x], d[x])
Counter({'a': 1, 'b': 1})
>>> c | d  # union:  max(c[x], d[x])
Counter({'a': 3, 'b': 2})
```
#### Others
```
sum(c.values())  # 所有计数的总数
c.clear()  # 重置Counter对象，注意不是删除
list(c)  # 将c中的键转为列表
set(c)  # 将c中的键转为set
dict(c)  # 将c中的键值对转为字典
c.items()  # 转为(elem, cnt)格式的列表
Counter(dict(list_of_pairs))  # 从(elem, cnt)格式的列表转换为Counter类对象
c.most_common()[:-n:-1]  # 取出计数最少的n-1个元素
c += Counter()  # 移除0和负值
```
