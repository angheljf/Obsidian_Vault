---
title: Applying Random Sampling Techniques
created: 2023-09-09T20:17:00
last modified: Saturday 9th September 2023 20:17
aliases: 
tags:
  - AI
  - UL
  - SL
type: Imbalanced
---
- Refer to [Activity 02-Random_Resampling](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/05-ML-Optimization/demos/02-Random_Resampling) in order to see examples of random under and oversampling.
- Initial DataFrame:
```python
# Read the CSV file into a Pandas DataFrame
df = pd.read_csv('https://static.bc-edx.com/mbc/ai/m5/datasets/bank.csv')

# Review the DataFrame
df.head()
```
![[random-sampling-bank.PNG]]
- Split the data into X and y variables and encode any categorical variables using `get_dummies`:
```python
# Split the features and target data
y = df['y']
X = df.drop(columns='y')

# Encode the features dataset’s categorical variables using get_dummies
X = pd.get_dummies(X)

# Review the features DataFrame
X.head()
```
```text
5 rows x 51 columns
```
- Split data into training and testing datasets and review the distinct values from y:
```python
# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)

# Count of unique values from y
y_train.value_counts()
```
```text
no   3012
yes  378
```
- Use the standard scaler to scale the data:
```python:
# Instantiate a StandardScaler instance
scaler = StandardScaler()

# Fit the training data to the standard scaler
X_scaler = scaler.fit(X_train)

# Transform the training data using the scaler
X_train_scaled = X_scaler.transform(X_train)

# Transform the testing data using the scaler
X_test_scaled = X_scaler.transform(X_test)
```
- Train a model on the data before any sampling techniques are applied for later comparison:
```python
# Import the RandomForestClassifier from sklearn
from sklearn.ensemble import RandomForestClassifier

# Instantiate a RandomForestClassifier instance
model = RandomForestClassifier()

# Fit the training data to the model
model.fit(X_train_scaled, y_train)

# Predict labels for original scaled testing features
y_pred = model.predict(X_test_scaled)
```
## Random Undersampling
---
- Random undersampling removes randomly selected instances from the majority class until the size of that class is reduced, typically to the size of the minority class.
- In class imbalance problems, we can measure the success of a model by how well it found instances of the minority class.
- This can be measured with the precision and recall (sensitivity) metric.
- Set up and apply the `RandomUnderSampler` instance:
```python
# Import RandomUnderSampler from imblearn
from imblearn.under_sampling import RandomUnderSampler

# Instantiate the RandomUnderSampler instance
rus = RandomUnderSampler(random_state=1)

# Fit the training data to the random undersampling model
X_undersampled, y_undersampled = rus.fit_resample(X_train_scaled, y_train)

# Count distinct values
y_undersampled.value_counts()
```
```text
no   378
yes  378
```
- Fit a random forest classifier to the resampled dataset, generate predictions with the model, and compare the classification report for the model trained with undersampling to the model trained without it:
```python
# Instantiate a new RandomForestClassifier model
model_undersampled = RandomForestClassifier()

# Fit the undersampled data to the new model
model_undersampled.fit(X_undersampled, y_undersampled)

# Predict labels for oversampled testing features
y_pred_undersampled = model_undersampled.predict(X_test_scaled)

# Print classification reports
print(f"Classification Report - Original Data")
print(classification_report(y_test, y_pred))
print("---------")
print(f"Classification Report - Undersampled Data")
print(classification_report(y_test, y_pred_undersampled))
```
![[classification-report-random-sampling-1.png]]
- The undersampled data identified many more points as being part of the minority class. 
- The recall has gone up considerably for the minority class. By allowing more false positives, we went from capturing 22% of the known minority class labels to 81%.
## Random Oversampling
---
- In random oversampling, the algorithm randomly selects instances of the minority class and adds them to the training set until the majority and minority classes are balanced.
- Set up and apply the `RandomOverSampler` instance:
```python
# Import RandomOverSampler from imblearn
from imblearn.over_sampling import RandomOverSampler

# Instantiate a RandomOversampler instance
ros = RandomOverSampler(random_state=1)

# Fit the model to the training data
X_oversampled, y_oversampled = ros.fit_resample(X_train_scaled, y_train)

# Count distinct values
y_oversampled.value_counts()
```
```text
no   3012
yes  3012
```
- Create two RandomForestClassifier models, one using the original data and the other using the oversampled data. Then, generate the predictions and compare the results:
```python
# Instantiate a new RandomForestClassifier model
model_oversampled = RandomForestClassifier()

# Fit the oversampled data to the new model
model_oversampled.fit(X_oversampled, y_oversampled)

# Predict labels for oversampled testing features
y_pred_oversampled = model_oversampled.predict(X_test_scaled)

# Print classification reports
print(f"Classification Report - Original Data")
print(classification_report(y_test, y_pred))
print("---------")
print(f"Classification Report - Undersampled Data")
print(classification_report(y_test, y_pred_undersampled))
print("---------")
print(f"Classification Report - Oversampled Data")
print(classification_report(y_test, y_pred_oversampled))
```
![[classification-report-random-sampling-2.png]]
- Using oversampling to correct the imbalance, we found only 26% of the minority class instances and we were correct 36% of the time when predicting the minority class.
- Compare this to the predictions using undersampling: We found 80% of the minority class instances and were correct 51% of the time.
- Regardless of the different outcomes, both undersampling and oversampling improved the results over the original data.
---
>Related Notes: [[Accuracy]], [[Other Metrics]], [[Confusion Matrix]], [[Oversampling and Undersampling]]

>Tags: #AI #UL #SL 
