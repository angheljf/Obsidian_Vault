---
title: Model Evaluation
created: 2023-07-28T20:33:00
last modified: Friday 28th July 2023 20:32
aliases: 
tags:
  - AI
  - SL
type: Intro SL
---
- They are different methods to test the accuracy of a supervised learning model.
- **Resampling methods**: Resampling involves rearranging data samples to assess whether the model performs well on different samples to the ones used to train it. Resampling helps us discern whether the model will generalize well.
- **Random split methods**: Random splits entail randomly dividing the data into at least two sets, a training set and a testing set. Sometimes, you can randomly divide the data to include a second test set, which is called a validation set.
- **Time-based split methods**: Time-based splits require data to be reserved for a certain number of time intervals for testing. The model is trained using the immediately preceding time intervals. Time-based splits are important when randomly mixing the data would scramble the pattern in time-series data.
- **K-fold cross-validation methods**: Cross-validation involves randomly shuffling the dataset and splitting it into k groups. One group is reserved as the test set and all the other groups are combined into the training set.
- There are many metrics for evaluating a model’s accuracy, precision, and recall.
- We’ll primarily use the mean squared error (MSE) and R-squared (R2) for linear regression.
- **Note**: MSE and R<sup>2</sup> are defined in the [[Model Evaluation - Quantifying Regression]] note.
---
>Related Notes: [[Model-Fit-Predict]]
>Tags: #AI #SL 
