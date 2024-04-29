---
title: Balanced Models
created: 2023-09-16T20:23:00
last modified: Saturday 16th September 2023 20:23
aliases: 
tags:
  - AI
  - UL
  - SL
type: Imbalanced
---
- `imblearn` contains another class that implements random undersampling on top of a random forest classifier: `BalancedRandomForestClassifier`.
- This classifier is useful when you want to undersample your data, but is otherwise no different from `RandomForestClassifier`.
- Initial DataFrame:
![[random-sampling-bank.PNG]]
- Split and scale data:
```python
# Split target column from dataset
y = df['y']
X = df.drop(columns='y')

# Encode the categorical variables using get_dummies
X = pd.get_dummies(X)

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)

# Count distinct values
y_train.value_counts()

# Scale the data
scaler = StandardScaler()
X_scaler = scaler.fit(X_train)
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
- Create an instance of the classifier, fit it to the data, and then use it to predict labels from the scaled test dataset:
```python
# Import BalancedRandomForestClassifier from imblearn
from imblearn.ensemble import BalancedRandomForestClassifier

# Instantiate a Balanced Random Forest Classifier instance
brf = BalancedRandomForestClassifier()

# Fit the model to the training data
brf.fit(X_train_scaled, y_train)

# Predict labels for testing features
y_pred = brf.predict(X_test_scaled)

# Print classification report
print(classification_report(y_test, y_pred))
```
![[balanced-classification-report.png]]
- Fundamentally, this is the same as before, but in this case the **balanced** random forest classifier incorporates random undersampling directly into the algorithm so there is no need to do that as a separate step.
- When training models on imbalanced data without applying the proper preprocessing and without using an appropriate metric can cause results that seem great on first glance but actually perform poorly in practice.
---
>Related Notes: [[Random Forest]], [[Oversampling and Undersampling]], [[Applying Random Sampling Techniques]]
>Tags: #AI #UL #SL 
