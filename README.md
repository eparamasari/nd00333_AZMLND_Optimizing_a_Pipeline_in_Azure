# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
This dataset contains data of direct phone call marketing of a Portuguese banking institution, taken from the University of California, Irvine machine learning repository (link: https://archive.ics.uci.edu/ml/datasets/Bank+Marketing.)

We seek to predict whether the customer decided to subscribe to the bank's product or not.

After comparing the results of hyperdrive run and automl run, the best performing model was one performed by automl, namely Voting Ensemble, with an accuracy of 0.91730.

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

The pipeline consists of data import --> data cleaning and one hot encoding --> data split into train and test sets --> setting of parameter sampling --> logistic regression instance creation --> model fitting --> model accuracy check --> model registration.

The parameters used in the hyperparameter tuning were C and max_iter. C is an inverse of regularization strength, where smaller values specify stronger regularization, while max_iter specifies the number of maximum iterations that can be taken for the solvers to converge.

Logistic regression was used since it is a good type of model for binary classification. It transforms its output using the logistic sigmoid function to return a probability value.

**What are the benefits of the parameter sampler you chose?**

The random sampling method was chosen in this case particularly because of the limited time available to do the run. This method uses less computation resources and takes less time, compared to other sampling methods such as grid sampling. This is due to the fact that random sampling randomly selects hyperparameter values from the defined seach space, while grid sampling performs a simple but exhaustive grid search over all possible values.

**What are the benefits of the early stopping policy you chose?**

The Bandit policy saves time and computation resources in running models that do not perform well, since it stops those models early, as soon as they are showing bad results.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

A total of 25 models were generated during the automl run, and Voting Ensemble was chosen as the best one.

Ensemble models are ensemble learning methods that combines different algorithms together, and Voting Ensemble predicts the class with the most votes from the different models.

The following hyperparameters were used: intercept_scaling=1, l1_ratio=None, max_iter=100, multi_class='ovr', n_jobs=1, penalty='l1', random_state=None, solver='saga', tol=0.0001, verbose=0, warm_start=False.

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

The accuracy of the custom-coded model with hyperdrive run was 0.9074355083459787, while the accuracy of the autoML best run was 0.9172988214259388. The automl was better by approximately 1.09%. Theoretically, the automl result was better since it was able to automatically compare different types of model to fit the data. Another advantage is that it is a lot faster to do so with automl, compared to having to reiterate different models manually, which will take significantly a lot more time. 

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

Here are some of the things that can be done for future improvement:
- One might try other classification models for the hyperdrive run. It would be interesting to see how the AutoML run compares to other classification models such as k-Nearest Neighbors or Decision Trees. 
- One can also try changing the options in the parameter sampler and/or the policy to see how it compares to automl, as well changing the parameter sampler itself to Bayesian sampling / grid sampling to see how they compare.
- A warning of possible data imbalance was received. One can use resampling to even the class imbalance, either by up-sampling the smaller classes or down-sampling the larger classes. Other metrics can also be used here, such as AUC or precision/recall instead of accuracy.
- One can change the number of cross validations and/or increase experiment timeout for automl to 60 minutes or more, to see if the accuracy of the best model can increase with more pipelines iterated.

## Proof of cluster clean up

The compute cluster deletion is included in the code.
