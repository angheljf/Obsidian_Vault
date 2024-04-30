---
title: Realities and Limitations
created: 2024-04-30T15:17:00
last modified: 2024-04-30 15:17
aliases: 
tags:
  - AI
  - UL
type: Tuning
---
- Each model has a limit to the complexity of relationships it is capable of understanding.
- Once data complexity surpasses the limitations of a model, optimizing the model will be tedious at best and fruitless at worst.
- To see this in practice, follow the listed steps along with us by implementing the following code:
```python
# Load libraries
import pandas as pd
from sklearn.svm import SVC
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

# Import data and plot
df = pd.read_csv('https://static.bc-edx.com/mbc/ai/m5/datasets/spirals.csv')
df.plot.scatter("x1", "x2", color=df["y"].map({1.0: "purple", 0.0:"orange"})).get_figure().savefig("spirals_data_scatter.png")
```
![[spirals-scatter.png]]
- Next:
```python
# Split the data into training and testing sets
X = df[['x1', 'x2']]
y = df['y']
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state = 13)

# Train and score a model
clf = SVC()
clf.fit(X_train, y_train)
y_pred = clf.predict(X_test)
print(classification_report(y_pred, y_test))
```
![[classification-report-limits.png]]
- Plot predictions made by the model:
```python
# Plot the predictions made by the model
X_test.plot.scatter("x1", 
                    "x2",
                    color = pd.Series(y_pred)\
                    .map({1.0: "purple", 0.0:"orange"})).get_figure().savefig("spirals_predictions_scatter.png")
```
![[spirals-predictions-scatter.png]]
- The SVC model was not able to fully learn the spiral shape of the data (A RandomForest model would be able to classify the points in this spiral dataset).
- The issue of overcoming increasingly complex data is where huge strides have been made in Machine Learning in recent years.
---
>Related Notes: [[How Much is Enough]], [[Hyperparameter Tuning]]
>Tags: 
