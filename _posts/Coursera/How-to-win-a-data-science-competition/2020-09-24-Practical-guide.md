---
layout: post
title:  "Coursera - Tips and Tricks - Practical Guide"
categories: coursera data_science
author: "Manuel"
---

# Check the objective of entering a competition
- For example, if you are interested in data science, in application to medicine, you can try to predict lung cancer in the Data Science Bowl 2017. Or to predict seizures in long term human EEG recordings, in the Melbourne University Seizure Prediction Competition
- If you want to get acquainted with new software tools, you may want the competition to have required tutorials. For example, if you want to learn a neural networks library. You may choose any of competitions with images like the nature conservancy features, monitoring competition. Or the planet, understanding the Amazon from space competition.


# After you enter a competitios: Working with ideas
1. Organize ideas in some structure
    1.1. Check forums and look for ideas in the forum
2. Select the most important and promising ideas
3. Try to undestand the reasons why somehing does/doesn't work

# After you enter a competition: Everything is a hyperparameter
Sort all parameters by these principles:
1. Importance: Arrange parameters from important to not useful at all
2. Feasibility: From it is easy to tune, to it can take forever to tune
3. Understanding: From I undertand 

Note: Changing one parameter can affect the whole pipeline

e.g.
- For example if you increase the number features significantly, you may want to change the ratio of columns which is used to find the best split.
- If you change the number of layers in a CNN you will need more epochs to train it.

# Data Loading
- Usually start with basic date preprocessong, like label encoding categorical data.
- Do basic preprocessing and convert csv/txt files into hdf5/npy for much faster loading
    - HDF5 for Pandas dataframes
    - NPY for non bit arrays
- Do not forget that by default data is stored in 64-bit arrays, most of the time you can safely downcast it to 32-bits
- Large datasets can be processed in chunks
    - Panda's support out of the box data relinks via chunk size parameter in read_csv function.
    - Most of the datasets may be preprocessed without a lot of memory

# Performace evaluation
- Extensive validation is no always needed
    - You can validate your models with a simple train test split
- Start with fastest models - LightGBM
- It is recommended to use early stopping, so you don't need to tune the number of boosting iterations.
- Don't start with SVM, Random Forests or Neural Networks, you will waste too much time waiting for them to fit
- Switch to tunning models, ensembling and stacking only when you are satisfyed with feature engineering

# Fast and Dirty always better
- Don't pay too much attention to code quality
- Keep things simple: save onl important things, don't track every little change
- If you feel uncomfortable with given computational resources - rent a larger server

# Initial pipeline
- Start with simple (or even primitive) solution
- Debug full pipeline: From reading data to writing submission file
    - The main purpose of such solution is not to build a good model but to debugthe full pipeline from the beginning.
- "From simple to complex"
    - For example, start with random forest, rather than Gradient Boosted Decision Trees

# Best Practices from Software Development.
- Use good variable names
    - If your code is hard to read you will definitely will have problems sooner or later.
- Keep your research reproducible
    - Fic random seed
    - Write down exactly how any features were generated
    - Use version control Systems (Git)
- Reuse code
    - Especially important to use the same code for train and test stages
    - Move reusable code into separate functions or a separate model

# Read papers
- This can get you ideas about ML-related things
    - For example, how to optimize AUC
- Way to get familiar with problem domain
    - Especially useful for feature generation

# My pipeline
- Read forums and examine kernels first
- Start with quick EDA and a simple baseline
    - To make sure data is loaded correctly
    - To check if validation is stable
- Add features in bulks
    - Create all the feature you can make up
    - Evaluate many features at once (not "add one and evaluate")
- Hyperparameter optimization
    - First find parameters to overfit train dataset
    - And then try to trim the model

# Code organization: keeping it clean
- Very mportant to have reproducible results
    - Keep important code clean
- Long execution history leads to mistakes (too many defined global variables)
- Remember to sometimes reestart your notbooks
- One notebook per submission
- Before creating a sumission restart the kernel
    - Use "Restart and run all" button

- Split train.csv intro train and val with structure of train.csv and test.csv
{% highlight python %}
train = pd.read_csv('data/train.csv')
test = pd.read_csv('data/test.csv')
{% endhighlight %}

{% highlight python %}
from sklearn.model_selection import train_test_split

# train set into new train and validation
train_train, train_val =  train_test_split(train, random_state = 660)

# save to dik
train_train.to_csv('data/val/train.csv')
train_val.to_csv('data/val/val.csv')
{% endhighlight %}

- When validating, set it at the top of the notebook
{% highlight python %}
train_path = 'data/val/train.csv'
test_path = 'data/val/val.csv'
{% endhighlight %}

- To retrain models on the whole dataset and get predictions for test set just change:
{% highlight python %}
train_path = 'data/train.csv'
test_path = 'data/test.csv'
{% endhighlight %}

# Code Organization: 
- Macros
