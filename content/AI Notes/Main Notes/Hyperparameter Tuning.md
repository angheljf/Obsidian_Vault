---
title: Hyperparameter Tuning
created: 2023-10-27T20:10:00
last modified: Friday 27th October 2023 20:10
aliases: 
tags:
  - AI
  - UL
  - SL
type: Tuning
---
- Selecting a machine learning algorithm is like selecting a type of car to perform a specific task.
- Machine learning models all have additional custom options called “hyperparameters” that can be tweaked to improve the viability or performance of your model.
- Simply put, **hyperparameters** allow you to customize how algorithms behave to a specific dataset.
- Hyperparameters are different to parameters in that they are specified by you and not by an internally learning algorithm.
- Picking the best hyperparameters for a model can be difficult, therefore we use random or grid search strategies for optimal values:
	- **Grid search** strategies are a brute-force search paradigm approach where you can specify a list of values for different hyperparameters, which the computer uses to evaluate the model performance for each combination of hyperparameters to obtain the optimal set.
	- **Random search** strategies are similar to a grid search in many ways. You can still define an estimator, which hyperparameters to tune, and the range of values for each hyperparameter. Also, you can set a cross-validation scheme and scoring function. But, when it comes to undertaking the search, rather than trying every single combination, you randomly sample N combinations and try them out.
## Grid Search
---
- Here is some code that shows an example of grid search:
```python
# Import modules
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings("ignore")

# Import data
df = pd.read_csv('https://static.bc-edx.com/mbc/ai/m5/datasets/numeric_bank.csv')
df.head()
# Create X and y data
target = df["y"]
target_names = ["negative", "positive"]
data = df.drop("y", axis=1)
data.head()

# Split data into training and testing
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=42)

# Create the SVC model
from sklearn.svm import SVC
untuned_model = SVC(kernel='linear')
untuned_model

## Train a model without tuning
from sklearn.metrics import classification_report
untuned_model.fit(X_train, y_train)
untuned_y_pred = untuned_model.predict(X_test)
print(classification_report(y_test, untuned_y_pred,
                            target_names=target_names))
```
- Here is the output of the classification report:
![[classification-report-hyperparameters-untuned.png]]
- For reference, [here](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html#sklearn.svm.SVC) is the documentation about SVC(**Support Vector Classification**) 
- Scikit-learn refers to these as parameters, but note that they’re not internal parameters.
- A machine learning model sets its internal parameters based on data.
- Note the `C` and `gamma` hyperparameters from the documentation. Let’s tweak these parameters and see what effect they will have on our model:
```python
param_grid = {'C': [1, 5, 10, 50],
              'gamma': [0.0001, 0.0005, 0.001, 0.005]}

# Create grid search estimator
from sklearn.model_selection import GridSearchCV
grid_clf = GridSearchCV(model, param_grid, verbose=3)
```
- Above, we are using Scikit-learn’s built-in function for trying all the possible combinations of these parameters. This function, `GridSearchCV()`, also fits the model-fit-predict pattern, so we consider it to be a _hypermodel_. We initialize it with a base model and a dictionary of parameters.
- Fit the `GridSearchCV()` model to the training data:
```python
# Fit the model by using the grid search classifier.
# This will take the SVC model and try each combination of parameters.
grid_clf.fit(X_train, y_train)
```
- From the first line of the output: `Fitting 5 folds for each of the 16 candidates, totalling 80 fits`, you can see that each combination of parameters was run five times. Afterwards, the scores were averaged.
- Output the pair of parameters that `GridSearchCV()` selected as the best considering these average scores:
```python
# List the best parameters for this dataset
print(grid_clf.best_params_)

# List the best score
print(grid_clf.best_score_)
```
```python
{'C': 5, 'gamma': 0.0001}
0.9333333333333333
```
- But you only need to do this if you wish to see the winning parameters and score for yourself. Instead, we can simply use the existing `predict()` and `score()` functions to access the trained base `SVC` model:
```python
# Make predictions with the hypertuned model
predictions = grid_clf.predict(X_test)
predictions

# Score the hypertuned model on the test dataset
grid_clf.score(X_test, y_test)
```
```python
array([0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 0, 0, 1,
     1, 0, 0])
0.88
```
## Random Search
---
- Instead of trying to brute-force test every combination, we can try a random subsample and then take the best of the results. A function exists in Scikit-learn for doing exactly this: `RandomizedSearchCV()`.
- Let us create another parameter grid for `C` and `gamma`:
```python
big_param_grid = {
    'C' : np.arange(0, 100, 1),
    'gamma': np.arange(0, 0.01, .0001),
}
big_param_grid
```
- Let’s take a look at what this parameter grid looks like:
```python
{'C': array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
        17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
        34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50,
        51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67,
        68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84,
        85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]),
 'gamma': array([0.    , 0.0001, 0.0002, 0.0003, 0.0004, 0.0005, 0.0006, 0.0007,
        0.0008, 0.0009, 0.001 , 0.0011, 0.0012, 0.0013, 0.0014, 0.0015,
        0.0016, 0.0017, 0.0018, 0.0019, 0.002 , 0.0021, 0.0022, 0.0023,
        0.0024, 0.0025, 0.0026, 0.0027, 0.0028, 0.0029, 0.003 , 0.0031,
        0.0032, 0.0033, 0.0034, 0.0035, 0.0036, 0.0037, 0.0038, 0.0039,
        0.004 , 0.0041, 0.0042, 0.0043, 0.0044, 0.0045, 0.0046, 0.0047,
        0.0048, 0.0049, 0.005 , 0.0051, 0.0052, 0.0053, 0.0054, 0.0055,
        0.0056, 0.0057, 0.0058, 0.0059, 0.006 , 0.0061, 0.0062, 0.0063,
        0.0064, 0.0065, 0.0066, 0.0067, 0.0068, 0.0069, 0.007 , 0.0071,
        0.0072, 0.0073, 0.0074, 0.0075, 0.0076, 0.0077, 0.0078, 0.0079,
        0.008 , 0.0081, 0.0082, 0.0083, 0.0084, 0.0085, 0.0086, 0.0087,
        0.0088, 0.0089, 0.009 , 0.0091, 0.0092, 0.0093, 0.0094, 0.0095,
        0.0096, 0.0097, 0.0098, 0.0099])}
```
- That’s a significantly chunkier range of parameters to check. If we were to use the previous grid search method on this, it would have to run the model 50 000 times. To save time and processing power, we can instead run a random sample of parameter combinations:
```python
# Create the randomized search estimator along with a parameter object containing the values to adjust
from sklearn.model_selection import RandomizedSearchCV
random_clf = RandomizedSearchCV(model, big_param_grid, n_iter=100, random_state=1, verbose=3)
random_clf

# Fit the model by using the randomized search estimator. 
# This will take the logistic regression model and try a random sample of combinations of parameters.
random_clf.fit(X_train, y_train)
```
- Then, just like before, we can check the best parameters, list the best score, and make predictions with the new hypertuned model:
```python
# List the best parameters for this dataset
print(random_clf.best_params_)

# List the best score
print(random_clf.best_score_)

# Make predictions with the hypertuned model
predictions = random_clf.predict(X_test)
```
```python
{'gamma': 0.0005, 'C': 9}
0.9333333333333333
```
-  For reference, [here](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html#sklearn.model_selection.RandomizedSearchCV) is the documentation about `RandomizedSearchCV`.
---
>Related Notes: [[Linear Models]], [[Predict Occupancy with SVM]]

>Tags: #AI #SL #UL 
