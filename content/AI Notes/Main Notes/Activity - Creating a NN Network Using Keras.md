---
title: Activity - Creating a NN Network Using Keras
created: 2024-05-03T09:16:00
last modified: 2024-05-03 9:15
aliases: 
tags:
  - AI
  - NN
type: NN Predictions
---
- Continuation of [Activity 01-Make_Predictions_With_Neural_Network](file:///C:/Users/anghe/Documents/Work/mbc-ai/06-Neural-Networks/demos/01-Make_Predictions_With_Neural_Network)
- Create an instance of the Sequential model, stored in a variable called `neuron`. The `neuron` variable will store the architecture of your model:
```python
neuron = Sequential()
```
- Create the input and hidden layers. In this step, you are specifying that your input layer will contain two inputs and that your hidden layer will consist of three neurons:
```python
# Define the no. of inputs and hidden nodes
number_inputs = 2
number_hidden_nodes = 1

#Create the input and hidden layers
neuron.add(Dense(units=number_hidden_nodes, activation="relu", input_dim=number_inputs))
```
- Let's look more closely at the parameters we specified above in the `Dense` module:
	- The `input_dim` parameter specifies how many inputs the neuron receives.
	- The `units` parameter specifies the number of neurons in the first hidden layer.
	- The `activation` parameter specifies which type of activation function will process the values of the input features before they are passed to the first hidden layer. By adding this activation function on the first layer, we introduce non-linearity so that our neural network can learn about non-linear relationships as it trains on the data.
- Add the output layer:
```python
# No. of neurons in the output layer
number_classes = 1

# Adding the output layer
neuron.add(Dense(units=number_classes, activation="sigmoid"))
```
- The `units` parameter specifies the number of output neurons. In this demo, we will only include one output neuron in the output layer since we are building a **classification model** that will output a binary decision about each input data point.
- Our output must be **transformed** so that it ranges between 0 and 1, so that the model can map the result to a probability that the input data belongs to Class 1 or to Class 0. To do so, we use the **sigmoid activation function**
- We can check the model structure using the `summary` function:
```python
# Display model summary
neuron.summary()
```
![[tf-neuro-summary.png]]
- The summary displays the structure of each layer in our `neuron` model.
---
>Related Notes: [[Activity - Create a Neural Network]]

>Tags: #AI #NN 
