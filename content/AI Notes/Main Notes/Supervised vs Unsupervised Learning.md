---
title: Supervised vs Unsupervised Learning
created: 2023-07-22T20:30:00
last modified: Saturday 22nd July 2023 20:36
aliases: 
tags:
  - AI
  - UL
  - SL
type: Intro SL
---
- In supervised learning, we use labeled data and in unsupervised learning, we use unlabeled data in order to find patterns.
- The following figure illustrates the differences in how data is plotted using using a classification supervised learning model vs using a clustering unsupervised learning model:
![[supervised-v-unsupervised-plot.png]]
- The following table summarizes the main differences between supervised and unsupervised learning:

|                    | Supervised Learning                                                                 | Unsupervised Learning                                                         |
| ------------------ | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Human Intervention | Needed                                                                              | Limited                                                                       |
| Data               | Labeled                                                                             | Unlabeled                                                                     |
| Tools              | Linear and logistic regression, decision trees, and support vector machines         | Clustering and dimensionality reduction                                       |
| Model              | Regression and classification                                                       | Clustering and association                                                    |
| Action             | Model is trained to use known results and update the model's parameters             | Model segments the data into groups or reduces the dimensionality of the data |
| Goal               | Forecast and predict a predefined output                                            | Find hidden patterns in the data                                              |
| Results            | Results include metrics that can reflect the model's ability to generalize the data | Exploratory results that help identify groups or anomalies within the data    |
| Disadvantages      | Labeled data is always required. Models may suffer from overfitting or underfitting | May not produce meaningful results. The results are always subject to interpretation|                                                                              |

---
>Related Notes: [[What is Unsupervised Learning]]

>Tags: #AI #UL #SL 
