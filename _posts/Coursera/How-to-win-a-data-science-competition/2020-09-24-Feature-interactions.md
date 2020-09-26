---
title:  "Coursera - Advanced Features II - Feature Interactions"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

Suppose that we are building a model to predict the best advertisement banner to display on a website. Among available features, there are two categorical ones that we will concentrate on. The category of the advertising banner itself and the category of the site the banner will be showing on.
Certainly, we can use the features as two independent ones, but a really important feature is indeed the combination of them. We can explicitly construct the combination in order to incorporate our knowledge into a model.

# Some data for CTR Task
![Banner Selection]({{ site.baseurl }}/assets/Feature_interactions_1.png)

# Frequent operations for feature interaction
- Multiplication
- Sum
- Diff
- Division 

# Practical Notes
- We have a lot of possible interactions - N*N for N features
    - Even more if we use several types of interactions
- Need to reduce it's number
    a. Dimensionality reduction
    b. Feature selection 

# Example of interaction generation pipeline

![Banner Selection]({{ site.baseurl }}/assets/Feature_interactions_2.png)
