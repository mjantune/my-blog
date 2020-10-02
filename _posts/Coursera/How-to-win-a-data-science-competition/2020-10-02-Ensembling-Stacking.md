---
title:  "Coursera - Ensembling - Stacking and Stacknet"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

Here we review Stacking methods

What is Stacking?
Mean making predictions of a number of models in a hold-out set and then using a different (Meta) mode to train on these predictions.

# Stacking

Methodology:

1. **Splitting** the train set into two disjoint sets
2. **Train** several base learners on the first part.
3. **Make predictions** with the base learners on the second (validation) part.
4. using the **predictions** from (3) as the input train a higher level learner.

Stacking Example

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.linear_model import LinearRegression
import numpy as np
from sklearn.model_selection import train_test_split

# train is the training data
# test is the test data
# y is the target variable for the train data

training, valid, ytraining, yvalid = train_test_split(train, y, test, test_size = 0.5)

# Specify models
model1 = RandomForestRegressor()
model2 = LinearRegression()

# Fit Models
model1.fit(training, ytraining)
model2.fit(training, ytraining)

# Make predictions for validation
preds1 = model1.predict(valid)
preds2 = model2.predict(valid)

# Make predictions for test data
test_preds1 = model1.predict(test)
test_preds2 = model2.predict(test)

# Form a new dataset for valid and test via stacking the predictions
stacked_predictions = np.column_stack((preds1,preds2))
stacked_test_predictions = np.column_stack((test_preds1,test_preds2))

# Specify meta model
meta_model = LinearRegression()

# Fit meta model on stacked predictions
meta_model.fit(stacked_predictions, yvalid)

#Make predictions on the stacked predictions of the test data
final_predictions = meta_model.predict(stacked_test_predictions)
```

## Things to be mindful of

- With time sensitive data - respect time
- Diversity as important as performance (how different a model is from each other)
- Diversity may come from:
  - Different algorithms
  - Different input features, for example in one model use label encoding, and in other one hot encoding.
- Performance plateauing after N models.
- Meta model is normally modest

# StackNet

A scalable meta modelling methodology that utilizes stacking to combine multiple models in a neural network architecture of multiple levels.

StackNet is a scalable meta modeling methodology that utilizes stacking to combine multiple models in a neural network architecture of multiple levels. It is scalable because within the same level, we can run all the models in parallel.
