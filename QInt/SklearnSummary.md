# Summary of Simple ML Algorithms

[Source](http://scikit-learn.org/stable/user_guide.html)

## Supervised Learning

### Generalized Linear Models (Linear Regression, Logistical Regression)
#### Linear Regression
In Lin Reg, we min. the residual sum of squares
![LinReg](http://scikit-learn.org/stable/_images/math/e8e92a5482d9327d939e7a17946a8a1b98006018.png)

```
>>> from sklearn import linear_model
>>> reg = linear_model.LinearRegression()
>>> reg.fit ([[0, 0], [1, 1], [2, 2]], [0, 1, 2])
LinearRegression(copy_X=True, fit_intercept=True, n_jobs=1, normalize=False)
>>> reg.coef_
```

Four assumption of Lin Reg: (Error terms has)
- Linear Relation
- Independent
- Constant Variance
- Normal Distribution

#### Ridge Regression
**Complexity:** Ridge Regression has same complexity as Ordinary Least Squares.

Can add Regularization to the Lin Reg obj fn. Ridge/L-2 Regularizaton is more robust to collinearity.

![Ridge Reg](http://scikit-learn.org/stable/_images/math/48dbdad39c89539c714a825c0c0d5524eb526851.png)

```
>>> reg = linear_model.RidgeCV(alphas=[0.1, 1.0, 10.0])
>>> reg.fit([[0, 0], [0, 0], [1, 1]], [0, .1, 1])
```

#### Lasso Regression
L-1 Regularization. The Lasso is a linear model that estimates sparse coefficients. It is useful in some contexts due to its tendency to prefer solutions with fewer parameter values, effectively reducing the number of variables upon which the given solution is dependent. For this reason, the Lasso and its variants are fundamental to the field of compressed sensing.

![Lasso](http://scikit-learn.org/stable/_images/math/07c30d8004d4406105b2547be4f3050048531656.png)

```
>>> reg = linear_model.Lasso(alpha = 0.1)
>>> reg.fit([[0, 0], [1, 1]], [0, 1])
```

#### ToDo

### Naive Bayes

