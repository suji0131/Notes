# Data Science Interview Questions

[Source](https://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html)
### Explain what regularization is and why it is useful.
[blog about regularization](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)

To prevent overfitting. It discourages learning a more complex or flexible model, so as to avoid the risk of overfitting. We 
multiply the parameters by regularization coefficient, λ (a tuning parameter that decides how much we want to penalize the flexibility of our model)

![Ridge Regression](https://cdn-images-1.medium.com/max/800/1*CiqZ8lhwxi5c4d1nV24w4g.png)

![Lasso](https://cdn-images-1.medium.com/max/800/1*tHJ4sSPYV0bDr8xxEdiwXA.png)

Regularization, significantly reduces the variance of the model, without substantial increase in its bias. So the tuning parameter λ, used in the regularization techniques described above, controls the impact on bias and variance. As the value of λ rises, it reduces the value of coefficients and thus reducing the variance. Till a point, this increase in λ is beneficial as it is only reducing the variance(hence avoiding overfitting), without loosing any important properties in the data. But after certain value, the model starts loosing important properties, giving rise to bias in the model and thus underfitting. Therefore, the value of λ should be carefully selected.

### How would you validate a model you created to generate a predictive model of a quantitative outcome variable using multiple regression.
- Using R<sup>2</sup> is one way.
- If the values seem to be reasonable, examine the parameters; any of the following would indicate poor estimation or multi-collinearity: opposite signs of expectations, unusually large or small values, or observed inconsistency when the model is fed new data.
- Use jackknife resampling if the dataset contains a small number of instances, and measure validity with R squared and mean squared error (MSE). The jackknife estimator of a parameter is found by systematically leaving out each observation from a dataset and calculating the estimate and then finding the average of these calculations. Given a sample of size n, the jackknife estimate is found by aggregating the estimates of each n-1 sized sub-sample.

### Explain what precision and recall are. How do they relate to the ROC curve?
Precision-Recall is a useful measure of success of prediction when the classes are very imbalanced. 

Recall (sensitivity): True positive divided by how real ones are there. (how many of the positive samples have been identified as being positive)

A system with high recall but low precision returns many results, but most of its predicted labels are incorrect when compared to the training labels.

Precision: True positive divided by how many ones did you predict
A system with high precision but low recall is just the opposite, returning very few results, but most of its predicted labels are correct when compared to the training labels.

Sensitivity is the other name for recall but specificity is **NOT PRECISION**. Specificity is a measure of how many of the negative samples have been identified as being negative. 

Precision is used when positive class is more interesting than the negative class. So, if your problem involves kind of searching a needle in the haystack when for ex: the positive class samples are very rare compared to the negative classes, use a precision recall curve. Othwerwise use a ROC curve because a ROC curve remains the same regardless of the baseline prior probability of your positive class (the important rare class).

### How can you prove that one improvement you've brought to an algorithm is really an improvement over not doing anything?
One common way to achieve the above guidelines is through A/B testing, where both the versions of algorithm are kept running on similar environment for a considerably long time and real-life input data is randomly split between the two. This approach is particularly common in Web Analytics. 

(more on AB Testing later)

### What is root cause analysis?
Essentially, you can find the root cause of a problem and show the relationship of causes by repeatedly asking the question, "Why?", until you find the root of the problem.



### price elasticity
Price Elasticity: This curve measures how demand varies with changes in price.

### What is statistical power?
Power binary hypothesis test is the probability that the test correctly rejects the null hypothesis (H0) when the alternative hypothesis (H1) is true. To put in another way, Statistical power is the likelihood that a study will detect an effect when the effect is present. The higher the statistical power, the less likely you are to make a Type II error (concluding there is no effect when, in fact, there is). (Different fromn AB testing?).

### Is it better to have too many false positives, or too many false negatives? Explain.
It depends on the question as well as on the domain for which we are trying to solve the question. 

In medical testing, false negatives may provide a falsely reassuring message to patients and physicians that disease is absent, when it is actually present. This sometimes leads to inappropriate or inadequate treatment of both the patient and their disease. So, it is desired to have too many false positive. 

For spam filtering, a false positive occurs when spam filtering or spam blocking techniques wrongly classify a legitimate email message as spam and, as a result, interferes with its delivery. While most anti-spam tactics can block or filter a high percentage of unwanted emails, doing so without creating significant false-positive results is a much more demanding task. So, we prefer too many false negatives over many false positives. 

### What is selection bias, why is it important and how can you avoid it?
Selection bias, in general, is a problematic situation in which error is introduced due to a non-random population sample. For example, if a given sample of 100 test cases was made up of a 60/20/15/5 split of 4 classes which actually occurred in relatively equal numbers in the population, then a given model may make the false assumption that probability could be the determining predictive factor. Avoiding non-random samples is the best way to deal with bias; however, when this is impractical, techniques such as resampling, boosting, and weighting are strategies which can be introduced to help deal with the situation. 

### K-fold Cross Validation
By partitioning the available data into three sets, we drastically reduce the number of samples which can be used for learning the model, and the results can depend on a particular random choice for the pair of (train, validation) sets.

A solution to this problem is a procedure called cross-validation (CV for short). A test set should still be held out for final evaluation, but the validation set is no longer needed when doing CV. In the basic approach, called k-fold CV, the training set is split into k smaller sets (other approaches are described below, but generally follow the same principles). The following procedure is followed for each of the k “folds”:

- A model is trained using k-1 of the folds as training data;
- the resulting model is validated on the remaining part of the data (i.e., it is used as a test set to compute a performance measure   such as accuracy).

The performance measure reported by k-fold cross-validation is then the average of the values computed in the loop. This approach can be computationally expensive, but does not waste too much data (as it is the case when fixing an arbitrary test set), which is a major advantage in problem such as inverse inference where the number of samples is very small.






















