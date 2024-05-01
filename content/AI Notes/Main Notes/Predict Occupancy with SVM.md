---
title: Predict Occupancy with SVM
created: 2023-08-12T20:47:00
last modified: Saturday 12th August 2023 18:47
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- Refer to [Activity 02-SVM](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/02-SVM) in order to see an example of application of an SVM classifier to predict if an office space is occupied based on different factors.
- Initial DataFrame:
```python
# Import data
file_path = "https://static.bc-edx.com/mbc/ai/m4/datasets/occupancy.csv"
df = pd.read_csv(file_path)
df.head()
```
![[occupancy-dataframe.png]]
- Split our data into features and target set:
```python
# Get the target variable (the "Occupancy" column)
y = df["Occupancy"]

# Get the features (everything except the "Occupancy" column)
X = df.copy()
X = X.drop(columns="Occupancy")
```
- Split into training and testing set:
```python
# Split data into training and testing
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=42)
```
- Create the SVM model:
```python
# Create the support vector machine classifier model with a 'linear' kernel
model = SVC(kernel='linear')
```
- The `kernel` argument is used to express the degree of dimensionality needed to separate the data into classes, i.e., the `kernel` parameter is used to identify the orientation of the hyperplane.
- Values available for the `kernel` argument are:
	- **linear:** Creates a linear 2D hyperplane.
	- **rbf:** Creates a parabolic non-linear hyperplane.
	* **poly:** Creates a polynomial non-linear hyperplane.
- Fit the model to our data:
```python
# Fit the model to the training data
model.fit(X_train, y_train)
```
- Validate our model using the `model.score()` function:
```python
# Validate the model by checking the model accuracy with model.score
print('Train Accuracy: %.3f' % model.score(X_train, y_train))
print('Test Accuracy: %.3f' % model.score(X_test, y_test))
```
```text
Train Accuracy: 0.987
Test Accuracy: 0.986
```
- Make predictions using the testing data:
```python
# Make and save testing predictions with the saved SVM model using the testing data
testing_predections = model.predict(X_test)
```
- Evaluate the model with the `accuracy_score()` function:
```python
# Display the accuracy score for the testing dataset
accuracy_score(y_test, testing_predections)
```
```text
0.9862475442043221
```
---
>Related Notes: [[Linear Models]]

>Tags: #AI #SL 
