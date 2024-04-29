---
title: The Elbow Method
created: 2023-07-15T21:15:00
last modified: Saturday 15th July 2023 21:15
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- When working with a new unlabeled dataset with many features, we often find it difficult to identify the value to use for `k`.
- The **Elbow method** is the most well known method available for determining the optimal value for `k`.
- Also worth considering is the **Silhouette method** described [here](https://towardsdatascience.com/silhouette-method-better-than-elbow-method-to-find-optimal-clusters-378d62ff6891) and [here](https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html)
- We use the Elbow method to find the optimal value for `k`–that is, to determine how many clusters best fit the data.
- The elbow method runs the K-means algorithm for a range of possibilities for `k`. The resulting elbow curve plots the values for `k` (number of clusters) on the x-axis, and the measure of inertia on the y-axis. Inertia is commonly used as an objective function.
- **Inertia** measures how distributed or spread out the data points are within a cluster.
![[clusters-inertia.png]]
- The more clusters you have in a dataset, the smaller the measure of inertia is for each cluster.
- You can find the optimal value for k at the elbow of the curve, or when the measure of inertia (y-axis) shows minimal change for each additional cluster added (x-axis) to the dataset.
![[simple-elbow-curve.png]]
---
>Related Notes: [[Clustering]]
>Tags: #AI #UL 
