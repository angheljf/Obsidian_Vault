---
title: Activity - Make Predictions with a NN
created: 2024-05-06T23:27:00
last modified: 2024-05-06 23:27
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- Using the `predict` function in the neural network model we built will allow you to generate predictions on new data.
- To do this, you have to supply the function with:
	- The data
	- A threshold value
- Any input that is valued below your threshold after being weighted and moving through the layers of the network will be classified as a `0` while anything valued above the threshold will be classified as a `1`.
- To demonstrate, let's create a dummy dataset and then predict the class of the data points with a threshold value of `0.5` for the predict function:
```python
# Create 10 new samples of dummy data
new_X, new_y = make_blobs(n_samples=10, centers=2, n_features=2, random_state=1)

# Make predictions
predictions = (neuron.predict(new_X) > 0.5).astype("int32")
```
- Next, we want to see how the model's predicted classifications, which we’ve stored in the variable `predictions`, compare to the actual classifications for each data point in the dummy dataset:
```python
# Create a DataFrame to compare the predictions with the actual values
results = pd.DataFrame({"predictions": predictions.ravel(), "actual": new_y})

# Display sample data
results.head(10)
```
![[neural-network-predictions.png]]
- As the table shows, the model correctly classified all 10 data points!
---
>Related Notes: [[Activity - Train a Neural Network]]

>Tags: #AI #NN 
