# ActiveHrs/Ear_nin

## SQL
### Given two tables and asked to do a Group By type Question
Takeaways:
Ans is something like this:
```
SELECT ((CAST (SUM(table.colA)) AS Float)/ (CAST (SUM(table.colB)) AS Float))
FROM table1 LEFT JOIN table2 ON ....
WHERE .....
GROUP BY table.colC
```
- If you are dividing two Ints in SQL then the answer will also be an Int. So we should cast int as a float
- SUM(exp1)/SUM(exp2) is allowed in SQL when doing the groupby

### A table like below is given:
```
tablename: UserExperiment
ID    expID   groupID
101   1       1
101   2       2
102   1       2
103   2       1
```
### We want IDs that have following condition (expID=1, groupID=1) AND (expID=2, groupID=2) All 4 of these must be met. For above table these conditions are met for ID 101.
We can do this by **joining the UserExperiment to itself** and getting a table like this:
```
ID    exp1   group1    exp2   group2
101   1       1         1       1
101   1       1         2       2
101   2       2         2       2
101   2       2         1       1
102   1       2         1       2
103   2       1         2       1
```
Now we can use a case statement to group IDs (what was asked in the Int) 
```
CASE
WHEN exp1 =1 AND group1 =1 AND exp2=2 AND group2 =2 THEN 'Group1'
ELSE 'Group2'
END
```

## Python
### Given an array of items and an array of weights associated with that array (both will have same length). Write a fn that returns the elements of first array with probabilities associated with wts array in long run.
```
A = [X, Y, Z]
wts = [1/3, 1/17, 1/7]
# In long run, probability of X being drawn from the A should be = wts[0] / (wts[0]+wts[1]+wts[2])
```
Answer is simple use weighted random choice
```
from numpy.random import choice
#in our case list_of_candidates=A, number_of_items_to_pick=1, p=wts/(wts[0]+wts[1]+wts[2])
draw = choice(A, 1, p=wts/(wts[0]+wts[1]+wts[2]))
```



#Given an N element array, find all triples a, b, and c, that satisfy the following famous geometric equality: a^2 + b^2 = c^2
```
# assume all elements are unique, positive integers

myArray = [2, 11, 13, 15, 12, 17, 3, 5, 7, 9, 4]

import math
def triples(a): # a is the array
    triples = []
    squared = [a[i]*a[i] for i in range(len(a))]
    for i in range(len(a)):
        for j in range(len(a)):
            if a[i] != a[j]:
                c = squared[i]+squared[j]
                if c  in squared:
                    ans = [a[i], a[j], math.sqrt(c)]
                    triples.append(ans)
                    
    return triples
```
   
Whats happening to the ML algorithm below:
```        
#Sample Size      1000    5000    10000    20000    30000
#Training Err     0.5     1       2        2        2
#Test Error       10.0    8       6        6        6

# test set - 100000000000
```
- Learning rate is not decaying properly so as no of training samples inc. the accu. has fallen because SGD may have gone to another local minima. (But why is test error decreasing?)
