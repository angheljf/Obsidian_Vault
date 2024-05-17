---
title: Activity - Train a Neural Network
created: 2024-05-04T09:11:00
last modified: 2024-05-04 21:10
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- Continuation of [Activity 01-Make_Predictions_With_Neural_Network](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/demos/01-Make_Predictions_With_Neural_Network)
- We will move on to the fitting portion of the process, also known as **training** the neural network model.
- To train your Keras model, you will use the `fit` function and provide:
	- The `x` and `y` training values.
	- The number of epochs. An **epoch** refers to a single pass of the entire training dataset through the model.
- When you fit a neural network model, the optimizer and loss functions adjust the weights of each input during each epoch.
- The following code fits the binary classification model stored in the `neuron` variable:
```python
# Fitting the model
model = neuron.fit(X_train_scaled, y_train, epochs=100)
```
![[fitting-a-neural-network.png]]
- Keeping in mind that our aim is to minimize the loss function and to get the accuracy metric as close to 1 as possible, we can plot the loss function and the accuracy across all epochs to visualize the model's performance.
## Visualizing the Model's Performance
---
- Whenever we fit a neural network, a dictionary of the training results is automatically created.
- The `history` dictionary will have stored all the loss and accuracy results for all epochs.
- After creating the DataFrame, we will use the Pandas `plot` function to plot the loss and the accuracy:
```python
# Create a DataFrame with the history dictionary
df = pd.DataFrame(model.history, index=range(1, len(model.history["loss"]) + 1))

# Plot the loss
df.plot(y="loss")

# Plot the accuracy
df.plot(y="accuracy")
```
- The resulting plots confirm that as the model progresses, the accuracy increases and the loss function decreases.
![[plotting-loss-and-accuracy.png]]
## How Many Epochs?
---
- The approach is generally to start training the model with 20 epochs and then vary that number according to the model’s performance.
- The goal would be to see an improvement in the loss function and accuracy metrics, so we would plot those values over the course of 20 epochs, then continue training the model in increments of 20 epochs until the loss function is getting close to zero and the accuracy metric is getting closer to 1.
## Evaluate Performance Using Test Data
---
- Ultimately, the model’s performance on data that was not used in training is what really matters.
- We'll use the `evaluate` function. Then, we’ll print the testing loss and accuracy values, as shown in the code that follows:
```python
# Evaluate the model using testing data
model_loss, model_accuracy = neuron.evaluate(X_test_scaled, y_test, verbose=2)

# Display evaluation results
print(f"Loss: {model_loss}, Accuracy: {model_accuracy}")
```
![[evaluating-a-neural-network.png]]
- Next, we’ll use our model to make predictions on unseen data.
---
>Related Notes: [[Activity - Compile a Neural Network]]

>Tags: #AI #NN 
