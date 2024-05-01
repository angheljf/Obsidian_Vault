---
title: Improving Bank Marketing Campaigns with Synthetic Sampling
created: 2023-09-16T20:39:00
last modified: Saturday 16th September 2023 20:39
aliases: 
tags:
  - AI
  - UL
  - SL
type: Imbalanced
---
- Refer to [Activity 02-Balanced_Random_Forest](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/05-ML-Optimization/activities/02-Balanced_Random_Forest) in order to see an example of how to fit various balanced and imbalanced models to small-business loan data and compare the results.
- The dataset contains the following columns:
	- **Year:** The fiscal year of the loan application.
	- **Month:** The month of the fiscal year.
	- **Amount:** The issued loan amount.
	- **Term:** The term of the loan, in months.
	- **Zip:** The borrower’s ZIP code.
	- **CreateJob:** The number of jobs that were created by using the loan.
	- **NoEmp:** The number of business employees.
	- **RealEstate:** Whether the loan is backed by real estate.
	- **RevLineCr:** Whether the loan is a revolving line of credit.
	- **UrbanRural:** The location type of the borrower.
	- **Default:** Whether the borrower defaulted on the loan (1) or not (0).
- Initial DataFrame:
```python
# Read the sba_loans.csv file from the Resources folder into a Pandas DataFrame
loans_df = pd.read_csv('https://static.bc-edx.com/mbc/ai/m5/datasets/sba-loans.csv')

# Review the DataFrame
loans_df.head()
```
![[sba-loans-dataframe.PNG]]
- Separate the independent variables (X) from the target column (y):
```python
# Split the data into X (features) and y (labels)
# The y variable should focus on the Default column
y = loans_df['Default']

# The X variable should include all features except the Default column
X = loans_df.drop(columns=['Default'])
```
- Split the data into training and testing sets and scale the data:
```python
# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)

# Scale the data
scaler = StandardScaler()
X_scaler = scaler.fit(X_train)
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
- Check the value counts in the target column:
```python
# Count the distinct values in the original labels data
y_train.value_counts()
```
```text
0   1063
1   96
Name: Default, dtype: int64
```
- Create and train a random forest model and a balanced random forest model for comparison:
```python
from sklearn.ensemble import RandomForestClassifier

# Create a random forest classifier
rf_model = RandomForestClassifier(n_estimators=100, random_state=1)

# Fitting the model
rf_model = rf_model.fit(X_train_scaled, y_train)

# Making predictions using the testing data
rf_predictions = rf_model.predict(X_test_scaled)

# Import BalancedRandomForestClassifier from imblearn
from imblearn.ensemble import BalancedRandomForestClassifier

# Instantiate a BalancedRandomForestClassifier instance
brf = BalancedRandomForestClassifier()

# Fit the model to the training data
brf.fit(X_train_scaled, y_train)

# Predict labels for testing features
brf_predictions = brf.predict(X_test_scaled)
```
- Use SMOTE on the training data and use it to train another random forest model:
```python
# Import SMOTE from imblearn
from imblearn.over_sampling import SMOTE

# Instantiate the SMOTE model instance
smote_sampler = SMOTE(random_state=1, sampling_strategy='auto')

# Fit the SMOTE model to the training data
X_resampled, y_resampled = smote_sampler.fit_resample(X_train, y_train)

# Fit the RandomForestClassifier on the resampled data
model_resampled_rf = RandomForestClassifier()
model_resampled_rf.fit(X_resampled, y_resampled)

# Generate predictions based on the resampled data model
rf_resampled_predictions = model_resampled_rf.predict(X_test)
```
- Print the confusion matrices for each model:
```python
# Print the confusion matrix for RandomForest on the original data
confusion_matrix(y_test, rf_predictions)
```
```text
array([[338,  10],
       [ 13,  26]])
```
```python
# Print the confusion matrix for balanced random forest data
confusion_matrix(y_test, brf_predictions)
```
```text
array([[315,  33],
       [  5,  34]])
```
```python
# Print the confusion matrix for RandomForest on the resampled data
confusion_matrix(y_test, rf_resampled_predictions)
```
```text
array([[329,  19],
       [  7,  32]])
```
- The first random forest model performed well on the majority class, but struggled on the minority class.
- The balanced random forest and the random forest trained with SMOTE both performed better on the minority class, but the random forest model trained with SMOTE performed better on the majority class than the balanced random forest model.
- Print accuracy metrics for all the models:
```python
# Print the accuracy score for the original data
baso = balanced_accuracy_score(y_test, rf_predictions)
print(baso)
```
```text
0.8189655172413792
```
```python
# Print the accuracy score for the resampled data
basr = balanced_accuracy_score(y_test, brf_predictions)
print(basr)
```
```text
0.8884836427939876
```
```python
# Print the accuracy score for the resampled data with SMOTE
basrs = balanced_accuracy_score(y_test, rf_resampled_predictions)
print(basrs)
```
```text
0.8829575596816976
```
```python
# Print the classification report for the original data
print(classification_report_imbalanced(y_test, rf_predictions))
```
```text
                   pre       rec       spe        f1       geo       iba       sup

          0       0.96      0.97      0.67      0.97      0.80      0.67       348
          1       0.72      0.67      0.97      0.69      0.80      0.63        39

avg / total       0.94      0.94      0.70      0.94      0.80      0.66       387
```
```python
# Print the classification report for the resampled data
print(classification_report_imbalanced(y_test, brf_predictions))
```
```text
                   pre       rec       spe        f1       geo       iba       sup

          0       0.98      0.91      0.87      0.94      0.89      0.79       348
          1       0.51      0.87      0.91      0.64      0.89      0.79        39

avg / total       0.94      0.90      0.88      0.91      0.89      0.79       387
```
```python
# Print the classification report for the resampled data
print(classification_report_imbalanced(y_test, rf_resampled_predictions))
```
```text
                   pre       rec       spe        f1       geo       iba       sup

          0       0.98      0.95      0.82      0.96      0.88      0.79       348
          1       0.63      0.82      0.95      0.71      0.88      0.77        39

avg / total       0.94      0.93      0.83      0.94      0.88      0.78       387
```
- Overall, both resampled models in this example perform better at identifying more of the eventual loan defaults. We can see this by looking at the increase recall for the “default” or “`1`” category in the two imbalanced models, when compared to the original random forest model.
- A higher recall for this category means that of all the loans that actually were in default, how many did this model correctly catch? A higher recall for a model means it’s going to do a better job at making sure any potential defaults are not missed.
- However, the higher recall for these two imbalanced models comes at a cost: a greater tendency to flag a loan as a potential default, even when it does not. This is evidenced by a lower precision for these two models. If precision looks at, of all those loans the model predicted as default, how many of them actually were defaults, then a lower precision value means that the model is making a lot of false positives; predicting a default when there isn’t actually one.
- This illustrates the main tradeoff when using imbalanced versions of machine learning models. If you really care about identifying those faulty loans (or whatever you’re trying to predict), and the cost of failing to identify a faulty loan is very high, then maybe an imbalanced model with lower precision is worth it. After all, we can always find another business to lend to, but if that business defaults, it’s very costly to us as a lender.
- If on the other hand, you have a situation in which the costs of misclassification are the same either way—if failing to correctly identify a `1` has the same practical cost as failing to correctly identify a `0`—then we may be better off with the overall higher accuracy of a standard machine learning model.
---
>Related Notes: [[Synthetic Resampling]]

>Tags: #AI #UL #SL 
