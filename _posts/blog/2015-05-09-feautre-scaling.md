---
layout: post
title: "Feature scaling"
modified:
categories: blog
excerpt: 
tags: []
image:
feature:
date: 2015-05-09
---

The [scikit-learn](http://scikit-learn.org/stable/) module makes it surprisingly easy to implement a wide range of machine learning algoirthms in Python. Often times, the only parameters you need to specify are your model and data, and scikit-learn will do the rest.

But before putting your raw data into the model, it's important that it's in the right format. This means ensuring that your predictor variables are numerical and properly scaled. This post will focus on properly scaling your features.

### Scaling methods

**Standard scale**

Features can be scaled to have mean 0 and variance 1, which is also known as calculating Z-scores for every observation. This will usually transform the data so that most of your data falls between [-3, 3].

**Min-max scale**

Another way of scaling is to subtract each value by the minimum value and divide by the range. This is called [min-max scaling](http://stn.spotfire.com/spotfire_client_help/norm/norm_scale_between_0_and_1.htm) and it transforms your feature to a scale of [0, 1]. For better or worse, this scaling technique does not change the distribution of your data.

### scikit-learn implementations

Scikit has easy implementations of scaling using its preprocessing module.

{% highlight python %}
sklearn.preprocessing.scale(X)
{% endhighlight %}

X can be an array or matrix, by default normalizes to mean 0 and variance 1.

If you want to consider scaling as part of your modeling step rather than your preprocessing step, you can fit your scalar to your training set and apply these same parameters to scaling your test set.

{% highlight python %}
std_scalar = sklearn.preprocessing.StandardScalar()
std_scalar.fit(X_train)
X_train_std = std_scalar.transform(X_train)
X_test_std = std_scalar.transform(X_test)
{% endhighlight %}

{% highlight python %}
std_scalar = sklearn.preprocessing.MinMaxScalar()
std_scalar.fit(X_train)
X_train_std = std_scalar.transform(X_train)
X_test_std = std_scalar.transform(X_test)
{% endhighlight %}

Normalizing to standard normal scale has a big impact on the quality of some models (SVM, kNN), a small impact on others (logistic regression, decision trees), and no impact on Naive Bayes (since the model does feature scaling by design):

![scaled_roc](/images/scaled_roc.png)

[Check out my code](/articles/Feature scaling demo.html)

There are many other ways to transform your variables, scaling being only one class of ways, and it's definitely worth exploring to try to improve the predictive power and fits of your models.
