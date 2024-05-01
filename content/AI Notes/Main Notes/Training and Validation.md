---
title: Training and Validation
created: 2023-08-04T21:02:00
last modified: Friday 4th August 2023 21:02
aliases: 
tags:
  - AI
  - SL
type: Classification
---
- Continuation of [Activity 01-Logistic_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/01-Logistic_Regression)
- Create our Logistic Regression model:
```python
# Import LogisticRegression from sklearn
from sklearn.linear_model import LogisticRegression

# Define our model
logistic_regression_model = LogisticRegression()
```
- Train the model using the `fit` function:
```python
# Fit the model
logistic_regression_model.fit(X_train, y_train)
```
- The following animation shows an example of fitting a logistic regression to a dataset that has two labels: `0` and `1`:
![[logistical-regression-fit.gif]]
- As the fitting proceeds, the S-curve becomes sharper—meaning that the logistic regression is achieving a better distinction between the labels.
- Score the model using the `score` function:
```python
# Score the model
print(f"Training Data Score: {logistic_regression_model.score(X_train, y_train)}")
print(f"Testing Data Score: {logistic_regression_model.score(X_test, y_test)}")
```
```text
Training Data Score: 1.0
Testing Data Score: 1.0
```
- If the training score is significantly more accurate than the testing score (closer to 1.0), the model may be overfitted.
---
>Related Notes: [[Understanding Categorical Data]], [[Preprocessing]]

>Tags: #AI #SL 
