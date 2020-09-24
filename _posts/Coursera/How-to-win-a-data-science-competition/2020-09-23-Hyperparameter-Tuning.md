---
layout: post
title:  "Coursera - Hyperparameter Tuning"
categories: coursera data_science
author: "Manuel"
---

# How do we tune parameters

1. Select the most influential parameters
    - There are many parameters and we can't tune all of them
2. Understand, how exactly they influence the training
3. Tune them!
    - Manually (change and examine)
    - Automatically (hyperopt, etc.)

### Libraries to try:
- Hyperopt
- Scikit-optimize
- Spearmint
- GPyOpt
- RoBo
- SMAC3

### Hyperparameter optimization software
{% highlight python %}
def xgb_score(param):
    # run XGBoost with parameters 'param'

def xgb_hyperopt():
    space = {
        'eta' : 0.01,
        'max_depth' : hp.quniform('max_depth', 10, 30, 1),
        etc
    }

    best = fmin(gb_score, space, algo=tpe.suggest, max_evals=1000)
{% endhighlight %}

### Color Coding Legend
- A parameter in *cursive* 
    - Increasing it impedes fitting
    - Increase it to reduce overfitting
    - Decrease to allow model to fit easier

- A parameter in **BOLD**
    - Increasing it leads to a better fit (overfit) on train set
    - Increase it if model underfits
    - Decrease if overfits

# Tree Based Models

| Model                    | Where                            |
|--------------------------|----------------------------------|
| GBDT                     | XGBBoost<br>LightGBM<br>CatBoost |
| RandomForest, ExtraTrees | scikit-learn                     |
| Others                   | RGF (baidu/fast_rgf)             |

## GBDT

| XGBoost                                    | LightGBM                                    | Recommendation                                                                                                           |
|--------------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **max_depth**                              | **max_depth/num_leaves**                    | Start with a max_depth = 7                                                                                               |
| **subsample**                              | **bagging_fraction**                        |                                                                                                                          |
| **colsample_bytree,<br>colsample_bylevel** | **feature_fraction**                        |                                                                                                                          |
| *min_child_weight,<br>lambda, alpha*       | *min_data_in_leaf,<br>lamdba_l1, lambda_l2* | Its one of the most important parameters to tune<br>Depending on the task, the optimum value could be 0, 5, 15, 300, etc |
| **eta<br>num_round**                       | **learning_rate<br>num_iteration**          | Learning rate too high, the model will not fit correctly, but too low, it will take too long to learn.                   |
| Others: seed                               | Others: _seed                               |                                                                                                                          |

# sklearn.RandomForest/ExtraTrees

ExtraTrees is a more randomized version of RandomForest, so they have the same parameters.

- N_estimators:
    Having a lot of trees doesn't lead to overfitting, and is controlled by the `N_estimators` parameter.
    e.g. start with 10 trees and increase depending on the time taken to train, to 100 for example
- **max_depth**: start with a depth of 7, bu could be even higher than 20
- **max_features**
- *min_samples_leaf*: similar to min_data_in_leaf from LightGBM

Others:
- criterion: gini or entropy
- random_state
- n_jobs: set to the number of cores you have

# Neural Networks

What frameworks to use?
- Keras (recommended), Lasagne
- TensorFlow
- MxNet
- PyTorch (recommended)
- sklearn MLP

## Neural Nets

- **Number of neurons per layer**
- **Number of layers**: Start with something simple, 2 layers and 64 units per layer, and check that the validation errors go down and the try to find a configuration that overfits the data. Use this as a sanity check.
- Optimizers
    - *SGD + momentum*
        - Slower but generalize better
    - **Adam/Adadelta/Adagrad/...** (Adaptive methods)
        - They train faster
        - In practice lead to more overfitting
- **Batch Size**: The larger the batch size, the more prone the network is to overfitting
- Learning Rate: Not too high or not too low. I usually start with a huge learning rate (0.1), and then go down trying to find a learning rate with which the model converges.
    
    - Rule of Thumb: If you increase the batch size by a factor of $$ \alpha $$, you can also increase the learning rate by that same factor
