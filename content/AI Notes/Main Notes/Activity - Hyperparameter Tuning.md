---
title: Activity - Hyperparameter Tuning
created: 2024-04-29T11:37:00
last modified: 2024-04-29 11:37
aliases: 
tags:
  - AI
  - UL
  - SL
type: Tuning
---
- Refer to [Activity 03-Hyperparameters](file:///C:/Users/anghe/Documents/Work/mbc-ai/05-ML-Optimization/activities/03-Hyperparameters) in order to see an example on how to use `GridSearchCV()` and `RandomizedSearchDV()` to choose the parameters for a KNN model.
- Initial DataFrame:
```python
# Read the CSV file into a Pandas DataFrame
df = pd.read_csv('https://static.bc-edx.com/mbc/ai/m5/datasets/numeric_bank.csv')

# Review the DataFrame
df.head()
```
![[numeric-bank.png]]
- Separate the data (X) from the target column (y):
```python
# Define the target and the target_names variables
target = df["y"]
target_names = ["negative", "positive"]

# Define the data variable
data = df.drop("y", axis=1)
```
- Split the data into training and testing sets:
```python
from sklearn.model_selection import train_test_split

# Split data
X_train, X_test, y_train, y_test = train_test_split(data, target, random_state=42)
```
- Create KNN classifiers:
```python
from sklearn.neighbors import KNeighborsClassifier

untuned_model = KNeighborsClassifier()
grid_tuned_model = KNeighborsClassifier()
random_tuned_model = KNeighborsClassifier()
```
- Train the untuned model:
```python
from sklearn.metrics import classification_report

untuned_model.fit(X_train, y_train)
untuned_y_pred = untuned_model.predict(X_test)
print(classification_report(y_test, untuned_y_pred,
                            target_names=target_names))
```
```text
              precision    recall  f1-score   support

    negative       0.91      0.96      0.93      1006
    positive       0.38      0.22      0.28       125

    accuracy                           0.87      1131
   macro avg       0.64      0.59      0.60      1131
weighted avg       0.85      0.87      0.86      1131
```
- Create the grid search estimator:
```python
# Create the grid search estimator along with a parameter object containing the values to adjust.
# Try adjusting n_neighbors with values of 1 through 19. Adjust leaf_size by using 10, 50, 100, and 500.
# Include both uniform and distance options for weights.
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_neighbors': [1, 3, 5, 7, 9, 11, 13, 15, 17, 19],
    'weights': ['uniform', 'distance'],
    'leaf_size': [10, 50, 100, 500]
}
grid_clf = GridSearchCV(grid_tuned_model, param_grid, verbose=3)
```
- Fit the model using the **grid search estimator**
```python
# Fit the model by using the grid search estimator.
# This will take the KNN model and try each combination of parameters.
grid_clf.fit(X_train, y_train)
```
- Print the best parameters:
```python
# List the best parameters for this dataset
print(grid_clf.best_params_)
```
```text
{'leaf_size': 10, 'n_neighbors': 17, 'weights': 'distance'}
```
- Print the classification report for the best model:
```python
grid_y_pred = grid_clf.predict(X_test)
print(classification_report(y_test, grid_y_pred,
                            target_names=target_names))
```
```text
              precision    recall  f1-score   support

    negative       0.91      0.98      0.94      1006
    positive       0.48      0.18      0.26       125

    accuracy                           0.89      1131
   macro avg       0.69      0.58      0.60      1131
weighted avg       0.86      0.89      0.86      1131
```
- Create the parameter object for the **randomized search estimator**:
```python
param_grid = {
    'n_neighbors': np.arange(1,20,2),
    'weights': ['uniform', 'distance'],
    'leaf_size': np.arange(1, 500)
}
```
- Create the randomized search estimator and fit the model using it:
```python
# Create the randomized search estimator
from sklearn.model_selection import RandomizedSearchCV

random_clf = RandomizedSearchCV(random_tuned_model, param_grid, random_state=0, verbose=3)

# Fit the model by using the randomized search estimator.
random_clf.fit(X_train, y_train)
```
- List the best parameters for the randomized search estimator:
```python
# List the best parameters for this dataset
print(random_clf.best_params_)
```
```text
{'weights': 'distance', 'n_neighbors': 19, 'leaf_size': 243}
```
- Make predictions using the hypertuned model:
```python
# Make predictions with the hypertuned model
random_tuned_pred = random_clf.predict(X_test)
```
- Print the classification report:
```python
# Calculate the classification report
print(classification_report(y_test, random_tuned_pred,
                            target_names=target_names))
```
```text
              precision    recall  f1-score   support

    negative       0.91      0.98      0.94      1006
    positive       0.51      0.18      0.26       125

    accuracy                           0.89      1131
   macro avg       0.71      0.58      0.60      1131
weighted avg       0.86      0.89      0.87      1131
```
- Interpretations:
	- The best hyper parameter combination was {'weights': 'distance', 'n_neighbors': 19, 'leaf_size': 243}
	- They improved the overall accuracy of the model from 0.87 to 0.89.
	- If Recall of the positive class was the metric of interest however, the adjusted hyperparameters performed worse.
---
>Related Notes: [[Hyperparameter Tuning]]

>Tags: #AI #SL #UL 
