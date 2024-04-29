---
title: Confusion Matrix
created: 2023-08-26T18:38:00
last modified: Saturday 26th August 2023 18:38
aliases: 
tags:
  - AI
  - UL
  - SL
type: Optimization
---
- There are two ways in which a model with discrete outcomes’ results can be true, and two ways in which it can be false.
- You have **true and false positives, and true and false negatives**.
- These four types of results can be organized into a **confusion matrix**, a table that groups results according to whether they are predicted as true or false, and whether they are actually true or false. An example of a confusion matrix is illustrated in the following table:
![[confusion-matrix-layout.png]]
- Generating one of these matrices for your particular model is simple as Scikit-learn already includes a `confusion_matrix` function in the `metrics` package.
```python
confusion_matrix(y_test, predictions)
```
```text
array([[11, 1],
	   [0, 13]])
```
- For a prettier confusion matrix, refer to this [link](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.ConfusionMatrixDisplay.html)
![[ConfusionMatrixDisplay.png]]
-  Refer to [Activity 01-Confusion_Matrix](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/05-ML-Optimization/activities/01_Confusion_Matrix) in order to see an example of how to build a confusion matrix.
- Initial DataFrame:
```python
df = pd.read_csv("https://static.bc-edx.com/mbc/ai/m5/datasets/blobs_data.csv")
df.head()
```
![[confusion-matrix-dataframe.PNG]]
- Scatter plot to visualize the data:
```python
df.plot.scatter(x="X1", y="X2", color=df['y'].map({1: "orange", 0: "purple"}),
				alpha=0.8)
```
![[confusion-matrix-scatterplot.PNG]]
- From the scatter plot, we can observe the following:
	- This dataset is imbalanced; there are far more instances of the negative class (purple) than the positive class (orange).
	- There is significant overlap between the two classes, and therefore perfect accuracy is an unreasonable expectation.
	- It will be more difficult for the model to score well on the positive (orange) data points, and accuracy alone will not tell us enough about the model's performance.
- Separate data into training and testing sets:
```python
X = df[["X1", "X2"]]
    y = df['y']
    X_train, X_test, y_train, y_test = train_test_split(X,
                                                        y,
                                                        random_state=1,
                                                        stratify=y)
```
- Create and fit the model:
```python
# Create a Logistic Regression Model
classifier = LogisticRegression(solver='lbfgs', random_state=1)

# Fit (train) or model using the training data
classifier.fit(X_train, y_train)

# Make predictions on the test data
predictions = classifier.predict(X_test)

# Calculate the accuracy of the model
classifier.score(X_test, y_test)
```
```text
0.9236363636363636
```
- A couple of things to keep in mind when looking at the accuracy score for this model:
	- A model that predicts that every data point is negative (purple) would yield an excellent accuracy score as well.
	- The accuracy score doesn't tell us whether the positive class (orange) is predicted well.
- Create a confusion matrix:
```python
# Create a confusion matrix
confusion_matrix(y_test, predictions, labels = [1,0])
```
```text
array([[ 14,  11],
       [ 10, 240]])
```
- Reading a confusion matrix:
	- The top left is "True Negative" and indicates the positive data points that were correctly predicted to be positive.
	- The top right is "False Positive" and indicates the negative data points that were incorrectly predicted to be positive.
	- The bottom left is "False Negative" and indicates the positive data points that were incorrectly predicted to be negative.
	- The bottom right is "True Positive" and indicates the negative data points that were correctly predicted to be negative.
---
>Related Notes: [[Overfitting and Underfitting]]
>Tags: #AI #UL #SL 
