---
title: Synthetic Resampling
created: 2023-09-10T21:57:00
last modified: Sunday 10th September 2023 21:57
aliases: 
tags:
  - AI
  - UL
  - SL
type: Imbalanced
---
- We will explore three types of synthetic resampling methods, namely **cluster centroids**, **SMOTE**, and **SMOTEENN**.
## Cluster Centroids
---
- In machine learning, clustering algorithms are used to group similar data points together. The cluster centroid is the center of the cluster, and it is the average of all the data points in that cluster.
- Synthetic sampling creates new data points from existing observations. There are several ways to do this, but the most common approach is to use **KNN** to generate the new points.
- Refer to [Activity 03-Synthetic_Resampling](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/05-ML-Optimization/demos/03-Synthetic_Resampling) in order to see an examples of synthetic resampling.
- Initial DataFrame:
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
- **Cluster centroids** is a synthetic method of resampling the data to achieve a balance between what started as the majority and minority classes.
- We identify the center of a cluster of the majority class, and then generate points in that cluster using KNN.
- These generated points are then undersampled until there is an equivalent number of instances compared to the minority class.
- Use the standard scaler to scale the data:
```python
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
- Set up and apply the `ClusterCentroids` instance:
```python
# Import ClusterCentroids from imblearn
from imblearn.under_sampling import ClusterCentroids
from sklearn.cluster import KMeans

# Instantiate a ClusterCentroids instance
cc_sampler = ClusterCentroids(estimator=KMeans(n_init='auto', random_state=0), random_state=1)

# Fit the training data to the cluster centroids model
X_resampled, y_resampled = cc_sampler.fit_resample(X_train_scaled, y_train)

# Count distinct values for the resampled target data
y_resampled.value_counts()
```
```text
no   378
yes  378
```
- Instantiate the `RandomForestClassifier` model, fit the models, and analyze the classification reports on the predicted values:
```python
# Instantiate a new RandomForestClassifier model
cc_model = RandomForestClassifier()

# Fit the resampled data to the new model
cc_model.fit(X_resampled, y_resampled)

# Predict labels for resampled testing features
cc_y_pred = cc_model.predict(X_test_scaled)

# Print classification reports
print(f"Classification Report - Original Data")
print(classification_report(y_test, y_pred))
print("---------")
print(f"Classification Report - Resampled Data - CentroidClusters")
print(classification_report(y_test, cc_y_pred))
```
![[classification-report-cluster-centroids.png]]
- Although the accuracy with the resampled data was not improved, the resampled model using cluster centroids improved recall for the “yes” class from 0.19 to 0.99!
## SMOTE
---
- The synthetic minority oversampling technique (**SMOTE**) is another synthetic resampling technique. It also works by using KNN to generate synthetic data. Only this time, the synthetic points are from the minority class.
- The set of synthetic points from the minority class is oversampled until it is the same size as the majority class.
- Set up and apply the `SMOTE` instance:
```python
# Import SMOTE from imblearn
from imblearn.over_sampling import SMOTE

# Instantiate the SMOTE instance 
# Set the sampling_strategy parameter equal to auto
smote_sampler = SMOTE(random_state=1, sampling_strategy='auto')

# Fit the SMOTE model to the training data
X_resampled, y_resampled = smote_sampler.fit_resample(X_train, y_train)

# Count resampled values
y_resampled.value_counts()
```
```text
no   3012
yes  3012
```
- Note that we add the parameter `sampling_strategy='auto'` when instantiating the SMOTE instance. This allows the algorithm to automatically resample the training dataset.
- Instantiate the `RandomForestClassifier` model, fit the models, and analyze the classification reports on the predicted values:
```python
# Instantiate a new RandomForestClassifier model 
smote_model = RandomForestClassifier()

# Fit the resampled data to the new model
smote_model.fit(X_resampled, y_resampled)


# Predict labels for resampled testing features
smote_y_pred = smote_model.predict(X_test_scaled)

# Print classification reports
print(f"Classification Report - Original Data")
print(classification_report(y_test, y_pred))
print("---------")
print(f"Classification Report - Resampled Data - SMOTE")
print(classification_report(y_test, smote_y_pred))
```
![[classification-report-smote.png]]
- SMOTE improved the results of the minority class, but they were not the best that we have observed for this dataset.
## SMOTEENN
---
- **SMOTEENN** is a combination of SMOTE oversampling and undersampling by removing misclassified points using edited nearest neighbors (ENN).
- **ENN** is a rule that uses the three nearest neighbors to find a misclassified point and then removes it.
- Set up and apply the `SMOTEENN` instance:
```python
# Import SMOTEENN from imblearn
from imblearn.combine import SMOTEENN

# Instantiate the SMOTEENN instance
smote_enn = SMOTEENN(random_state=1)

# Fit the model to the training data
X_resampled, y_resampled = smote_enn.fit_resample(X_train_scaled, y_train)

# Count distinct values for the resampled target data
y_resampled.value_counts()
```
```text
1   2927
0   2394
```
- Notice that the value counts are not the same because we applied ENN to remove misclassified points.
- Instantiate the `RandomForestClassifier` model, fit the models, and analyze the classification reports on the predicted values:
```python
# Instantiate a new RandomForestClassifier model
smoteenn_model = RandomForestClassifier()

# Fit the resampled data to the new model
smoteenn_model.fit(X_resampled, y_resampled)

# Predict labels for resampled testing features
smoteenn_y_pred = smoteenn_model.predict(X_test_scaled)

# Print classification reports
print(f"Classification Report - Original Data")
print(classification_report(y_test, y_pred))
print("---------")
print(f"Classification Report - Resampled Data - SMOTEENN")
print(classification_report(y_test, smoteenn_y_pred))
```
![[classification-report-smoteen.png]]
- In conclusion, SMOTE and SMOTEENN both improved the recall of the “yes” class, while cluster centroids _dramatically_ improved it to almost 100%.
---
>Related Notes: [[Oversampling and Undersampling]], [[Applying Random Sampling Techniques]]

>Tags: #AI #UL #SL 
