---
title: Linear Models
created: 2023-08-12T20:30:00
last modified: Saturday 12th August 2023 18:30
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- Logistic regression defines a line to separate two sets of data, that might result in the misclassification of new data.
- The following image illustrates how different lines could classify a data point into different classes:
![[which-line-classification-plot.png]]
- **Support Vector Machine** or SVM can separate classes of data into multidimensional space by plotting data points with dimensions.
- Therefore, SVMs can employ both a linear and non-linear approach when predicting outcomes.
- Once all the data points are plotted, we can create a **hyperplane**. A hyperplane is a line that delineates data points into different classes.
- The following image shows an optimal hyperplane with the widest margin of separation of the data points that is equidistant for all classes.
![[svm-optimal-hyperplane.png]]
- The data points closest to, or within the margin of, the hyperplane are called **support vectors**. Support vectors are used to define the boundaries of the hyperplane.
![[support-vectors.png]]
- **Note**: When support vectors fall within the margin of the hyperplane, these data points should be considered errors. In such instances, the classification should not be relied on because the data points in that range are equally likely to be in either class as shown in the following image.
![[svm-hyperplane-overlapping-data.png]]
- Hyperplanes can be 3D in order to clearly delineate classes with non-overlapping data points or outliers, as shown in the following image:
![[svm-3d-hyperplane-orientation.png]]
- Hyperplanes also support what’s considered zero tolerance with perfect partition, which is a non-linear hyperplane that will position and orient the hyperplane to correctly classify overlapping or outlying data points.
![[nonlinear-hyperplane-in-2d.png]]
- SVM is often more beneficial than logistic regression because the model supports the classification of outliers and overlapping data points. Also, for many datasets, SVM can provide higher accuracy with less computation power.
---
>Related Notes: [[Linear vs Non-linear Data]], [[Logistic Regression]]
>Tags: #AI #SL 
