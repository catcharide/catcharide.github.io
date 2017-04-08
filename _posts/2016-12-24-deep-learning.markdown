---
layout: post
title: "Deep Learning"
date: 2016-12-24
categories: stuff
---

Logistic Classifier , Use Softmax function. Convert scores -> probabilities.

<img src="http://bit.ly/2ibtppj" align="center" border="0" alt="S( y_{i}) = \frac{e^{y_{i}}}{ \sum_j e^{y_{j}} }  " width="112" height="51" />

```python
"""Softmax."""

scores = [3.0, 1.0, 0.2]

import numpy as np

def softmax(x):
    return np.exp(x)/np.sum(np.exp(x),axis=0)

print(softmax(scores))

# Plot softmax curves
import matplotlib.pyplot as plt
x = np.arange(-2.0, 6.0, 0.1)
scores = np.vstack([x, np.ones_like(x), 0.2 * np.ones_like(x)])

plt.plot(x, softmax(scores).T, linewidth=2)
plt.show()
```

One Hot Encoding

Convert probabilities to Classifier

Inefficient Hot encoding if many classes

Cross Entropy

Distance b/w two matrix

Multinomial Logistic Classfication

Average Cross Entropy

Gradient Descent

Normalized Inputs -> Zero Mean , Equal Variance

Weight Initialization  -> Pick weights from gaussian distribution with sigma

Train , Test , Validation


Stochastic Gradient Descent (SGD) scalable brother of Gradient Descent . Rather than running computation on all the dataset , run it on random sample of data.

Momentum -> Rather than computing derivative over each step , use the momentum as M <- 0.9M ∆∂ .

Learning Rate Decay -> Make step size smaller (eg. exponential decay).


SGD (Black Magic)

Many Hyperparameters

Initial Learning Rate
Learning Rate Decay
Momentum ( instead of derivative )
Batch Size
Weight Initialization

ADAGRAD -> SGD which has some of the Hyperparameters(Initial Learning Rate,Learning Rate Decay,Momentum) already tuned.
