---
title: Preprocessing
created: 2023-08-04T20:40:00
last modified: Friday 4th August 2023 20:40
aliases: 
tags:
  - AI
  - SL
type: Classification
---
- Continuation of [Activity 01-Logistic_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/01-Logistic_Regression)
- **Preprocessing** the data includes preparing and then splitting it into training and testing sets before the machine can learn from it.
- Preview DataFrame and count the number of firms in each category:
```python
# Preview the DataFrame
df.head(3)

# Count how many firms are in each category
# 1 = Healthy and 0 = Unhealthy
df['Firm Category'].value_counts()
```
![[bankruptcy-dataframe-annotated.png]]
- Split the data into training and testing datasets using the `train_test_split` function:
```python
# Import Module
from sklearn.model_selection import train_test_split

# Split training and testing sets
# Create the features DataFrame, X
X = df.copy()
X = X.drop(columns='Firm Category')

# Create the target DataFrame, y
y = df['Firm Category']

# Use train_test_split to separate the data
X_train, X_test, y_train, y_test = train_test_split(X, y)
```
- Preview the `X_train` DataFrame:
```python
X_train
```
![[lr-demo-x-train-dataframe.png]]

---
>Related Notes: [[Training and Testing Data]], [[Understanding Categorical Data]]
>Tags: #AI #SL 
