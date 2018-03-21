# Data Science Interview Questions

[Source](https://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html)
### Explain what regularization is and why it is useful.
To prevent overfitting. It discourages learning a more complex or flexible model, so as to avoid the risk of overfitting. We 
multiply the parameters by regularization coefficient, lambda (a tuning parameter that decides how much we want to penalize the flexibility of our model)

![Ridge Regression](https://cdn-images-1.medium.com/max/800/1*CiqZ8lhwxi5c4d1nV24w4g.png)

![Lasso](https://cdn-images-1.medium.com/max/800/1*tHJ4sSPYV0bDr8xxEdiwXA.png)

Regularization, significantly reduces the variance of the model, without substantial increase in its bias. So the tuning parameter λ, used in the regularization techniques described above, controls the impact on bias and variance. As the value of λ rises, it reduces the value of coefficients and thus reducing the variance. Till a point, this increase in λ is beneficial as it is only reducing the variance(hence avoiding overfitting), without loosing any important properties in the data. But after certain value, the model starts loosing important properties, giving rise to bias in the model and thus underfitting. Therefore, the value of λ should be carefully selected.
