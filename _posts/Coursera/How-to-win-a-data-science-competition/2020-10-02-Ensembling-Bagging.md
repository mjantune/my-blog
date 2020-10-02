---
title:  "Coursera - Ensembling - Bagging - Boosting"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

Here we review Bagging and Boosting methods 

# Bagging

## What is Bagging?

Means **averaging** slightly different version of the same model to improve accuracy.

## Parameters

- Changing the seed
- Row (Sub) sampling or Bootstrapping (Creating an artificial dataset, for example by copying the training data 4 times and taking a sample).
- Shuffling (Some algorithms are sensitive to the order of the data)
- Column (Sub)sampling
- Model-specific parameters (For example regularization parameter in a linear model)
- Number of models (or bags) Usually more than 10
- (Optionally) Paralelism

**BaggingClassifier** and **BaggingRegressor** from SKlearn

## Example

```python
# train is the training data
# test is the test data
# y is the target variable
model = RandomForestRegressor()
bags=10
seed=1
# Create array object to hold bagged predictions
bagged_prediction = np.zeros(test.shape[0])
# Loop for as many times as we want bags
for n in range(0, bags):
    model.set_params(random_state =  seed+n) # update seed
    model.fit(train, y) # fit model
    preds = model.predict(test) # predict on test data
    bagged_prediction += preds # add predictions to bagged predictions

# take average of predictions
bagged_prediction /= bags
```

# Boosting

What is Boosting?
A form of weighted averaging of models where each model is built sequentially via taking into account the past model perfomance.
Every model qe add sequentially into the ensemble, takes into accodunt how well the past models have done.

## Main boosting types

### Weight Based boosting

Example:
![Weight Based Boosting]({{ site.baseurl }}/assets/images/WeightBasedBoosting.png)

Next you fit a new model using the same features and the same target variables, but you also add these weights. This is like saying to the model that you want to give more significance to certain rows. This can be interpreted as the number of times a certain row appears in the data.

Weight based boosting parameters

- Learning rate (or shrinkage or eta)
- Number of estimators (The larger the number of estimators, the smaller the learning rate)
- Input model - Can be anything that accepts weights
- Sub boosting type:
  - AdaBoost - Good implementation in sklearn (python)
  - LogitBoost - Good implementation in weka (java)

### Residual based boosting

This type of boosting has been extremely succesful

![Residual Based Boosting 1]({{ site.baseurl }}/assets/images/ResidualBasedBoosting1.png)

![Residual Based Boosting 2]({{ site.baseurl }}/assets/images/ResidualBasedBoosting2.png)

Residual based boosting parameters

- Learning rate (or shrinkage or eta)
prediction $$ prediction_N = pred_0 + pred_1*\eta + ... + pred_N*\eta $$

- Number of estimators (The larger the number of estimators, the smaller the learning rate)
- Row (sub) sampling
- Columns (sub) sampling
- Input model - Trees work very well
- Sub boosting type:
  - Fully gradient based
  - Dart (Imposes drop-out mechanisms to control the contribution of the trees)

Residual based favourite implementations:

- Xgboost
- Lightgbm (very fast)
- H2O's GBM (Can handle categorical variables out of the box)
- Catboost (Can handle categorica variables out of the box)
- Sklearn's GBM
