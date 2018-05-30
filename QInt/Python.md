# Python

## Basic

[basic](https://www.dezyre.com/article/100-data-science-in-python-interview-questions-and-answers-for-2018/188)

### Write code to sort a DataFrame in Python in descending order
```
df.sort_values(by=['col1', 'col2'], ascending=False, inplace=True, na_position='first')
```

### Write the code to sort an array in NumPy by the nth column
Using argsort () function this can be achieved. If there is an array X and you would like to sort the nth column then code for this will be 
```
x[x [: n-1].argsort ()]
```

### What is the different between range () and xrange () functions in Python
range () returns a list whereas xrange () returns an object that acts like an iterator for generating numbers on demand.

### How can you randomize the items of a list in place in Python
```
from sklearn.utils import shuffle
shuffle([1,2,3])
```

### How are arguments passed in Python- by reference or by value?
The answer to this question is neither of these because passing semantics in Python are completely different. In all cases, Python passes arguments by value where all values are references to objects.

### Diff between == and is?
is is identity testing, == is equality testing. what happens in your code would be emulated in the interpreter like this:
```
>>> a = 'pub'
>>> b = ''.join(['p', 'u', 'b'])
>>> a == b
True
>>> a is b
False
```
In other words: 'is' is the id(a) == id(b) {its comparing address}

### li = [1,2,3,4] then li[8:] returns?
An empty list []. Most of the people might confuse the answer with an index error because the code is attempting to access a member in the list whose index exceeds the total number of members in the list. The reason being the code is trying to access the slice of a list at a starting index which is greater than the number of members in the list.

### Reverse a string
```
word = 'ABCD'
reverse = word[::-1]
```

## Pandas

### To datetime (apply and lambda too)
```
# to get only the date part
df.Date = pd.to_datetime(df.Date).apply(lambda x: x.date())
```

### Group By
```
# sum or mean etc. is imp if col is not grouped
final1 = finalSched.groupby(by=['Provider','Date', 'Activity'],as_index=False)['mins'].sum()
```

### Col comparisions
```
# can include more than two conditions
df.loc[(df.col1 == 1) & (df.col2 == 2)]
df.loc[(df.col1 == 1) | (df.col2 == 2)] 
```

### reset index
```
df.reset_index(drop=True, inplace=True)
```

### sort
```
# 0 for col, 1 for row
df.sort_values(by='Date', axis=0, ascending=True,inplace=True)
```

## Algo_Type

[algo_typ](https://www.dezyre.com/article/2018-data-science-interview-questions-for-top-tech-companies-/189)

### Sort a list based on another list
```
#sort B based on values in A
A = [10,20,15]
B = [0,1,2]
[b for a,b in sorted(zip(A, B))]
```




