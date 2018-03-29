# Good Blogs and Papers on ML

## AutoML
[Link](https://research.googleblog.com/2018/03/using-evolutionary-automl-to-discover.html)
### Summary

## NN Optimization and Learning Rate Decay
[Link](https://research.googleblog.com/2018/03/using-machine-learning-to-discover.html)
### Summary
- It is possible to automate the discovery of new optimizers, in a way that is similar to how AutoML has been used to discover new competitive neural network architectures.
- PowerSign and AddSign Optimizers are discovered.
- In the PowerSign optimizer each update compares the sign of the gradient and its running average, adjusting the step size according to whether those two values agree.
- Also discovered a simple learning rate decay scheme, [**linear cosine decay**](https://www.tensorflow.org/api_docs/python/tf/train/linear_cosine_decay), which we found can lead to faster convergence.
