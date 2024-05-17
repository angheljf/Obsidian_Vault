---
title: Activity - Predict Credit Card Defaults
created: 2024-05-11T20:43:00
last modified: 2024-05-11 20:43
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- Refer to [Activity 01-Credit_Card_Defaults](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/activities/01-Credit_Card_Defaults)in order to see an example of a neural network model that predicts whether a credit card customer will default on their debt.
- Import packages for preprocessing the data:
```python
# Import required libraries
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression
```
- Load in the CSV file as a DataFrame:
```python
# Read the cc_default.csv file into a Pandas DataFrame
file_path = "https://static.bc-edx.com/mbc/ai/m6/datasets/cc_default.csv"
cc_df = pd.read_csv(file_path)

# Review the DataFrame
cc_df.head()
```
![[cc_default_df.png]]
- Create the X and y variables to hold the independent variables and the target column, respectively:
```python
# Define features set X by selecting all columns but DEFAULT
X = cc_df.drop(columns=["DEFAULT"]).copy()

# Display the features DataFrame
X.head()

# Define target set by selecting the DEFAULT column
y = cc_df["DEFAULT"]

# Display a sample y
y[:5]
```
- Split the data into training and testing sets:
```python
# Create training and testing datasets using train_test_split
# Assign the function a random_state equal to 1
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)
```
- Fit a scaler to the training data, then use it to transform both the training and testing data:
```python
# Create the StandardScaler instance
X_scaler = StandardScaler()

# Fit the scaler to the features training dataset
X_scaler.fit(X_train)

# Scale both the training and testing data from the features dataset
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
- Import the packages needed to create the neural network:
```python
# Imports
import tensorflow as tf
from tensorflow.keras.layers import Dense
from tensorflow.keras.models import Sequential
```
- Define the number of inputs and the number of hidden nodes, and use those values to build the structure of the model:
```python
# Define the the number of inputs to the model
number_inputs = 22

# Define the number of hidden nodes for the model
number_hidden_nodes = 12

# Create the Sequential model instance
neuron = Sequential()

# Add a Dense layer specifying the number of inputs, the number of hidden nodes, and the activation function
neuron.add(Dense(units=number_hidden_nodes, input_dim=number_inputs, activation="relu"))

# Add the output layer to the model specifying the number of output neurons and activation function
neuron.add(Dense(1, activation="sigmoid"))
```
- Now that the layers have been added, compile the model:
```python
# Compile the Sequential model
neuron.compile(loss="binary_crossentropy", optimizer="adam", metrics=["accuracy"])
```
- Fit the model using 100 epochs:
```python
# Fit the model using 100 epochs and the training data
model = neuron.fit(X_train_scaled, y_train, epochs=100)
```
- Create a plot of the loss function throughout the epochs:
```python
# Create a DataFrame using the model history and an index parameter
model_plot = pd.DataFrame(model.history, index=range(1, len(model.history["loss"]) + 1))

# Visualize the model plot where the y-axis displays the loss metric
model_plot.plot(y="loss")
```
![[cc_default_loss.png]]
- Create a plot of the accuracy per epoch:
```python
# Visualize the model plot where the y-axis displays the accuracy metric
model_plot.plot(y="accuracy")
```
![[cc_default_accuracy.png]]
- As a simplified example, if the model outputs 0.70 when predicting a particular data point, the final prediction would be rounded to 1. If the point in question was actually a 1, then the accuracy of the prediction would be 100%. The loss of the model might be `1 - 0.70` or 0.3.
- Evaluate the model:
```python
# Evaluate the model loss and accuracy metrics using the evaluate method and the test data
model_loss, model_accuracy = neuron.evaluate(X_test_scaled, y_test, verbose=2)

# Display the evaluation results
print(f"Loss: {model_loss}, Accuracy: {model_accuracy}")

# Make predictions on test data
predictions = (neuron.predict(X_test_scaled) > 0.5).astype("int32")

# Create a DataFrame to compare the predictions with the actual values
results = pd.DataFrame({"predictions": predictions.ravel(), "actual": y_test})

# Display sample data
results.head(5)
```
![[cc_default_predictions.png]]
- Next, we will learn more about Deep Learning.
---
>Related Notes: [[Activity - Make Predictions with a NN]]

>Tags: #AI #NN 
