---
title: Random Forest Demonstration
created: 2023-08-18T21:22:00
last modified: Friday 18th August 2023 21:22
aliases: 
tags:
  - AI
  - SL
type: Ensemble Learning
---
- Refer to [Activity 04-Random_Forest](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/04-Random_Forest) in order to see an example of how to apply a Random Forest model.
- Initial DataFrame:
```python
# Load data
file_path = "https://static.bc-edx.com/mbc/ai/m4/datasets/app-data.csv"
df_apps = pd.read_csv(file_path)
df_apps.head()
```
![[app-dataframe.png]]
- Define the features set:
```python
# Define the features set
X = df_apps.copy()
X.drop("Result", axis=1, inplace=True)
X.head()
```
- Define the target set:
```python
# Define the target set
# The ravel method perfomrs the same procedure on the target set as the values attribute
y = df_apps["Result"].ravel()
y[:5]
```
- Split into training and testing set:
```python
# Split into Train and Test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=78)
```
- Create the Random Forest model:
```python
# Create the random forest classifier instance
# n_estimators sets the numer of trees (best practice => 64-128)
rf_model = RandomForestClassifier(n_estimators=128, random_state=78)
```
- Fit the model to our training datasets:
```python
# Fit the model
rf_model = rf_model.fit(X_train, y_train)
```
- Make predictions using the testing data:
```python
# Make predictions using the testing data
predictions = rf_model.predict(X_test)
```
- Evaluate the accuracy of the model:
```python
# Calculate the accuracy score
acc_score = accuracy_score(y_test, predictions)

# Display results
print(f"Accuracy Score : {acc_score}")
```
```text
Accuracy Score : 0.9672712396018001
```
- Analyze which features had the most impact on the result:
```python
# Get the feature importance array
importances = rf_model.feature_importances_
# List the top 10 most important features
importances_sorted = sorted(zip(rf_model.feature_importances_, X.columns), reverse=True)
importances_sorted[:10]
```
```text
[(0.2526418903981927, 'android.permission.READ_PHONE_STATE'),
 (0.11323230656064623, 'com.google.android.c2dm.permission.RECEIVE'),
 (0.08156488911416043, 'android.permission.RECEIVE_BOOT_COMPLETED'),
 (0.06579127309698081, 'android.permission.ACCESS_COARSE_LOCATION'),
 (0.05883799614741168, 'com.android.launcher.permission.INSTALL_SHORTCUT'),
 (0.043793946991240375, 'android.permission.ACCESS_FINE_LOCATION'),
 (0.03813886967165418, 'android.permission.GET_TASKS'),
 (0.02303354853086105, 'android.permission.SYSTEM_ALERT_WINDOW'),
 (0.022989587959897147, 'android.permission.READ_EXTERNAL_STORAGE'),
 (0.022280304346836505, 'com.android.vending.BILLING')]
```
- One reason we might want to check the feature importance results is because the weight of some features can be significantly higher than other features and overpower the results.
- Sometimes, machine learning programmers choose to remove these features from the dataset before training the model, so that they cannot skew the results. Identifying and removing features with a low importance can also improve the accuracy of the model.
---
>Related Notes: [[Random Forest]], [[Decision Trees]]
>Tags: #AI #SL 
