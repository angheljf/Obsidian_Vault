---
title: Overfitting
created: 2023-08-18T21:02:00
last modified: Friday 18th August 2023 21:02
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- Decision trees are a complex model that can very accurately capture patterns in the training data but may fail to make good predictions with new data. That is, they can **overfit** the data.
- The following image illustrates the case where the classification line correctly identifies all the training data points but deviates to incorrectly identify some of the testing data points:
![[classification-overfitting.png]]
- A model that accurately predicts each training data point but misses a significant number of testing data points overfits the data.
- When overfitting occurs, it is generally because the data is too complex for the model, and the patterns it has learned are too specific to the training dataset.
- One solution to reduce overfitting, and therefore variance, is to reduce complexity.
---
>Related Notes: [[Decision Trees]]
>Tags: #AI #SL 
