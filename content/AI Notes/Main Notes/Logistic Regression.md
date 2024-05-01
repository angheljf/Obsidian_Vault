---
title: Logistic Regression
created: 2023-08-05T15:30:00
last modified: Saturday 5th August 2023 15:30
aliases: 
tags:
  - AI
  - SL
type: Classification
---
- Refer to [Activity 01-Logistic_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/activities/01-Logistic_Regression) in order to see an example of the basic procedure to implement a logistic regression model.
- Initial DataFrame:
```python
# Read in the app-data.csv file into a Pandas DataFrame.
file_path = "https://static.bc-edx.com/mbc/ai/m4/datasets/app-data.csv"
app_data = pd.read_csv(file_path)

# Review the DataFrame
app_data.head()
```
![[app-dataframe.png]]
- Final columns of the initial DataFrame:
![[app-dataframe-final-columns.png]]
- Check total number of malware apps by using the `value_counts()` function:
```python
# The column 'Result' is the thing you want to predict.
# Class 0 indicates a benign app and class 1 indicates a malware app
# Using value_counts, how many malware apps are in this dataset?
app_data["Result"].value_counts()
```
```text
1    14700
0    14632
Name: Result, dtype: int64
```
- Separate data into `X` and `y` datasets:
```python
# The target column `y` should be the binary `Result` column.
y = app_data["Result"]

# The `X` should be all of the features.
X = app_data.copy()
X = X.drop(columns="Result")
```
- Split `X` and `y` into training and testing sets:
```python
# Split the dataset using the train_test_split function
X_train, X_test, y_train, y_test = train_test_split(X, y)
```
- Build the logistic regression model:
```python
# Declare a logistic regression model.
# Apply a random_state of 7 and max_iter of 120 to the model
logistic_regression_model = LogisticRegression(random_state=7, max_iter=120)
```
- **Explanation for the `max_iter` param:** It specifies the maximum number of iterations for the solver to converge. The solver is an optimization algorithm used to find the optimal weights for the logistic regression model. If the solver has not converged after `max_iter` iterations, it will stop and return the current weights as the solution. Increasing `max_iter` can improve the accuracy of the model, but it can also increase the training time.
- Fit the data to the untrained model:
```python
# Fit and save the logistic regression model using the training data
lr_model = logistic_regression_model.fit(X_train, y_train)
```
- Validate the model by using the `score()` function:
```python
# Validate the model
 print(f"Training Data Score: {lr_model.score(X_train, y_train)}")
 print(f"Testing Data Score: {lr_model.score(X_test, y_test)}")
```
```text
Training Data Score: 0.9594527023955635
Testing Data Score: 0.9605891176871676
```
- Make predictions using the `predict()` function:
```python
# Make and save testing predictions with the saved logistic regression model using the test data
testing_predections = lr_model.predict(X_test)

# Review the predictions
testing_predections
```
```text
array([1, 0, 0, ..., 1, 1, 1])
```
- Compare predictions against `y_test` using the `accuracy_score` function:
```python
# Display the accuracy score for the test dataset.
accuracy_score(y_test, testing_predections)
```
```text
0.9605891176871676
```
---
>Related Notes: [[Understanding Categorical Data]]

>Tags: #AI #SL 
