---
title: Create a Deep Learning Model
created: 2024-05-17T11:51:00
last modified: 2024-05-17 11:51
aliases: 
tags:
  - AI
  - NN
type: Deep Learning
---
- When creating a deep learning model, the goal is to optimize the performance of the model once it has been compiled.
- However, the number of neurons in each layer is equal to or less than the neurons in the layer before it.
- With that in mind, let's step through the design of each layer in the model:
	- **Input layer:** Our review of the data revealed that there are 11 characteristics (or features) in the input data. Hence, our input layer will consist of 11 nodes.
	- **Hidden layers:** Since we are creating a deep learning model, we will use two hidden layers. Our first hidden layer should have fewer neurons than the input layer. Let's say, 8 nodes. Then the second hidden layer should have, maybe 4 nodes, so that it has fewer neurons than the first hidden layer. The activation function we select for both hidden layers is ReLU.
	- **Output layer:** The output layer is the last layer so it will have the fewest neurons. We will use one neuron in our output layer. Since we ultimately need to classify the wine lots on a quality scale ranging from 1-10, the model’s output will be continuous rather than binary. In effect, the model we are building is a **regression model** and not a classification model like before. We will use the linear activation function for the output layer, which is suitable for regression problems.
- Create our deep learning model and add two hidden layers to the model:
```python
# Define the number of inputs and hidden nodes
number_input_features = 11
hidden_nodes_layer1 = 8
hidden_nodes_layer2 = 4

# Create a sequential neural network model
nn = Sequential()

# Add the first hidden layer
nn.add(Dense(units=hidden_nodes_layer1, input_dim=number_input_features, activation="relu"))

# Add the second hidden layer
nn.add(Dense(units=hidden_nodes_layer2, activation="relu"))

# Add the output layer
nn.add(Dense(units=1, activation="linear"))
```
- Note that when adding the second hidden layer, we do not define an `input_dim` parameter. We only define the number of neurons the layer will contain using the `units` parameter and the activation function using the `activation` parameter.
- Next, we will compile and fit the model.
---
>Related Notes: [[Predicting Wine Quality with Deep Learning]]

>Tags: #AI #NN 
