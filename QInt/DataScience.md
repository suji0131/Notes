# Data Science Interview Questions

[Source](https://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html)

[Source](https://elitedatascience.com/machine-learning-interview-questions-answers)

[ToDo - SpringBoard](https://www.springboard.com/blog/data-science-interview-questions/)

[ToDo - Glassdoor](https://www.glassdoor.com/Interview/data-scientist-interview-questions-SRCH_KO0,14.htm)

## The Big Picture
### What are parametric models? Give an example.
Parametric models are those with a finite number of parameters. To predict new data, you only need to know the parameters of the model. Examples include linear regression, logistic regression, and linear SVMs.

Non-parametric models are those with an unbounded number of parameters, allowing for more flexibility. To predict new data, you need to know the parameters of the model and the state of the data that has been observed. Examples include decision trees, k-nearest neighbors, and topic models using latent dirichlet analysis.

### What is the "Curse of Dimensionality?
The difficulty of searching through a solution space becomes much harder as you have more features (dimensions).

Consider the analogy of looking for a penny in a line vs. a field vs. a building. The more dimensions you have, the higher volume of data you'll need.

### Explain the Bias-Variance Tradeoff.
```
Bias: How far from truth is your model's expected value.
Variance: How the performance of model changes with new data.
```
Predictive models have a tradeoff between bias (how well the model fits the data or how far the expected value is from original mean) and variance (how much the model changes based on changes in the inputs).

Simpler models are stable (low variance) but they don't get close to the truth (high bias).

More complex models are more prone to being overfit (high variance) but they are expressive enough to get close to the truth (low bias).

The best model for a given problem usually lies somewhere in the middle.

## Optimization
### What is the difference between stochastic gradient descent (SGD) and gradient descent (GD)?
Both algorithms are methods for finding a set of parameters that minimize a loss function by evaluating parameters against data and then making adjustments.

In standard gradient descent, you'll evaluate all training samples for each set of parameters. This is akin to taking big, slow steps toward the solution.

In stochastic gradient descent, you'll evaluate only 1 training sample for the set of parameters before updating them. This is akin to taking small, quick steps toward the solution.

### When would you use GD over SDG, and vice-versa?
GD theoretically minimizes the error function better than SGD. However, SGD converges much faster once the dataset becomes large.

That means GD is preferable for small datasets while SGD is preferable for larger ones.

In practice, however, SGD is used for most applications because it minimizes the error function well enough while being much faster and more memory efficient for large datasets.

### Explain what regularization is and why it is useful.
[blog about regularization](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)

To prevent overfitting. It discourages learning a more complex or flexible model, so as to avoid the risk of overfitting. We 
multiply the parameters by regularization coefficient, λ (a tuning parameter that decides how much we want to penalize the flexibility of our model)

![Ridge Regression](https://cdn-images-1.medium.com/max/800/1*CiqZ8lhwxi5c4d1nV24w4g.png)

![Lasso](https://cdn-images-1.medium.com/max/800/1*tHJ4sSPYV0bDr8xxEdiwXA.png)

Regularization, significantly reduces the variance of the model, without substantial increase in its bias. So the tuning parameter λ, used in the regularization techniques described above, controls the impact on bias and variance. As the value of λ rises, it reduces the value of coefficients and thus reducing the variance. Till a point, this increase in λ is beneficial as it is only reducing the variance(hence avoiding overfitting), without loosing any important properties in the data. But after certain value, the model starts loosing important properties, giving rise to bias in the model and thus underfitting. Therefore, the value of λ should be carefully selected.

### Explain the difference between L1 (Lasso) and L2 (Ridge) regularization methods? (Elastic net is ratio of L1 & L2 Regu.)
For Lasso or L1-Regularization, you use L1 norm of coeficients for regularization. (L1 norm of a vector is sum of absolute values of its components) 

![Lasso](https://cdn-images-1.medium.com/max/800/1*tHJ4sSPYV0bDr8xxEdiwXA.png)

For Ridge or L2-Regularization, you use L2 norm of coeficients for regularization. (L2 norm of a vector is sum of squares of its components) 

![Ridge Regression](https://cdn-images-1.medium.com/max/800/1*CiqZ8lhwxi5c4d1nV24w4g.png)

### Which regularization is better L1 or L2?
As a rule-of-thumb, you should always go for L2 in practice.

Is there collinearity among some features? L2 regularization can improve prediction quality in this case. However, it is true in general that either form of regularization will improve out-of-sample prediction, whether or not there is multicollinearity and whether or not there are irrelevant features, simply because of the shrinkage properties of the regularized estimators. 

L1 regularization can't help with multicollinearity; it will just pick the feature with the largest correlation to the outcome

Even in the case when you have a strong reason to use L1 given the number of features, I would recommend going for Elastic Nets (ratio of L1 & L2 Regu.) instead. Granted this will only be a practical option if you are doing linear/logistic regression. But, in that case, Elastic Nets have proved to be (in theory and in practice) better than L1/Lasso.

### momentum

## Data Preprocessing
### What is the Box-Cox transformation used for?
[Blog](https://www.quora.com/In-laymans-language-Box-Cox-transformation-is-used-for-what)
The Box-Cox transformation is a generalized "power transformation" that transforms data to make the distribution more normal.

For example, when its lambda parameter is 0, it's equivalent to the log-transformation.

It's used to stabilize the variance (eliminate heteroskedasticity) and normalize the distribution.

### What are 3 data preprocessing techniques to handle outliers?
- cap at threshold (Winsorize).
- Transform to reduce skew (using Box-Cox or similar).
- Remove outliers if you're certain they are anomalies or measurement errors.

### What are 3 ways of reducing dimensionality?
- Removing collinear features.
- Performing PCA, ICA, or other forms of algorithmic dimensionality reduction.
- Combining features with feature engineering.

## Sampling & Splitting
### K-fold Cross Validation
By partitioning the available data into three sets, we drastically reduce the number of samples which can be used for learning the model, and the results can depend on a particular random choice for the pair of (train, validation) sets.

A solution to this problem is a procedure called cross-validation (CV for short). A test set should still be held out for final evaluation, but the validation set is no longer needed when doing CV. In the basic approach, called k-fold CV, the training set is split into k smaller sets (other approaches are described below, but generally follow the same principles). The following procedure is followed for each of the k “folds”:

- A model is trained using k-1 of the folds as training data;
- the resulting model is validated on the remaining part of the data (i.e., it is used as a test set to compute a performance measure   such as accuracy).

The performance measure reported by k-fold cross-validation is then the average of the values computed in the loop. This approach can be computationally expensive, but does not waste too much data (as it is the case when fixing an arbitrary test set), which is a major advantage in problem such as inverse inference where the number of samples is very small.

### If you split your data into train/test splits, is it still possible to overfit your model?
Yes, it's definitely possible. One common beginner mistake is re-tuning a model or training new models with different parameters after seeing its performance on the test set.

In this case, its the model selection process that causes the overfitting. The test set should not be tainted until you're ready to make your final selection.

### What is selection bias, why is it important and how can you avoid it?
Selection bias, in general, is a problematic situation in which error is introduced due to a non-random population sample. For example, if a given sample of 100 test cases was made up of a 60/20/15/5 split of 4 classes which actually occurred in relatively equal numbers in the population, then a given model may make the false assumption that probability could be the determining predictive factor. Avoiding non-random samples is the best way to deal with bias; however, when this is impractical, techniques such as resampling, boosting, and weighting are strategies which can be introduced to help deal with the situation. 

## Supervised Learning
### What are the advantages and disadvantages of decision trees?
Advantages: Decision trees are easy to interpret, nonparametric (which means they are robust to outliers), and there are relatively few parameters to tune.

Disadvantages: Decision trees are prone to be overfit. However, this can be addressed by ensemble methods like random forests or boosted trees.

### What are the advantages and disadvantages of neural networks?
Advantages: Neural networks (specifically deep NNs) have led to performance breakthroughs for unstructured datasets such as images, audio, and video. Their incredible flexibility allows them to learn patterns that no other ML algorithm can learn.

Disadvantages: However, they require a large amount of training data to converge. It's also difficult to pick the right architecture, and the internal "hidden" layers are incomprehensible.

### How can you choose a classifier based on training set size?
If training set is small, high bias / low variance models (e.g. Naive Bayes) tend to perform better because they are less likely to be overfit.

If training set is large, low bias / high variance models (e.g. Logistic Regression) tend to perform better because they can reflect more complex relationships.

### How is kNN different from k-means clustering?
kNN, or k-nearest neighbors is a classification algorithm, where the k is an integer describing the the number of neighboring data points that influence the classification of a given observation. K-means is a clustering algorithm, where the k is an integer describing the number of clusters to be created from the given data. Both accomplish different tasks.

### What are some situations where a general linear model fails?
- When there is a non-linear relationship. 
- Four Assumptions are violated. (Nor, Lin, Indepen, Variance)

### Batch Normalization

## Unsupervised Learning
###  Explain Latent Dirichlet Allocation (LDA).
Latent Dirichlet Allocation (LDA) is a common method of topic modeling, or classifying documents by subject matter.

LDA is a generative model that represents documents as a mixture of topics that each have their own probability distribution of possible words.

The "Dirichlet" distribution is simply a distribution of distributions. In LDA, documents are distributions of topics that are distributions of words.

### Explain Principle Component Analysis (PCA).
PCA is a method for transforming features in a dataset by combining them into uncorrelated linear combinations.

These new features, or principal components, sequentially maximize the variance represented (i.e. the first principal component has the most variance, the second principal component has the second most, and so on).

As a result, PCA is useful for dimensionality reduction because you can set an arbitrary variance cutoff.

## Model Evaluation
### Explain what precision and recall are. How do they relate to the ROC curve?
Precision-Recall is a useful measure of success of prediction when the classes are very imbalanced. 

Recall (sensitivity): True positive divided by how many real ones are there. (how many of the positive samples have been identified as being positive)

A system with high recall but low precision returns many results, but most of its predicted labels are incorrect when compared to the training labels.

Precision: True positive divided by how many ones did you predict
A system with high precision but low recall is just the opposite, returning very few results, but most of its predicted labels are correct when compared to the training labels.

Sensitivity is the other name for recall but specificity is **NOT PRECISION**. Specificity is a measure of how many of the negative samples have been identified as being negative. 

Precision is used when positive class is more interesting than the negative class. So, if your problem involves kind of searching a needle in the haystack when for ex: the positive class samples are very rare compared to the negative classes, use a precision recall curve. Othwerwise use a ROC curve because a ROC curve remains the same regardless of the baseline prior probability of your positive class (the important rare class).

### Is it better to have too many false positives, or too many false negatives? Explain.
It depends on the question as well as on the domain for which we are trying to solve the question. 

In medical testing, false negatives may provide a falsely reassuring message to patients and physicians that disease is absent, when it is actually present. This sometimes leads to inappropriate or inadequate treatment of both the patient and their disease. So, it is desired to have too many false positive. 

For spam filtering, a false positive occurs when spam filtering or spam blocking techniques wrongly classify a legitimate email message as spam and, as a result, interferes with its delivery. While most anti-spam tactics can block or filter a high percentage of unwanted emails, doing so without creating significant false-positive results is a much more demanding task. So, we prefer too many false negatives over many false positives.

### What is the difference bt Type-1 and Type-2 Errors?
- Type-1 is FP
- Type-2 is FN

### How can you prove that one improvement you've brought to an algorithm is really an improvement over not doing anything?
One common way to achieve the above guidelines is through A/B testing, where both the versions of algorithm are kept running on similar environment for a considerably long time and real-life input data is randomly split between the two. This approach is particularly common in Web Analytics. 

(more on AB Testing later)

### How to observe over-fitting?
![Overfitting](https://codelabs.developers.google.com/codelabs/cloud-tensorflow-mnist/img/d1a460e8334d6b1c.png)

As seen in above fig to the left end of graph we can see that the loss on train data is very low and on validation it is increasing which is a sign of overfitting. Dropout and Regularization are some of the methods that help to reduce the overfitting.

### What is statistical power?
Power of a hypothesis test is the probability that the test correctly rejects null hypothesis (H0) when alternative hypothesis (H1) is true. To put in another way, Statistical power is the likelihood that a study will detect an effect when the effect is present. The higher the statistical power, the less likely you are to make a Type II error (concluding there is no effect when, in fact, there is). (Different fromn AB testing?).

### How would you test if survey responses were filled at random by certain individuals, as opposed to truthful selections?
- I would design the test in a way that certain information is asked two different ways. if two answers disagree with each other I would seriously doubt the validity of the answers.
- Calculate Cronbach's alpha for the survey items. If it is low (below .5), it is very likely that the questions were answered at random.

### How would you validate a model you created to generate a predictive model of a quantitative outcome variable using multiple regression.
- Using R<sup>2</sup> is one way.
- If the values seem to be reasonable, examine the parameters; any of the following would indicate poor estimation or multi-collinearity: opposite signs of expectations, unusually large or small values, or observed inconsistency when the model is fed new data.
- Use jackknife resampling if the dataset contains a small number of instances, and measure validity with R squared and mean squared error (MSE). The jackknife estimator of a parameter is found by systematically leaving out each observation from a dataset and calculating the estimate and then finding the average of these calculations. Given a sample of size n, the jackknife estimate is found by aggregating the estimates of each n-1 sized sub-sample.

### What is root cause analysis?
Essentially, you can find the root cause of a problem and show the relationship of causes by repeatedly asking the question, "Why?", until you find the root of the problem.

### confounding factors

### In your opinion, which is more important when designing a machine learning model: Model performance? Or model accuracy?

### I have two models of comparable accuracy and computational performance. Which one should I choose for production and why?
- Depends on Data (balanced or unbalanced?)
- Your requirement. Sometimes high Flase Pos is req another time False Neg are prefered (Health care and Spam filtering respec.)

## Ensemble Learning
### Why are ensemble methods (Combining multiple models for better performance) superior to individual models?
They average out biases, reduce variance, and are less likely to overfit.

This implies that you can build your models as usual and typically expect a small performance boost from ensembling.

### Do you think 50 small decision trees are better than a large one? Why?
They average out biases, reduce variance, and are less likely to overfit. If we built/used those 50 trees properly

### Explain bagging.
Bagging, or Bootstrap Aggregating, is an ensemble method in which the dataset is first divided into multiple subsets through resampling.

Then, each subset is used to train a model, and the final predictions are made through voting or averaging the component models.

Bagging is performed in parallel.

## Business Applications

### price elasticity
Price Elasticity: This curve measures how demand varies with changes in price.

### How can you help our marketing team be more efficient?
The answer will depend on the type of company. Here are some examples.

- Clustering algorithms to build custom customer segments for each type of marketing campaign.
- Natural language processing for headlines to predict performance before running ad spend.
- Predict conversion probability based on a user's website behavior in order to create better re-targeting campaigns.

### How do you detect individual paid accounts shared by multiple users?
- If within some timeframe multiple logins from regions geographically far apart log in, then you know those credentials have been shared.
- Bandwitdh consumption: if your site offers lots of content, if a user goes over some high limit, it means its credentials have been shared.
- Keep a counter of live sessions so you can see how many people log in at the same time. This is imprecise because the same person can log in through multiple browsers from the same IP and have a session on each one.

### How do you take millions of users with 100's of transactions each, amongst 10k's of products and group the users together in a meaningful segments? (Apple)
- Type of Products can be segments (Macs, Iphones, Ipads etc.) Based on each segment we can do further analysis.
- Calc vector distances

## Visualization

### How would you effectively represent data with 5 dimensions? 
With visual attributes such as color, size and shape one can easily add some more dimensions to a visualization. So using a 2D scatter plot with diff colors for one dim, size of other dim, and shapes for another dim we can represent 5D data. Correct plot  depends on the correct combination of displayed columns, so try diff combinations.

## Probability and Statistics
### You're about to get on a plane to Seattle. You want to know if you should bring an umbrella. You call 3 random friends of yours who live there and ask each independently if it's raining. Each of your friends has a 2/3 chance of telling you the truth and a 1/3 chance of messing with you by lying. All 3 friends tell you that "Yes" it is raining. What is the probability that it's actually raining in Seattle?
Bayesian stats: you should estimate the prior probability that it's raining on any given day in Seattle. If you mention this or ask the interviewer will tell you to use 25%. Then it's straight-forward: P(raining | Yes,Yes,Yes) = Prior(raining) * P(Yes,Yes,Yes | raining) / P(Yes, Yes, Yes) P(Yes,Yes,Yes) = P(raining) * P(Yes,Yes,Yes | raining) + P(not-raining) * P(Yes,Yes,Yes | not-raining) = 0.25*(2/3)^3 + 0.75*(1/3)^3 = 0.25*(8/27) + 0.75*(1/27) P(raining | Yes,Yes,Yes) = 0.25*(8/27) / ( 0.25*8/27 + 0.75*1/27 ) Bonus points if you notice that you don't need a calculator since all the 27's cancel out and you can multiply top and bottom by 4. P(training | Yes,Yes,Yes) = 8 / ( 8 + 3 ) = 8/11





















