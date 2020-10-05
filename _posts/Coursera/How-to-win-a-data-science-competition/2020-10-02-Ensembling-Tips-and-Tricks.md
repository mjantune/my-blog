---
title:  "Coursera - Ensembling Tips and Tricks"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

## 1st level tips

- Diversity based on algorithms:
  - 2-3 gradient boosted trees (lightgb, xgboost, H2O, catboost)
  - 2-3 Neural nets (keras, pytorch)
  - 1-2 ExtraTrees/Random Forest (sklearn)
  - 1-2 linear models as in logitic/ridge regression, linear svm (sklearn)
  - 2 knn models (sklearn)
  - 1 Factorization machine (libfm)
  - 1 svm with nonlinear kernel if size/memory allows (sklearn)

- Diversity based on input:
  - Categorical features: One hot, label encodig, target encoding
  - Numerical features: outliers, binning, derivatives, percentiles, scaling.
  - Interactions: col1*/+-col2, groupby, unsupervised

## Subsequent level tips

- Simpler (or shallower) algorithms:
  - Gradient boosted trees with small depth (like 2 or 3)
  - Linear models wit high regularization
  - Extra trees
  - Shallow networks (as in 1 hidden layer)
  - knn with BrayCurtis Distance
  - Brute forcing a search for best linear weights based on CV

- Feature Engineering:
  - Pairwise differences between meta features
  - Row wise statistics like averages or stds
  - Standard feature selection techniques

- Rule of Thumb **For every 7.5 models in previous levekl we add 1 meta**
- Be mindful of target leakage.

## Software for Stacking

- Stacknet (https://github/kaz-Anova/StackNet)
  - It supports many prominent tools (xgboost, lightgbm, H2O, keras...)
  - Can run classifiers in regression and vice versa
  - It has several top 10s in competitions
  - Parameters section
- Stacked ensembles from H2O
- Xcessiv (https://github.com/reenakano/xcessiv)
