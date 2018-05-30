# Python
[basic](https://www.dezyre.com/article/100-data-science-in-python-interview-questions-and-answers-for-2018/188)
[algo_typ](https://www.dezyre.com/article/2018-data-science-interview-questions-for-top-tech-companies-/189)

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

### li = [1,2,3,4] then li[8:] returns?
An empty list []. Most of the people might confuse the answer with an index error because the code is attempting to access a member in the list whose index exceeds the total number of members in the list. The reason being the code is trying to access the slice of a list at a starting index which is greater than the number of members in the list.

### Sort a list based on another list
```
#sort B based on values in A
A = [10,20,15]
B = [0,1,2]
[b for a,b in sorted(zip(A, B))]
```
