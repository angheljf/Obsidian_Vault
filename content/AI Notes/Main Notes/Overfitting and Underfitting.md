---
title: Overfitting and Underfitting
created: 2023-08-26T18:32:00
last modified: Saturday 26th August 2023 18:31
aliases: 
tags:
  - AI
  - UL
  - SL
type: Optimization
---
- When evaluating the performance of a machine learning model, you also need to assess the model for its fit, as an overfit or underfit model can introduce bias and variance that will skew your results.
- **Underfitting** is a common problem in machine learning where a model fails to capture the relationship between the input data and the output variable sufficiently.
- **Overfitting** occurs when a model finds patterns and relationships in the training data that aren’t representative of the dataset as a whole.
- The following image offers a visual representation of over- and underfitting in identifying data patterns:
![[fitting-overfitting-underfitting-comparison.png]]
- Overfitting and underfitting can impact the usefulness of your model’s predictions by introducing bias and variance into the results, two significant causes of data prediction errors.
- A model with **high bias** is likely to produce similar results regardless of the particularities of a given dataset.
- A model with **high variance** will result in significant prediction error when confronted with new data due to its inability to generalize data trends effectively.
- In order to develop an effective predictive model, you must pay attention to balancing out bias and variance.
- One way to avoid this is to ensure that your model’s performance is tested and measured on fresh data on which it was not trained.
---
>Related Notes:
 
>Tags: #AI #UL #SL 
