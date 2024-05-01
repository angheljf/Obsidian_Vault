---
title: Model Evaluation - Quantifying Regression
created: 2023-07-30T20:32:00
last modified: Sunday 30th July 2023 20:32
aliases: 
tags:
  - AI
  - SL
type: Linear Regression
---
- There are a variety of ways to quantify models, but there are three very common quantification scores:
	- **R-squared (R<sup>2</sup>)**: This metric indicates how well the model accounts for variability of the data. R2 can fall between -1 and 1, and higher values signify that the model is highly predictive. An R2 value of 0.85 means that the model accounts for 85% of the variability of the data.
	- **Mean squared error (MSE):** This metric indicates how accurately the model predicts every data point. MSE is sensitive to outliers. MSE is a function of the training data, so the MSE will vary widely between projects. Use MSE to compare models trained on the same data, but not to compare models trained on different data.
	- **Root mean squared error (RMSE):** Just like MSE, RMSE can be used to compare the predictive capacity of various models for the same dataset.
- We will continue the [[Making Predictions with Linear Regression]] exercise in order to evaluate the model we created
- Import the necessary libraries and calculate the R<sup>2</sup>, MSE, and RMSE:
```python
from sklearn.metrics import mean_squared_error, r2_score

# Compute the metrics for the linear regression model
score = round(model.score(X, y, sample_weight=None),5)
r2 = round(r2_score(y, predicted_y_values),5)
mse = round(mean_squared_error(y, predicted_y_values),4)
rmse = round(np.sqrt(mse),4)

# Print relevant metrics.
print(f"The score is {score}.")
print(f"The r2 is {r2}.")
print(f"The mean squared error is {mse}.")
print(f"The root mean squared error is {rmse}.")
```
```text
The score is 0.95696.
The r2 is 0.95696.
The mean squared error is 31270951.7223.
The root mean squared error is 5592.0436.
```
- Note that R<sup>2</sup> is the default score for `sklearn`’s linear regression model.
---
>Related Notes: [[Model Evaluation]]

>Tags: #AI #SL 
