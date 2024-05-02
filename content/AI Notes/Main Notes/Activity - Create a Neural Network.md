---
title: Activity - Create a Neural Network
created: 2024-05-02T09:37:00
last modified: 2024-05-02 9:37
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- There are two ways to code a neural network:
	- You can do all the math and code it from scratch using Python, Pandas, and NumPy.
	- Or, you can use an industry-standard application programming interface (API) or framework to speed up your implementation and focus your efforts on improving your model.
- **TensorFlow** is an open-source platform for machine learning that will allow you to run code across multiple platforms efficiently.
- **Keras** is an abstraction layer on top of TensorFlow that makes it easier to build models.
- Refer to [Activity 01-Make_Predictions_With_Neural_Network](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/demos/01-Make_Predictions_With_Neural_Network) in order to see an example of a basic neural network.
- Import all necessary packages:
```python
# Initial imports
import pandas as pd
from sklearn.datasets import make_blobs
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split

# Keras modules
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
```
- Let’s create a neural network with a single neuron that solves a binary classification problem.
- Create a dummy dataset using the `make_blobs` function from `sklearn`:
```python
X, y = make_blobs(n_samples=1000, centers=2, n_features=2, random_state=1)
```
- As part of data preprocessing, transform `y` into a vertical vector:
```python
# Transforming y to a vertical vector
y = y.reshape(-1, 1)
y.shape
```
```text
(1000, 1)
```
- Create a DataFrame with the dummy data to generate a plot using Pandas' `plot()` method:
```python
# Creating a DataFrame with the dummy data
df = pd.DataFrame(X, columns=["Feature 1", "Feature 2"])
df["Target"] = y

# Plotting the dummy data
df.plot.scatter(x="Feature 1", y="Feature 2", c="Target", colormap="winter")
```
![[neuron-two-blobs.png]]
- As we did with other machine learning algorithms, we’ll use the scikit-learn `train_test_split` function to split the data into training and testing datasets:
```python
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=1)
```
- Before using a neural network, we must normalize, or standardize, our data. This makes it easier for the neural network to adjust the weights in the network.
- Developers commonly use scikit-learn's `MinMaxScaler` or `StandardScaler` functions to scale and normalize input features:
```python
# Create the scaler instance
X_scaler = StandardScaler()

# Fit the scaler
X_scaler.fit(X_train)

# Scale the data
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
---
>Related Notes: [[The Structure of a Neural Network]]
>Tags: #AI #NN 
