---
title:  "Coursera - Tips and Tricks - KazAnova's competition pipeline"
categories: coursera data_science
author: "Manuel"
toc: true
toc_sticky: true
---

# The Pipeline
1. Undertand the Problem (1 day)
2. Exploratory analysis (1-2 days)
    a. Define cross validation strategy
3. Feature engineering (until last 3-4 days)
4. Modeling (Until last 3-4 days)
5. Ensembling (last 3-4 days)

# Understand broadly the problem
- Type of problem
    - Image classification
    - Sound classification
    - Text classification
    - Optimization problem

- Type of Dataset
    - Tabular Dataset
    - Image Dataset
    - Time series?

- How BIG is the data (How much I need?)?
- Hardware needed (CPU's, GPU's, RAM, Disk space)
- SOftware needed
    - Keras and Tensor Flow
    - LightBGM
    - ScikitLearn
    - XGBoost

- Create an Anaconda Environment of a Virtual Environment
- What is the metric being tested on?

# Do some EDA
- Plot histograms of variables. Check that a feature looks similar between train and test
- Plot features versus the target variable and vs time
- Consider univariate predictability metrics (Information Value, Chi Squared, AUC)
- Binning numerical features and orrelation matrices

# Define a Cross Valdation Strategy
- This step is critical. Its success is a good indicator for what is going to happen in the competition
- People have won by just selecting the right way to validate
- Create a validation approach that best resembles what you are being tested on
- **Is time important?** Split by time. **Time-based validation**
- Different entities than the train. **Stratified validation**
- Is it completely random. **Random validation** (random k-fold)
- Combination of all the above
- Use test leader board to test

# Feature Engineering
The type of problem define sthe feature engineering.
- **Image Classification**: (suggestion: previous data science bowls)
    - Sclaing
    - Shifting
    - Rotations
    - CNNs.
- **Sound Classification**: (Tenso Flow speech recognition)
    - FOurier
    - MFCC
    - Spectrograms
    - Scaling
- **Text Classification**: (StumbleUpon Evergreen Classification)
    - tf-idf,
    - SVD
    - Stemming
    - Spell Checking
    - Stop Words removal
    - X-grams
- **Time Series**: (Walmart Recruiting)
    - Lags
    - Weighted Averaging
    - Exponential Smoothing
- **Categorical** (Amazon Employee)
    - Target enc
    - Frequancy Encoding
    - One-hot Encoding
    - Ordinal
    - Label Encoding
- **Numerical** (Africa Soil)
    - Scaling
    - Binning
    - Derivatives
    - Outlier Removals
    - Dimensionality reduction 
- **Interactions** (Homesite):
    - Multiplications
    - Divisions
    - Group-by Features
    - Concatenations
- **Recommenders** (Acquire Valued Shoppers)
    - Featurs on trnasactional history
    - Item popularity
    - Frequency of Purchase
- This process **can be automated** using selection with cross validation

# Modeling
The type of problem defines the feature engineering
- **Image classification**: CNNs (Resnet, VGG, densenet...)
- **Sound Classification**: CNNs (CRNN), LSTM
- **Text classification**: GBMs, Linear, DL, Naive bayes, KNNs, LibFM, LIBFFM
- **Time Series**: Autoregressive models, ARIMA, linear, GBMs, DL, LSTMs
- **Categorial Features**: GBMs, Linear Models, DL, LibFM, LibFFM
- **Numerical Features**: GBMs, Linear models, DL, SVMs
- **Intercations** GBMs, Linear Models, DL
- **Recommenders**: CF, DL, LibFM, LIBFFM, GBMs

# Ensembling
- All this time, predictions on internal validation and test are saved. (If collaborating with others, this is the point where everyone passes on their predictions as CSV files)
- Different ways to combine from averaging to multilayer stacking.
- Small data requieres simpler esemble techniques (like averaging)
- Helps to average a few **low-correlated predictions** with good scores
- Bigger data can utilize stacking
- Stacking process repeats the modelling process.

# Tips on collaboration
- Its more fun.
- You learn more.
- You score better.
- Different points of view (See the problem from different angles)

# Final Tips
- In these challenges you never lose. You may not win prize money, BUT you always gain in terms of knowledge, experience, meeting/collaborating with talented people in the field, boost your CV.
- Coffee is kind of a must when you do this
- See it like a game
- Take a break often to rest ou mind - do some physical exercise as it is unhealthy sitting on a chair many hours
- The kaggle community may be the most kind, helpful community I have ever experienced in any social context
- After the competition look for people sharin approaches
- Create a notebook with useful methods and update it