---
title: The K-Means Algorithm
created: 2023-07-15T11:30:00
last modified: Saturday 15th July 2023 15:54
aliases: 
tags:
  - AI
  - UL
type: Intro
---
- **K-Means** is an unsupervised algorithm that can help us to objectively and automatically group our data.
- K-Means takes a predetermined amount of clusters and then assigns each data point to one of those clusters.
- First, it assigns points to the closest cluster center.
![[four-cluster-centers.png]]
- Then, it re-adjusts the cluster's center by setting each center as the mean of all the data points contained within that cluster.
![[four-adjusted-cluster-centers.png]]
- The following image depicts how the K-Means algorithm repeats this process again and again, each time getting a little bit better at separating the data points into distinct groups. This process is described in five steps:

	Step 1: The algorithm randomly selects K-clusters.
	Step 2: Each object is assigned to a similar centroid randomly.
	Step 3: The cluster centers are updated based on the new means.
	Step 4: The data points are reassigned based on the new cluster centers.
	Step 5: The reassigned data points are shown without the cluster centers.
![[K-means-adjusted-cluster-centers.png]]
---
>Related Notes: 
>Tags: #AI #UL