- Regularization:
    - *L2/L1 for weights*
    - *Dropout/Dropconnect* This helps the networks find the features that really matter
    - *Static dropconnect* 

## Linear models
- **Scikit-learn**
    - SVC/SVR
        - Sklearn wraps `libLinear` and `libSVM`
        - Compile yourself for multicore support
    - LogisticRegression/LinearRegression + regularizers
    - SGDlassifier/SGDRegressor
- **Vowpal Wappit**: For huge datasets that don't fit in memory 
    - FTRL (Follow the Regularized Leader)

### Regularization parameters
- *Regularization parameter (C, Lambda, alpha)*
    - Start with very small value and increase it
    - SVC starts to work slower as C (start with 10^-6) increases
- Regularization type
    - L1/L2/L1+L2 --try each
    - L1 can be used for feature selection

# Tips

- **Don't spend too much time tuning hyperparameters**
    Only if you don't have any more ideas or you have spare computational resources
- **Be patient**
    It can take thousands of rounds for GBDT or neural nets to fit
- **Average everything**
    - Over random seed
    - Or over small deviations from optimal parameters
        e.g. avergae max_depth=4,5,6 for an optimal 5

# Practice Quiz
1. Question 1: What can we do to deal with overfitting in LightGBM? (1 point)

    - Increase `bagging_fraction`
    - Increase `bagging_seed`
    - X Increase `min_data_in_leaf`
    - X Decrease `num_leaves`
    - Decrease `min_data_in_leaf`
<br /><br />
2. Question 2: What of the following parameter changes speed-up training process for LightGBM? That is, time needed for one boosting iteration is decreased. 1 point

    - X Decreasing bagging_fraction
    - X Decreasing num_leaves
    - Increasing max_bin
    - Decreasing verbosity
<br /><br />
3.  Question 3: How usually training time of SVM changes if we increase the value of parameter "C"? 1 point

    - X Training time increases
    - Training time decreases

# Quiz
1. Question 1: Which hyperparameters are first to tune in sklearn's RandomForest? 1 point

    - X n_estimators, max_depth, min_samples_split.
    - n_jobs, random_state, verbose.
    - bootstrap, oob_score, warm_start.
<br /><br />
2. Question 2: Suppose you fit LightGBM to your train data and check performance on the validation set. The train set consists of 500 rows and 1000 different features and validation set consist of 50 objects. You run automatic hyperparameter optimization method overnight and in the morning you select the best parameters, produce results for the test set and submit to the leaderboard. We also know that test set comes from the same distribution as train and validation sets. 1 point

    - There is a low chance of overfitting to the validation set. That is, there is a high chance that score on the test set will be good. This is because we found good parameters on validation set and test set is similar to the test set.
    - X There is a high chance of overfitting to the validation set. That is, there is a high chance that score on the test set will be bad. This is because we've tried too much hyperparameters while the dataset is small and the number of features is large.
<br /><br />
3. Question 3: Suppose you want to find a good set of hyperparameters for a dataset with 1000 points and have resources to do fitting 2000 times. Which method of model selection your should use? 1 point

    - Hold-Out scheme (i.e. divide data into two parts, use first for model fitting and second for estimation of quality).
    - Leave-one-out validation (i.e. fit model for all points except one and estimate quality for this single point; repeat for every point).
    - X k-Fold scheme (i.e. split data into k part, use k-1 parts for training and the last one for quality estimation; repeat for each part)
    - Select model by quality on training set (i.e. fit model on whole dataset and measure quality on the same data).
<br /><br />
4. Question 4: Suppose you train Neural Network with SGD and see that it overfits data. Which of the following actions can help you to regularize model? 1 point

    - Change optimization method to Adam.
    - Add more layers.
    - X Insert (or increase rate of) Dropout layers inside NN.
    - X Reduce number of parameters (e.g. remove some layers)
    - X Add (or increase) Weight Decay.