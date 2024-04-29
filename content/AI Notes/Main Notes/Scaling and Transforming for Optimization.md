---
title: Scaling and Transforming for Optimization
created: 2023-07-17T10:27:00
last modified: Monday 17th July 2023 10:26
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- Prior to applying **PCA** (Principal Component Analysis), the features of the data must be transformed by applying standard scaling.
- The numeric values in our data must all have the same scale in order to prevent K-means from putting too much weight on any single variable.
- When we **scale** data, we eliminate the measurement units and scale the numeric values to a similar scale.
- The most common way to scale data is to apply **standard scaling**, which is a method of centering values around the mean, as shown in the following images:
![[before-scaling.png]]

![[after-scaling.png]]
- We can use the `StandardScaler` function from the `scikit-learn` library. The `StandardScaler` will transform our data by calculating the mean value of the column and scaling the data in the column to a standard deviation of 1.
- After scaling this way, the data has a mean of 0 and a standard deviation of 1. In statistics, this is referred to as **data standardization**.
---
>Related Notes: 
>Tags: #AI #UL 
