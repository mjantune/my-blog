---
title:  "Predictive Modelling with Azure Machine Learning Studio"
categories: coursera azure
author: "Manuel"
toc: true
toc_sticky: true
---

In this course, we are going to focus on three learning objectives:

- Build a predictive model using Azure ML Studio.
- Demonstrate a working knowledge of setting up experiments on Azure ML Studio.
- Operationalise machine learning work flows with Azure's drag-and-drop modules.

By the end of this course, you will be able to train and evaluate a predictive model on Azure Machine Learning Studio, all without writing a single line of code! You will predict flight delays using weather data provided by the US Bureau of Transportation Statistics and the National Oceanic and Atmospheric Association (NOAA).

#Course Structure

This course is divided into 3 parts:

- Course Overview: This introductory reading material.
- Feature Engineering and Custom Models Project: This is the hands on project that we will work on in Rhyme.
- Graded Quiz: This is the final assignment that you need to pass in order to successfully complete the course and earn a Course Certificate.

# Project Structure

The hands on project on Predicting Flight Delays Using Weather Data on Azure Machine Learning Studio is divided into the following tasks:

## Task 1: Introduction and Setup Instructions

- Introduction to the Rhyme interface.
- Azure Machine Learning Studio is a GUI-based integrated development environment for constructing and operationalizing machine learning workflows on Azure.
- In this task, we will signup for an ML Studio account and avail $200 worth of free credits to create our machine learning experiments! 

## Task 2: Importing the Data Sets

- We start by signing in to our Azure ML Studio account.
- Next, we create a blank experiment and use the drag and drop module to import our two data sets: [Flight On-Time Data](https://www.transtats.bts.gov/ONTIME/) from the US Bureau of Transportation Statistics, and [Weather Data](https://www.ncdc.noaa.gov/cdo-web/datasets) from the National Oceanic and Atmospheric Administration.
- Lastly, we convert our input data to the internal Dataset format used by Azure ML Studio. This is done using the [Convert to Dataset](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/convert-to-dataset) module.

![Screenshot Task 2]({{ site.baseurl }}/assets/images/Importig-the-Data.png)

## Task 3: Scrubbing Missing Values

- Now that we have imported the data, it's time to get a sense of its properties so that we can make informed decisions when pre-processing.
- We use the [Summarize Data](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/summarize-data) module to generate and visualize descriptive statistics for the columns in the data.
- Dealing with missing data is an essential pre-processing step. There are a number of ways to impute data. We will use the [Clean Missing Data](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/clean-missing-data) module to substitute all missing values in our data with 0.

![Screenshot Task 3]({{ site.baseurl }}/assets/images/Scrubbing-Missing-Values.png)

## Task 4: Eliminating Target Leaks

- Since the data set is made available to the general public and not specifically created for our machine learning problem, it contains additional data that we don't want going into our model.
= Some of these columns are known as target leaks and need to be removed. To actually use the model in real life, we will not have access to information such as the number of minutes the flight was delayed, since we're trying to predict that in the first place.
- So, in this task, we will use the [Select Columns in Dataset](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/select-columns-in-dataset) module to exclude the target leaks from our input.

## Task 5: Conversion to Categorial Features

- In this task, we use the [Edit Metadata](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/edit-metadata) module to convert three columns to categorical feature types.

![Screenshot Task 4_5]({{ site.baseurl }}/assets/images/Task_4_5.png)

## Task 6: Preparing Features to be Joined with Weather Data

- Our strategy is going to be to join this dataset with the Weather dataset. We want to join them by time. Since we don't have weather information by the minute, we will join by the hour of the day.
- To extract the hour from this value, we will use the [Apply Math Operation](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/apply-math-operation) module to divide the columns of interest by 100 in-place. Since we want just the hour, we will use another Apply Math Operation module to round the number down.

![Screenshot Task 6]({{ site.baseurl }}/assets/images/Task_6.png)

## Task 7: Preprocessing the Weather Dataset

- For the Weather Data, we will have to do a lot of the same things as we did earlier.
- We scrub any missing data, convert a few columns to categorical feature types, and extract the hour values adjusted for time zones.

![Screenshot Task 7]({{ site.baseurl }}/assets/images/Task_7.png)

## Task 8: Joining Both Datasets

- Once we have completed pre-processing the Flight Delay and Weather data, we can use the [Join Data](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/join-data) module to join them together.
- For both datasets, we need to specify the same columns which we want to use to join.

![Screenshot Task 8]({{ site.baseurl }}/assets/images/Task_8.png)

## Task 9: Training and Evaluating the Model

- In this final task, our goal is to train and evaluate a binary logistic regression model.
- Using the [Split Data](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/split-data) module, we partition our data into 80/20 train/test splits.
- We train the [Two-Class Logistic Regression](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/two-class-logistic-regression) module on the train split and evaluate its performance on the test split using the [Score Model](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/score-model) and [Evaluate Model](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/evaluate-model) modules.

![Screenshot Task 9]({{ site.baseurl }}/assets/images/Task_9.png)
