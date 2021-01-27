# Optimizing an ML Pipeline in Azure

## Overview
In this project, we are making and optimizing an Azure ML pipeline using the Python SDK and a provided SK learn model.
The end task is to compare the manual model with Azure AutoML run.

## Summary
The data set contains information about the financial institution's direct marketing campaigns. Problem planning is a binary split where our project goal is to predict whether the client will pay a term deposit (those are variable results y). In the original database we have about 17 prediction variables, both numerical and catagorical.


During the project we would like to predict whether a given client with a pre-defined token collection (input group) will pay or will not register.

We would construct a default Ml pipeline for that with the basic steps of:

Data cleaning and preparation
Model building - including optimizing the hyperparameters as well (on a test/valid set).
Model performance evaluation step on a held-out-set.
Thus we would use all the 3 part of the dataset namely the train / test / validation sets for different purposes. We show how to set up the above pipeline from a jupyter-notebook and execute it through the Azure ML studio. For the hyperparameter tuning part we use Hyperdrive functionality of the ML-studio.

## Scikit-learn Pipeline
As a benchmark implementation we chose the logistic-regression model from the scikit-learn package. As a first iteration we execute the complete pipeline in a single step, namely:

1. Preprocess and cleanse the data
2. Model-fitting / hyperparameter tuning
3. Evaluation on a held-out-set

As baseline solution for the classification problem we choose logistic regression. In the scikit-learn implementation we choose to optimize the C regularization parameter along with the max_iter parameter for controlling the possible number of iteration until the algorithm converge.

The optimization policy defines the early termination strategy of the executed runs, namely un that doesn't fall within the slack factor or slack amount of the evaluation metric with respect to the best performing run will be terminated. The early termination policy helps with the compute efficiency since it cancels the least promising runs during the experiment.
*learning_rate: - controlling the learning - shrinkage rate
*max_depth: limit the max depth for tree model
*num_leaves: max number of leaves in one tree
*min_data_in_leaf: minimal number of data in one leaf
*num_iterations: number of boosting rounds

We are using RandomParameterSampling because we can greatly reduce computation costs and speedup up the exploration of the parameter space.
Given the low dimensionality of the UCI Bank Marketing dataset, and the small number of hyperparameter to tune random sampling is a better choice w.r.t. GridSearch

## AutoML
We compared our previous models to a more-or-less fully automated autoML run. During that no preprocessing step is necessary, thus we just defined the task tpye, set some config parameters and referenced the train and validation datasets which were made available to our workspace in a previous step.

After the execution the job, it resulted that there is no significant difference between manual and Auto ML based on the validation set. Auto ML can save a huge amount of time with trade of little accuracy
The best model generated by AutoML is a VotingEnsemble method with a pre-processing step that uses.
The Ensemble consist of two models, namely XGBoostClassifier and SGDClassifier, which use a StandardScaler and MaxAbsScaler as pre-processing step, respectively

## Pipeline comparison
There is very little difference between the accuracy of model. Althoug the manual is performing better in terms of accuracy but there is very little difference between two different model

## Future work
Yes we can different model and different run. We can also change the estimator. But the most important thing we can do is feature engineering based on the domain knowledge. This will help us to generate more columns. Now Auto ML can take these columns and gives better performance

