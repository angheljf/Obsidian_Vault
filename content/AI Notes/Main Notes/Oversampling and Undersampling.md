---
title: Oversampling and Undersampling
created: 2023-09-08T20:18:00
last modified: Friday 8th September 2023 20:17
aliases: 
tags:
  - AI
  - UL
  - SL
type: Imbalanced
---
- There are several techniques that exist for dealing with imbalanced training data, and the majority fall under either the oversampling or undersampling umbrellas.
- **Oversampling** deals with creating more instances of the minority class in order to balance the dataset, as shown in the following figure:
![[oversampling-concept-visual-aid.png]]
- **Undersampling** deals with creating fewer instances of a class label, or cutting data points from the majority class until the amount of data points in each class matches up. However, there must remain enough data in the undersampled majority class for the model to remain useful:
![[undersampling-concept-visual-aid.png]]
- Depending on your needs you may also use a combination of the two with a combination sampling method.
- There are two key sampling methods that can be used to obtain new samples for your dataset, namely **random sampling** and **synthetic sampling**.
	- With random sampling, the algorithm chooses random instances from the existing dataset. We can use either oversampling or undersampling when sampling randomly.
	- With **synthetic sampling**, the algorithm generates new instances from observations about existing data.
![[resampling-tree.png]]
---
>Related Notes: [[Intro to Imbalanced Data]]

>Tags: #AI #UL #SL 
