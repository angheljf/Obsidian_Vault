---
title: Prediction
created: 2023-08-05T15:20:00
last modified: Saturday 5th August 2023 15:20
aliases: 
tags:
  - AI
  - SL
type: Classification
---
- Continuation of [Activity 01-Logistic_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/01-Logistic_Regression)
- Use the `predict` function to classify our features and create a new DataFrame:
```python
# Generate predictions from the model we just fit
predictions = logistic_regression_model.predict(X_train)

# Convert those predictions (and actual values) to a DataFrame
results_df = pd.DataFrame({"Prediction": predictions, "Actual": y_train})
results_df
```
![[lr-demo-training-predictions-dataframe.png]]
- Test the model with new data:
```python
# Apply the fitted model to the test dataset
testing_predictions = logistic_regression_model.predict(X_test)

# Save both the test predictions and actual test values to a DataFrame
results_df = pd.DataFrame({
    "Testing Data Predictions": testing_predictions,
    "Testing Data Actual Targets": y_test})
results_df
```
![[lr-demo-testing-predictions-dataframe.png]]
- Evaluate the classifiers using the `accuray_score` function:
```python
# Import the accuracy_score function
from sklearn.metrics import accuracy_score

# Calculate the model's accuracy on the test dataset
accuracy_score(y_test, testing_predictions)
```
```text
1.0
```
- An extremely high metric should make you suspicious of overfitting.
- **Overfitting** means that the model is so good at predicting the correct target for the training data that it won’t perform well on new data that it wasn't trained on.
---
>Related Notes: [[Understanding Categorical Data]], [[Preprocessing]], [[Training and Validation]]

>Tags: #AI #SL 
