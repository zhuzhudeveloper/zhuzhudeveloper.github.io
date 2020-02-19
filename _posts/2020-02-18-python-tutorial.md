#Python Tutorial
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



