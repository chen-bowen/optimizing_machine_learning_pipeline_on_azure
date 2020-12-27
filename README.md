# Optimizing an ML Pipeline in Azure

## Overview

(This project is part of the Udacity Azure ML Nanodegree.)\
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model in Azure ecosystem.
This model is then compared to an Azure AutoML run on the same problem. This project serves as a prime example of running machine learning tasks on a well-known cloud service provider 

## Summary

In this project, we seek to use around 40 different demographical and event-related features to predict whether the user will eventually subscribe a term deposit. We will use sklearn's logistic regression framework, and tune its hyperparameters with HyperDrive. We will also utilize Azure's autoML feature to find us the best model for the bank marketing prediction problem.

## Scikit-learn Pipeline Architecture

### HyperDrive architecture

The hypedrive pipeline is built with these order of sequence

1. create the experiment inside the workspace
2. configure the compute cluster
3. create an sklearn estimator by setting up the main functionalities in the `train.py` script (including data preprocessing and model fitting)
4. use the `train.py` script as the entry point, create the `ScriptRunConfig` object 
5. use `ScriptRunConfig` object as entry point, create the `HyperDriveConfig` object
6. submit the `HyperDriveConfig` object for execution

**benefits of the bayesian parameter sampler**

Using the BayesianParameterSampling sampler gives us a smart way to try a large range of hyperparameters to achieve the best performance. Using BayesianParameterSampling achieves comparable, if not better, performances compared to the brute force grid search parameter sampler.

**benefits of the early stopping policy**

Using the Bandit stopping policy allow us to cancel the runs that are using hyperparameters that lead to really bad performances. This will save us valuable runtime and computing resources to avoid paying for runs we would not use.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

The AutoML pipeline is built with these order of sequence

1. create dataset from TabularDataSet object
2. configure AutoML settings by creating the `AutoMLConfig` object
3. create a designated experiment in the workspace
4. submit the `AutoMLConfig` object for execution

AutoML generates a variety of different models ranging from linear models to tree based models to essemble models. The best model is the voting essemble models, generating 0.9482 weighted AUC metric.

## Pipeline comparison

**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

The best model returned by autoML is the VotingEssemble algorithm that returns an accuracy of 0.9143, compare to the logistic regression returns an accuracy metric of 0.9124

## Future work
Some more detailed feature engineering prior to feeding the model into autoML would probably improve the accuracy/AUC by a lot. Combining the power of feature engineering and autoML will allow us to automatically try a lot of different models on already nicely engineered features.