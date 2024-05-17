---
title: Predicting Wine Quality with Deep Learning
created: 2024-05-16T19:15:00
last modified: 2024-05-16 19:15
aliases: 
tags:
  - AI
  - NN
type: Deep Learning
---
- Refer to [Activity 02-Predict_Wine_Quality](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/demos/02-Predict_Wine_Quality) in order to see an example of a deep learning model that will predict the quality scores of different wines.
- Create initial DataFrame:
```python
# Set the CSV file path
file_path = "https://static.bc-edx.com/mbc/ai/m5/datasets/wine_quality.csv"

# Read the data into a DataFrame
df = pd.read_csv(file_path)

# Display sample data
df.head()
```
![[read-wine-data.png]]
- The data contains 11 variables representing different wine characteristics. Together, these characteristics allow us to assess the overall “quality” of a wine on a scale from 1 to 10.
- Next, we preprocess the data:
```python
# Create the features (X) and target (y) sets
X = df.drop(columns=["quality"]).values
y = df["quality"].values
```
- Create the training and testing datasets, and scale the data:
```python
# Create the training and testing datasets
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)

# Create the scaler instance
X_scaler = StandardScaler()

# Fit the scaler
X_scaler.fit(X_train)

# Scale the features data
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
- Next, we will create our model
---
>Related Notes: [[What is Deep Learning]]

>Tags: #AI #NN 
