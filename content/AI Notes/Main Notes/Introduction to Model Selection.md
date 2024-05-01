---
title: Introduction to Model Selection
created: 2023-08-11T20:18:00
last modified: Friday 11th August 2023 20:18
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- When we have a classification problem, different models perform better depending on the problem, so how do we choose which model, or models, to try?
- When choosing a classification model, consider three factors related to the data:
	- Type of data
	- Size of the data
	- The complexity of the problem
- Is your data linear or non-linear? Meaning, can you separate the classes with a line or is there some overlap?
- If the decision boundary is non-linear or the classes are highly overlapping, a more complex algorithm like non-linear SVM or a decision tree may be required to accurately classify the data.
- See **Choosing the right estimator** from scikit-kearn [here]( https://scikit-learn.org/stable/tutorial/machine_learning_map/index.html)
- There are many other tools that you can use to automatically try different models and rank the results with a leaderboard system, such as [Amazon’s SageMaker](https://aws.amazon.com/sagemaker/autopilot/?sagemaker-data-wrangler-whats-new.sort-by=item.additionalFields.postDateTime&sagemaker-data-wrangler-whats-new.sort-order=desc)
---
>Related Notes: [[Intro to Classification]], [[Regression vs Classification]]

>Tags: #AI #SL 
