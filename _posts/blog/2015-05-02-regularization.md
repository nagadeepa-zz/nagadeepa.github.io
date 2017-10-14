---
layout: post
title: "Overfitting & Regularization"
modified:
categories: blog
excerpt: 
tags: []
image:
feature:
date: 2015-05-02
---

**The Problem of overfitting**

A common issue in machine learning or mathematical modeling is overfitting, which occurs when you build a model that not only captures the signal but also the noise in a dataset. 

Because we want to create models that generalize and perform well on different data-points, we need to avoid overfitting.

In comes regularization, which is a powerful mathematical tool for reducing overfitting within our model. It does this by adding a penalty for model complexity or extreme parameter values, and it can be applied to different learning models: linear regression, logistic regression, and support vector machines to name a few. 

Below is the linear regression cost function with an added regularization component.

![Regularization](/images/regularization.png)

The regularization component is really just the sum of squared coefficients of your model (your beta values), multiplied by a parameter, lambda. 

**Lambda**

Lambda can be adjusted to help you find a good fit for your model. However, a value that is too low might not do anything, and one that is too high might actually cause you to underfit the model and lose valuable information. It's up to the user to find the sweet spot.

Cross validation using different values of lambda can help you to identify the optimal lambda that produces the lowest out of sample error.

**Regularization methods (L1 & L2)**

The equation shown above is called Ridge Regression (L2) - the beta coefficients are squared and summed. However, another regularization method is Lasso Regreesion (L1), which sums the absolute value of the beta coefficients. Even more, you can combine Ridge and Lasso linearly to get Elastic Net Regression (both squared and absolute value components are included in the cost function).

L2 regularization tends to yield a "dense" solution, where the magnitude of the coefficients are evenly reduced. For example, for a model with 3 parameters, B1, B2, and B3 will reduce by a similar factor.

However, with L1 regularization, the shrinkage of the parameters may be uneven, driving the value of some coefficients to 0. In other words, it will produce a sparse solution. Because of this property, it is often used for feature selection- it can help identify the most predictive features, while zeroing the others.

It also a good idea to appropriately scale your features, so that your coefficients are penalized based on their predictive power and not their scale.

As you can see, regularization can be a powerful tool for reducing overfitting.

In the words of the great thinkers:

* ["when you have two competing theories that make exactly the same predictions, the simpler one is the better." - William of Ockham](http://math.ucr.edu/home/baez/physics/General/occam.html)

* ["Everything should be made as simple as possible, but not simpler." - Albert Einstein](http://c2.com/cgi/wiki?EinsteinPrinciple)

[An in-depth look into theory and application of regularization](https://www.stat.berkeley.edu/~bickel/Test_BickelLi.pdf).
