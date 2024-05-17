---
title: Activity - Compile a Neural Network
created: 2024-05-03T09:41:00
last modified: 2024-05-03 9:40
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- Continuation of [Activity 01-Make_Predictions_With_Neural_Network](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/demos/01-Make_Predictions_With_Neural_Network)
- To compile and fit a model, you will need to specify **loss**, **optimization**, and activation functions.
- When training the neural network model on a dataset, you pass the dataset through the model multiple times.
- The **loss function** provides an indicator of how the model's performance changes over each iteration.
- **Optimization functions** shape and mold a neural network while the model is being trained on the data.
- An optimization function reduces the model's losses and provides the most accurate output possible.
- When we fit the model, we also want to keep track of a key evaluation metric: **accuracy**.
- We use model predictive accuracy (`accuracy`) for classification models that are designed to answer whether-or-not type questions, such as the binary classification.
## Compiling the Model
---
- To **compile** the model, you will use the `compile` function from Keras:
```python
neuron.compile(loss="binary_crossentropy", optimizer="adam", metrics=["accuracy"])
```
- In this example, we have passed three parameters to the `compile` function:
	- The loss function, which we use to monitor the model's performance, is specified as the `binary_crossentropy` loss function. This function is designed to deal with binary classification problems.
	- The optimization function, which shapes the network while the model is trained on the data, has been set to `adam`. This optimizer usually finds a good balance between speed and quality when it's searching for the best model fit.
	- We set the observation metric to `accuracy`and we will be hoping for the accuracy metric to get as close to 1 as possible.
---
>Related Notes: [[Activity - Create a Neural Network]], [[Activity - Creating a NN Network Using Keras]]

>Tags: #AI #NN 
