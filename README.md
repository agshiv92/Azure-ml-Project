# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
The data set contains data related to a direct marketing campaigns of a financial institution. The problem setting is a binary classification where our project goal is to predict whether a client will subscribe a term deposit (that is outcome variable y). In the original dataset we have 17 possible predictor variables, both numeric and categorical ones.

During the project we would like to predict whether a given client with a set of previously known attributes (set of inputs) would or would not subscribe a term deposit.

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

## AutoML
We compared our previous models to a more-or-less fully automated autoML run. During that no preprocessing step is necessary, thus we just defined the task tpye, set some config parameters and referenced the train and validation datasets which were made available to our workspace in a previous step.

After the execution the job, it resulted in VotingEnsemble as the best performing model, based on the validation set. As in the previous experiments we downloaded the resulting model and evaluated it on the held-out test set. The VotingEnsemble model can be considered as a meta-model or a model-of models, since it combines the predictions from multiple other models.

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
